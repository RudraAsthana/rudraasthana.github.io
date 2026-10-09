# Digital Garden & Logbook

A minimalist, text-focused digital garden built with Jekyll and typeset for readability on the small web.

## Licensing

- **Code & Infrastructure:** [GPLv3](LICENSE)
- **Written Content:** [CC BY-NC-ND 4.0](https://creativecommons.org/licenses/by-nc-nd/4.0/)

## Project Structure

```text
rudraasthana.github.io/
├── _layouts/
│   ├── default.html         # Master template with theme toggle & footer
│   └── post.html            # Post template with auto-generated titles & dates
├── _posts/
│   ├── blog/                # Personal reflections and logs
│   ├── guide/               # Technical and procedural manuals
│   └── typeset/             # LaTeX compiled document releases
├── assets/
│   ├── img/                 # Image assets and document thumbnails
│   └── pdf/                 # Downloadable compiled PDFs
├── _config.yml              # Jekyll settings & timezone enforcement
├── index.html               # Homepage with dynamic category routing
├── LICENSE                  # GPLv3 text
├── README.md                # This file
└── styles.css               # High-contrast academic theme & typography limits
```

## Publishing Workflow

### 1. Standard Posts (Blog & Guides)

Create a new Markdown file inside `_posts/blog/` or `_posts/guide/` using the strict `YYYY-MM-DD-title.md` format.

```yaml
---
layout: post
title: "Your Post Title Here"
category: blog # or "guide"
---
```

_Note: Do not manually type `# Your Title` or the date at the top of your markdown body. The `post` layout automatically generates the `h1` heading and the "Date Published" line. Jekyll extracts the exact date entirely automatically directly from your `YYYY-MM-DD` filename._

### 2. Typeset Documents

For LaTeX or PDF documents, the site uses a custom Document Card component for clean downloading.

1. Place your compiled PDF into the `assets/pdf/` directory.
2. Generate a high-quality thumbnail of the first page using Ghostscript:
   ```bash
   \gs -o assets/img/your_file-thumb.jpg -sDEVICE=jpeg -dJPEGQ=85 -r150 -dTextAlphaBits=4 -dGraphicsAlphaBits=4 -dFirstPage=1 -dLastPage=1 assets/pdf/your_file.pdf
   ```
   _(Note: The backslash `\` ensures Zsh does not mistake `gs` for `git status`)._
3. Create a post in `_posts/typeset/` using the standard naming convention, setting the front matter to `category: typeset` and `layout: post`.
4. Paste this HTML at the bottom of your post, updating the respective filenames:
   ```html
   <div class="document-card">
     <div class="document-info">
       <span class="document-filename">your_file.pdf</span>
       <a
         href="{{ '/assets/pdf/your_file.pdf' | relative_url }}"
         class="document-download"
         download
       >
         <i data-lucide="download"></i> Download PDF
       </a>
     </div>
     <img
       src="{{ '/assets/img/your_file-thumb.jpg' | relative_url }}"
       class="document-thumbnail"
       alt="Document Thumbnail"
     />
   </div>
   ```

### 3. Adding Footnotes & Citations

Use Kramdown's native footnote syntax. Add `[^1]` inline where you want the number to appear. Then, at the bottom of your markdown file, define the footnote content:

```markdown
Here is a factual claim.[^1]

[^1]: This is the citation or expanded thought.
```

## ⚠️ Future Reference & Formatting Gotchas

### HTML inside Markdown

Markdown was fundamentally designed to be fully compatible with raw HTML. You can drop structural components (like the Document Card) directly into a `.md` file. However, Markdown parsers usually ignore Markdown syntax placed _inside_ raw block-level HTML tags. If you need to format text inside a `<div>`, use standard HTML tags like `<strong>` or `<em>` instead of `**` or `*`.

### CSS Flexbox & Image Crushing

By default, CSS Flexbox applies `flex-shrink: 1` to all children. If a flex container holds a long, unbroken string of text alongside an image, the browser will aggressively crush the image to make room for the text. This is prevented globally in `styles.css` using `flex-shrink: 0` and explicit `min-width` rules on thumbnails, coupled with `overflow-wrap: break-word` on text containers.

### Sub-Pixel Anti-Aliasing

Ghostscript renders text with jagged edges by default. Always include `-dTextAlphaBits=4` and `-dGraphicsAlphaBits=4` when extracting thumbnails from PDFs to force smooth font rendering. This is especially critical when dealing with complex LaTeX output.

### Draft Status

Jekyll ignores files unless their filenames strictly follow the `YYYY-MM-DD-title.md` format. To keep a post unpublished, you can simply remove the date from the filename or add `published: false` to the YAML front matter.
