# Digital Garden & Logbook

A minimalist, text-focused digital garden built with Jekyll and typeset for readability on the small web.

## Licensing

- **Code & Infrastructure:** [GPLv3](LICENSE)
- **Written Content:** [CC BY-NC-ND 4.0](https://creativecommons.org/licenses/by-nc-nd/4.0/)

## Project Structure

```text
rudraasthana.github.io/
├── _layouts/
│   └── default.html         # Master template with theme toggle & footer
├── _posts/
│   ├── blog/              # Personal reflections and logs
│   ├── guide/             # Technical and procedural manuals
│   └── typeset/           # LaTeX-compiled document releases
├── assets/
│   ├── img/               # Image assets and document thumbnails
│   └── pdf/               # Downloadable compiled PDFs
├── _config.yml              # Jekyll settings & timezone enforcement
├── favicon.svg              # 16x16 Pixel Art
├── index.html               # Homepage with dynamic category routing
├── LICENSE                  # GPLv3 text
├── README.md                # This file
└── styles.css               # Catppuccin theme & typography limits
```

## Publishing Workflow

### 1. Standard Posts (Blog & Guides)

Create a new Markdown file inside `_posts/blog/` or `_posts/guide/` using the `YYYY-MM-DD-title.md` format.

```yaml
---
layout: default
title: "Your Post Title Here"
category: blog # or "guide"
---
```

### 2. Typeset Documents

For LaTeX or PDF documents, the site uses a custom Document Card component for clean downloading.

1. Place your compiled PDF into the `assets/pdf/` directory.
2. Generate a thumbnail of the first page using Ghostscript:
   ```bash
   \gs -o assets/img/your_file-thumb.jpg -sDEVICE=jpeg -dJPEGQ=85 -r150 -dTextAlphaBits=4 -dGraphicsAlphaBits=4 -dFirstPage=1 -dLastPage=1 assets/pdf/your_file.pdf
   ```
   _(Note: The backslash `\` ensures Zsh does not mistake `gs` for `git status`)._
3. Create a post in `_posts/typeset/` using the standard naming convention, setting the front matter to `category: typeset`.
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

### 4. Format and Deploy

Run Prettier to ensure all formatting remains perfectly aligned before deploying to GitHub Pages.

```bash
npx prettier --write "**/*.{html,css,md,yml}"
git add .
git commit -m "Publish: [Post Title]"
git push
```
