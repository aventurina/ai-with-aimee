# AI with Aimee 🤖

My public notebook for learning AI: what I try, what surprises me, and what I get wrong along the way. Built with [Astro](https://astro.build), so every post is a version-controlled Markdown file that builds straight into a fast, static site.

![AI with Aimee Blog Screenshot](./screenshot-ai-with-aimee.png)

**[View the live blog →](https://ai-with-aimee.vercel.app/)**

## Features

- Fast and lightweight: generates pure static HTML with minimal JavaScript
- Markdown-first: write posts in clean, simple Markdown
- Minimal, distraction-free design
- Fully responsive on desktop, tablet, and mobile
- Tagging system to organize posts
- Posts sort automatically by publish date
- Deploys anywhere: Vercel, Netlify, GitHub Pages, and more

## Tech stack

- Framework: [Astro](https://astro.build), a static site generator built for content-driven sites
- Content: Markdown with frontmatter metadata
- Styling: CSS, kept minimal and easy to customize
- Deployment: static site generation (SSG)
- Node.js: v16+ recommended

## Quick start

### 1. Install and set up

```bash
npm install
```

### 2. Start the development server

```bash
npm run dev
```

Visit `http://localhost:3000`, your blog is ready with hot reload enabled.

### 3. Create a new post

Add a new file to `src/content/blog/`, for example `my-new-post.md`:

```markdown
---
title: My New Post
description: A short summary that appears in the blog list
pubDate: 2026-09-11
author: Aimee
tags: ["ai", "learning-journey"]
---

# My New Post

Write your content here in Markdown...
```

Posts appear instantly on the home page, sorted by date, newest first.

### 4. Deploy

```bash
npm run build
```

Deploy the `dist/` folder to your hosting provider.

## Writing blog posts

### File location

All blog posts live in `src/content/blog/` as `.md` files, for example `building-a-rag-chatbot-with-local-embeddings.md` and `why-im-starting-my-ai-learning-journey.md`.

Filenames use kebab-case:
- `my-awesome-post.md` becomes `/blog/my-awesome-post`

### Post frontmatter

Every post needs this frontmatter (YAML) at the top:

```markdown
---
title: "Your post title"              # Required
description: "Short summary"          # Required, appears in the blog list
pubDate: 2026-09-11                   # Required, YYYY-MM-DD format
author: "Aimee"                       # Optional
tags: ["tag1", "tag2", "tag3"]        # Optional, can have multiple
---
```

### Writing tips

- Standard Markdown syntax works throughout: `#`, `##` for headings, `**bold**`, `*italic*`, and so on.
- Code blocks get syntax highlighting automatically.
- Links, lists, tables, and images are all supported.
- Draft mode: rename a file to start with an underscore (`_draft-post.md`) to exclude it from the build.

## Project structure

```
src/
├── pages/
│   ├── index.astro                  # Home page (lists all posts)
│   └── blog/
│       └── [...slug].astro          # Single post template
├── content/
│   ├── config.ts                    # Content collection schema
│   └── blog/
│       └── *.md                     # Individual posts
├── components/                      # Reusable Astro components
├── styles/                          # Global styles
└── layouts/                         # Layout templates

astro.config.mjs                      # Astro configuration
package.json                          # Project dependencies
```

## Customization

### Change the blog title and tagline

Edit `src/pages/index.astro`:

```astro
<h1>Your Blog Name</h1>
<p class="subtitle">Your tagline here</p>
```

### Customize colors and fonts

Edit the `<style>` section in:
- `src/pages/index.astro`, home page styling
- `src/pages/blog/[...slug].astro`, post page styling

### Add more pages

Create new files in `src/pages/`:
- `src/pages/about.astro` becomes `/about`
- `src/pages/projects.md` becomes `/projects`

Use `.astro` for dynamic content or `.md` for static Markdown pages.

## Deployment

### Vercel (recommended)

1. Push code to GitHub.
2. Go to [vercel.com](https://vercel.com) and import the repo.
3. Vercel auto-detects Astro and deploys automatically.
4. Every push to main redeploys instantly.

### Netlify

1. Push code to GitHub.
2. Go to [netlify.com](https://netlify.com) and connect the repo.
3. Netlify detects the Astro config automatically.

### GitHub Pages

1. Build locally: `npm run build`.
2. Push the `dist/` folder to a `gh-pages` branch.
3. Enable GitHub Pages in repo settings.

### Other static hosts

Since Astro generates pure static HTML, this also deploys to Firebase Hosting, AWS S3 + CloudFront, Azure Static Web Apps, or any web server that serves static files.

## Performance

- Zero JavaScript by default: pure HTML and CSS
- Static content served at CDN speeds
- Minimal dependencies, no bloated frameworks
- SEO-friendly: clean HTML, fast page loads, proper metadata

## Resources

- [Astro documentation](https://docs.astro.build)
- [Astro content collections guide](https://docs.astro.build/en/guides/content-collections/)
- [Markdown syntax reference](https://www.markdownguide.org/)
- [YAML frontmatter guide](https://jekyllrb.com/docs/front-matter/)

## License

MIT License, feel free to use this as a starting point for your own blog.
