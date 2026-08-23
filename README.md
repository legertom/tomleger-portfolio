# tomleger.dev

Personal site of Tom Léger — AI Enablement Lead · Full-Stack Builder. New York, NY.

## What this is

A single, self-contained `index.html` — no framework, no build step, no dependencies beyond two Google Fonts. Deployed via GitHub Pages (`CNAME` → tomleger.dev).

- **Work** — case studies of AI builds at Clever (The AI Exchange, Casespace, Formula Studio, PMAT, a citation-first RAG assistant, SSO Explorer). Most are internal, so they're described, not linked; [formulastudio.net](https://www.formulastudio.net), [exampledistrict.com](https://www.exampledistrict.com), and the [PMAT course](https://github.com/legertom/clever-pmat-course) are public.
- **Enablement** — the AI Leads champion program, company-wide L&D, and the Clever AI Playbook.
- **Skills / Career / Contact** — the rest of the picture.

## Editing

Everything lives in `index.html`: content in semantic HTML, design tokens as CSS variables at the top of the `<style>` block (light theme on `:root`, dark theme via `prefers-color-scheme` plus a `data-theme` toggle).

The resume link points to `Tom-Leger-Resume.pdf` in the repo root — replace that file to update the resume.

## Deploying

Push to `main`; GitHub Pages does the rest.
