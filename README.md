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
│   ├── blog/
│   │   └── YYYY-MM-DD-title.md  ( * as many logs as published * )
│   └── guide/
│       └── YYYY-MM-DD-title.md  ( * as many manuals as published * )
├── _config.yml              # Jekyll settings & timezone enforcement
├── favicon.svg              # 16x16 Pixel Art
├── index.html               # Homepage with dynamic category routing
├── LICENSE                  # GPLv3 text
├── README.md                # This file
└── styles.css               # Catppuccin theme & typography limits
```

## Publishing Workflow

### 1. Create a Post

Create a new Markdown file inside either `_posts/blog/` or `_posts/guide/`. The filename **must** follow the `YYYY-MM-DD-title.md` format.

At the very top of the file, insert the YAML front matter:

```yaml
---
layout: default
title: "Your Post Title Here"
category: blog # or "guide"
---
```

Write your content directly below the second `---` using standard Markdown.

### 2. Format the Code (Optional but Recommended)

Run Prettier to ensure all markdown spacing, HTML indentation, and CSS syntax remain perfectly formatted:

```bash
npx prettier --write "**/*.{html,css,md,yml}"
```

### 3. Test Locally

Preview the changes on your Fedora environment before pushing to the live site:

```bash
jekyll serve
```

_(If port 4000 is blocked, append `--port 4001`)._

### 4. Deploy to GitHub Pages

Push the new markdown files to the repository. GitHub Actions will automatically detect the push, compile the Jekyll site, and update the live domain within 60 seconds.

```bash
git add .
git commit -m "Publish: [Post Title]"
git push
```
