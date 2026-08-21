# AI with Aimee 🤖

A modern, lightweight technical blog for exploring AI, web development, and tech innovation. Built with [Astro](https://astro.build) for blazing-fast performance and an optimal reading experience.

![AI with Aimee Blog Screenshot](./screenshot-ai-with-aimee.png)

**[👉 View the Live Blog →](https://ai-with-aimee.vercel.app/)**

## Features

✨ **Fast & Lightweight** – Generates pure static HTML with minimal JavaScript  
📝 **Markdown-First** – Write posts in clean, simple Markdown  
🎨 **Beautiful by Default** – Minimal, distraction-free design  
📱 **Fully Responsive** – Perfect on desktop, tablet, and mobile  
🏷️ **Tagging System** – Organize posts with flexible tags  
🔄 **Auto-Sorting** – Posts automatically sorted by publish date  
⚡ **Zero Configuration** – Start writing immediately, no setup hassle  
🚀 **Deploy Anywhere** – Works with Vercel, Netlify, GitHub Pages, and more  

## Tech Stack

- **Framework**: [Astro](https://astro.build) – The web framework for content-driven sites
- **Content**: Markdown with frontmatter metadata
- **Styling**: CSS (customizable, minimal framework overhead)
- **Deployment**: Static site generation (SSG)
- **Node.js**: v16+ recommended

## Quick Start

### 1. Install & Setup
```bash
npm install
```

### 2. Start Development Server
```bash
npm run dev
```
Visit `http://localhost:3000` – your blog is ready with hot reload enabled.

### 3. Create Your First Post
Create `src/content/blog/my-first-post.md`:
```markdown
---
title: My First Blog Post
description: A short summary that appears in the blog list
pubDate: 2026-08-21
author: Your Name
tags: ["astro", "blogging"]
---

# My First Post

Write your content here in Markdown...
```

Posts appear instantly on your home page, sorted by date (newest first).

### 4. Deploy
```bash
npm run build
```
Deploy the `dist/` folder to your hosting provider.

## Writing Blog Posts

### File Location
All blog posts go in `src/content/blog/` as `.md` files.

**Filename Format**: Use kebab-case  
- `my-awesome-post.md` → `/blog/my-awesome-post`
- `astro-tips-and-tricks.md` → `/blog/astro-tips-and-tricks`

### Post Frontmatter

Every post requires this frontmatter (YAML) at the top:

```markdown
---
title: "Your Post Title"              # Required
description: "Short summary"           # Required (appears in blog list)
pubDate: 2026-08-21                   # Required (YYYY-MM-DD format)
author: "Your Name"                   # Optional
tags: ["tag1", "tag2", "tag3"]        # Optional (can have multiple)
---

# Your post content starts here...
```

### Writing Tips

- Use standard Markdown syntax (`#`, `##` for headings, `**bold**`, `*italic*`, etc.)
- Code blocks work automatically with syntax highlighting
- Links, lists, tables, and images all supported
- Posts are fully styled with consistent typography
- **Draft mode**: Rename files starting with underscore (`_draft-post.md`) to exclude from builds

## Project Structure

```
src/
├── pages/
│   ├── index.astro                  # Home page (lists all posts)
│   └── blog/
│       └── [...slug].astro          # Single post template
├── content/
│   ├── config.ts                    # Content collection schema
│   └── blog/
│       ├── first-post.md            # Sample post (delete this)
│       └── your-posts.md            # Add your posts here
├── components/                      # Reusable Astro components
├── styles/                          # Global styles
└── layouts/                         # Layout templates

astro.config.mjs                      # Astro configuration
package.json                          # Project dependencies
```

## Customization

### Change Blog Title & Tagline
Edit `src/pages/index.astro`:
```astro
<h1>Your Blog Name</h1>
<p class="subtitle">Your tagline here</p>
```

### Customize Colors & Fonts
Edit the `<style>` section in:
- `src/pages/index.astro` – Home page styling
- `src/pages/blog/[...slug].astro` – Post page styling

Update CSS variables or add custom colors/fonts to match your brand.

### Add More Pages
Create new files in `src/pages/`:
- `src/pages/about.astro` → `/about`
- `src/pages/projects.md` → `/projects`
- `src/pages/contact.astro` → `/contact`

Use `.astro` for dynamic content or `.md` for static Markdown pages.

## Deployment

### Vercel (Recommended)
1. Push code to GitHub
2. Go to [vercel.com](https://vercel.com) and import your repo
3. Vercel auto-detects Astro and deploys automatically
4. Every push to main redeploys instantly

### Netlify
1. Push code to GitHub
2. Go to [netlify.com](https://netlify.com) and connect your repo
3. Netlify detects Astro config automatically
4. Your site is live with every commit

### GitHub Pages
1. Build locally: `npm run build`
2. Push `dist/` folder to `gh-pages` branch
3. Enable GitHub Pages in repo settings

### Other Static Hosts
Since Astro generates pure static HTML, deploy to:
- Firebase Hosting
- AWS S3 + CloudFront
- Azure Static Web Apps
- Any web server that serves static files

## Performance

This blog is optimized for speed:
- ⚡ **Zero JavaScript** by default (pure HTML & CSS)
- 🚀 **Instant loads** – static content served at CDN speeds
- 📦 **Minimal dependencies** – no bloated frameworks
- 🎯 **SEO-friendly** – clean HTML, fast page loads, proper metadata

## Resources

- [Astro Documentation](https://docs.astro.build)
- [Astro Content Collections Guide](https://docs.astro.build/en/guides/content-collections/)
- [Markdown Syntax Reference](https://www.markdownguide.org/)
- [YAML Frontmatter Guide](https://jekyllrb.com/docs/front-matter/)

## Contributing

Found a bug or want to improve this blog template? Feel free to:
1. Fork this repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

MIT License – Feel free to use this for personal or commercial projects.

---

**Happy blogging!** ✍️ Start writing amazing content today.
