---
title: "Building a RAG Chatbot with Local Embeddings and the Claude API"
description: "How retrieval-augmented generation actually works, and how to build a small version of it yourself, grounded answers, cited sources, and a local embedding model that keeps it nearly free to run."
pubDate: 2026-09-11
author: Aimee
tags: ["rag", "claude", "ai", "tutorial"]
---

# Building a RAG Chatbot with Local Embeddings and the Claude API

One of the things I built while working through this AI learning journey is [doc-chat](https://github.com/aventurina/doc-chat), a small app that lets you upload a document and ask it questions, with every answer pointing back to the exact passage it came from. The technique behind it is called retrieval-augmented generation, or RAG, and it was one of those concepts that sounded intimidating right up until I actually built one myself. Once I did, it stopped feeling like a buzzword and started feeling like something I genuinely understood.

This is the walkthrough I wish I'd had when I started.

## What you'll learn

How RAG actually works, and how to build a small version of it yourself: a document upload and chat flow where answers are grounded in the document's real content, with sources cited inline. Along the way you'll see why splitting the work into a free local step and one paid API call is what keeps the whole thing inexpensive to run.

## Prerequisites

- Node.js installed
- An API key from [console.anthropic.com](https://console.anthropic.com/)
- Basic familiarity with Express
- No machine learning background needed. The embedding model does its job without you having to understand how it works internally, I certainly didn't when I started.

## Step by step

### Step 1: Chunk the document

When someone uploads a document, don't hand the whole thing to a language model at once. Split it into overlapping segments instead. Overlap matters: if you cut chunks with hard, non-overlapping edges, you risk splitting a sentence or an idea right at the boundary, and losing the context that made it answerable.

### Step 2: Generate embeddings locally

Each chunk gets converted into an embedding. In plain terms, an embedding turns a piece of text into a list of numbers that captures what it means, not just the words used. Text with similar meaning ends up with numbers that are close together, even when the wording is completely different, so a chunk about "returning a product" and one about "sending something back for a refund" would land near each other, even though they don't share a single word.

This is done with a small local model (`all-MiniLM-L6-v2` via `@huggingface/transformers`), which runs on CPU with no API key and no per-call cost. This is the step most tutorials skip past, but it's the one that makes the whole approach affordable, and honestly, the one I found most interesting once I understood what it was actually doing.

### Step 3: Store the embeddings

For a small demo, a full vector database is overkill. An in-memory array with cosine similarity search is enough: no database to set up, no external service, and it's simple to reason about.

Cosine similarity is just a way of measuring how alike two embeddings are. Since each embedding is a list of numbers pointing in some direction, two chunks about the same topic end up pointing in roughly the same direction. Cosine similarity checks how closely those directions line up, the closer they point, the more related the chunks are, without you ever needing to know what any individual number means.

The trade-off with an in-memory store is that everything disappears when the server restarts, which is a fine trade for a demo and a bad one for anything you'd want to keep long-term.

### Step 4: Embed the question

When someone asks a question, embed it the same way you embedded the document chunks, locally, with the same model. This keeps the question and the chunks in the same vector space so they can be compared directly.

### Step 5: Retrieve the most relevant chunks

Run a cosine similarity search between the question's embedding and every stored chunk, then keep the handful that score highest. This is the "retrieval" half of retrieval-augmented generation, and it's still entirely free, nothing has touched a paid API yet.

### Step 6: Send the question and the retrieved chunks to Claude

Only now does Claude enter the picture. Send it the original question along with the specific chunks retrieved in Step 5, and ask it to answer using only that material. This is what keeps answers grounded instead of hallucinated: Claude never sees the whole document, only the pieces that are actually relevant, so it can't wander off and invent something the document doesn't say.

### Step 7: Return the answer with citations

Have Claude reference which excerpt it used for each part of its answer, and show that excerpt to the user alongside the response. This is what turns "trust me" into something a reader can actually verify, and it's my favorite part of the whole build.

## Why these choices

Embeddings and generation are different problems, and treating them differently is the whole point of this approach. Embeddings are a solved, inexpensive problem: a small local model handles them for free. Generation is where you actually need a strong language model, so that's the one place Claude gets involved, and the only step that costs money per call. Splitting them this way means the app stays testable and runnable without needing a live API key for anything except the final answer, and it keeps the cost surface to a single, controllable API instead of spreading spend across every step.

## Common pitfalls

- **PDF extraction fails silently on scanned or image-based PDFs.** Text extraction tools like `pdf-parse` only work on PDFs that actually contain text, not ones that are just images of text. Test with a real scanned document early, not just clean, text-native ones.
- **Chunking without overlap loses context at the edges.** If a relevant sentence gets split across two chunks with no overlap, neither chunk alone may contain enough context to be retrieved correctly.
- **Forgetting to cap `max_tokens`.** Without a cap, a single unusual request can generate a much longer, more expensive response than expected. Set the cap before you deploy, not after you get a surprising bill.
- **No rate limiting on a public demo.** If you're putting this somewhere public, add a request limit before you share the link, not after.

## What's next

The live version of this is running at [doc-chat-fdzl.onrender.com](https://doc-chat-fdzl.onrender.com), and the full code is in the [doc-chat repo](https://github.com/aventurina/doc-chat), including the actual architecture diagram and a more detailed breakdown of the cost controls. From here, the natural next steps are swapping the in-memory store for a persistent vector database, adding per-user sessions so documents don't leak between visitors, and adding a re-ranking step to improve retrieval quality on longer documents.

If you end up building your own version of this, I'd love to hear how it goes. And if something here doesn't quite make sense, that's useful too, tell me, and I'll fix it for the next person who reads it.
