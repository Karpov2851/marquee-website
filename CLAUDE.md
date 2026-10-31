# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Role and scope

Everything in this folder is client-side landing page development. When working here, act as a seasoned HTML/CSS developer and designer:

- Write semantic, accessible, mobile-first HTML and CSS. Plain HTML/CSS/vanilla JS is the default; only add a framework or build step if asked.
- Prioritise performance (small payloads, optimised images, minimal blocking scripts and fonts) and a premium, restrained visual feel.
- Make design decisions the way a designer would (hierarchy, spacing, type scale, contrast), and explain notable ones briefly.
- Treat `Main-html/` as the visual reference and `Original Req/` as the requirements.

## Useful skills

- `/run`: serve a page and check it in a browser.
- `anthropic-skills:built-in-browser` or `anthropic-skills:chrome-browser`: preview pages, check responsive widths, and read console errors.
- `anthropic-skills:canvas-design`: static visual assets such as OG images and posters.
- `artifact-design`: design guidance for polished standalone HTML pages (also shareable as Artifacts).
- `simplify` and `code-review`: clean up and review changes before handing off.
- `security-review`: use on the enquiry form and any scripts that handle user input.
- `/graphify`: map the project once it has real code.
- `archify`: site-map or flow diagrams.

## Project

Website for **Marquee Social** (Mumbai web studio). The repo is not a built application yet. It holds the client brief, a first-draft page, and a design mockup. There is no package.json, build, lint or test tooling, and the directory is not a git repository.

- `Original Req/` is the source of truth for requirements.
  - `marquee-social-website-brief.md` (also as a PDF) is the client brief. Read it before building anything.
  - `logo.png` is the black and silver logo.
  - `index.html` is a self-contained earlier draft (single page, inline CSS, Syne and Inter fonts).
- `Main-html/` is a design mockup exported from a visual design tool. Its README says to treat it as a **reference, not production code**: replicate its values (colors, font sizes, spacing, radii, shadows, layout) in the real implementation instead of copying it wholesale.
  - `Main.dc.html` is the artboard, an `<x-dc>` template plus a `DCLogic` class in `<script type="text/x-dc" data-dc-script>`. The design values are in inline `style=""` attributes and the `<helmet><style>` block.
  - `support.js` and `vendor/react*.js` are the runtime that renders `.dc.html` files. `support.js` is generated ("do not edit"), so don't modify it.
  - `assets/` holds the single uploaded image.
- `Main-html.zip` is an archive of `Main-html/`. Don't edit it, and regenerate it if the folder changes.

## Viewing the mockup

Serve the folder, because some browsers block the scripts over `file://`:

```
cd Main-html && python3 -m http.server
```

Then open `Main.dc.html`. `Original Req/index.html` opens directly in a browser.

## Target site (from the brief)

- **Three pages.**
  - Home: hero, selected work, services, 3 testimonials, closing CTA.
  - Work: portfolio, a 5-step process (Kickoff, Design, Build, Review, Launch), capability notes.
  - Pricing & Contact: Static vs Dynamic packages, enquiry form with email notification.
  - The mockup is a single scrolling page with `#work`, `#services`, `#pricing` and `#contact` sections.
- **Requirements.**
  - Mobile-first and fast.
  - WhatsApp click-to-chat and click-to-call on every page. Phone 8850930003, email marqueesocial22@gmail.com.
  - Basic SEO: meta titles and descriptions, alt text, sitemap.
  - Google Analytics and Search Console ready.
  - Scroll-triggered reveals.
- **Design system.** The mockup defines it in `:root`:
  - Colors: `--bg:#030303`, `--surface:#0d0d0d`, `--text:#f0f0f0`, `--muted:#777`, `--silver:#c8c8c8`, `--accent:#d0d0d0`, `--border:#1a1a1a`.
  - Fonts: Syne 700/800 for headings and Inter for body.
  - The brief still says the single accent colour is "to be defined" and should match the logo.
- **Tone.** Confident, clear, direct, with short sentences and no fluff.
- **Pricing.** Static is INR x and dynamic is INR y; both are still placeholders in the brief.

## Mockup behavior to preserve

`Main.dc.html`'s `Component` class mounts these in `componentDidMount`:

- Custom dot and ring cursor (`body{cursor:none}`).
- Nav that gains a blurred background after scrolling 40px.
- Full-hero WebGL fbm-noise shader canvas (`#gl`) that follows the mouse and hides itself if WebGL is unavailable.
- Scroll reveal.
- Draggable work strip (`#wt`).
- Contact form handler (`#msf`).
- A grain overlay.

Keep a fallback for touch devices (no custom cursor) and for WebGL failure, since the brief demands mobile-first and fast loads.
