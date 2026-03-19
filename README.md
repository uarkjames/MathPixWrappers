# MathPix Wrappers for Blackboard Ultra

Self-contained HTML wrapper/renderer files for displaying [Mathpix](https://mathpix.com/) PDF conversion outputs inside **Blackboard Ultra** HTML document blocks.

## Background

Mathpix converts PDFs into a variety of formats (Markdown, Mathpix Markdown, LaTeX, HTML, and others). The HTML export renders beautifully when pasted directly into an Ultra HTML block — but the other formats just download as files when students click them, rather than displaying inline.

These wrappers solve that by giving each format a self-contained HTML file that renders the content client-side, entirely from CDN-loaded libraries. No server, no build tools, no framework. Paste your content in, upload to Ultra, done.

## The Wrappers

### 1. `MarkedForUltra.html` — Markdown
For standard Markdown output from Mathpix (or any Markdown source). Uses [marked.js](https://marked.js.org/) loaded from CDN.

**Use when:** your Mathpix export is plain `.md` with no math notation.

---

### 2. `Marked+MathJaxForUltra.html` — Markdown with Math
For Markdown content that contains incidental LaTeX math fragments — the kind Mathpix sprinkles in for things like author footnotes (`${ }^{\mathbf{1}}$`), inline equations (`$E = mc^2$`), or display math (`$$...$$`).

Uses marked.js for Markdown rendering and [MathJax](https://www.mathjax.org/) for math typesetting, with a stash/restore pattern to prevent the two libraries from interfering with each other.

**Use when:** your Mathpix Markdown export has math notation mixed in but isn't a heavily math-oriented document.

---

### 3. `MathpixMarkdownForUltra.html` — Mathpix Markdown (MMD)
For full [Mathpix Markdown](https://mathpix.com/docs/mathpix-markdown/overview) (`.mmd`) output. Uses Mathpix's own official [`mathpix-markdown-it`](https://github.com/Mathpix/mathpix-markdown-it) browser bundle, which handles the complete MMD spec in one script.

Supports everything in the other two wrappers, plus:
- Numbered equations (`\begin{equation}...\end{equation}`)
- LaTeX tables (`\begin{tabular}...\end{tabular}`)
- Chemistry notation (`\ce{H2O}`)
- Author lists and abstract blocks

**Use when:** your Mathpix export is a `.mmd` file, or a math/science document with heavy LaTeX content.

---

## How to Use

### Step 1 — Pick the right wrapper
See the table above. When in doubt, start with `MathpixMarkdownForUltra.html` — it handles the most.

### Step 2 — Paste your content
Open the wrapper file in a text editor. Find the clearly marked paste zone:

```html
<!-- ============================================================
     PASTE YOUR MARKDOWN BELOW (between the script tags).
     ============================================================ -->
<script type="text/plain" id="markdown-source">

  ... your content goes here ...

</script>
<!-- ============================================================
     END OF PASTE ZONE
     ============================================================ -->
```

Select and replace everything between the `<script>` tags with your Mathpix output. Save the file.

### Step 3 — Add to Blackboard Ultra
1. Open your Ultra course and create or edit a **Document**
2. Add an **HTML Block**
3. Paste the entire contents of the wrapper file into the HTML block
4. Save — your content renders inline for students

---

## Requirements

- A Blackboard Ultra course with permission to add HTML blocks
- Internet access from the Ultra environment (the wrappers load libraries from CDN at render time)
- A text editor for the paste step (VS Code, Notepad++, anything works)

---

## Notes

- All styling is scoped to the `#rendered-output` div and should not conflict with Ultra's own CSS
- The wrappers are intentionally minimal — no frameworks, no dependencies to manage, no build step
- CDN libraries are pinned to stable channels; if you need reproducible long-term deployments, consider pinning to specific version numbers in the script `src` URLs

---

*Generated with [Claude](https://claude.ai) (Anthropic) as part of a Mathpix PDF accessibility evaluation at the University of Arkansas.*
