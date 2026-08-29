# Persianate Collective — website

A two-page site for Persianate Collective, a three-week immersive school of
Persian language, literature and culture, held in Lucknow, India. No build
step, no dependencies to install — plain HTML, CSS and JavaScript, shared
across both pages, plus Google Fonts loaded over a CDN link.

## Structure

```
persianate-collective/
├── index.html        the main page: hero, details strip, about, weeks,
│                     faculty, texture, who-it's-for, FAQ, contact + fee
│                     breakdown, footer
├── apply.html        the application page: info sidebar (left) + detailed
│                     application form (right)
├── css/
│   └── styles.css    shared by both pages — colors, type, the fluid
│                     gradient sections, the hero's string field, and the
│                     apply page's own layout, all in one file
├── js/
│   └── script.js     shared by both pages — each page only runs the parts
│                     that find matching elements, so nothing errors on
│                     apply.html for the sections it doesn't have (nav,
│                     hero string field, faculty carousel, FAQ accordion)
└── README.md
```

**The two pages are linked, not independent.** Every "Apply now" on
`index.html` (hero button, the pill fixed to the top-right corner, the
footer button, and "Apply" in the bottom nav) points to `apply.html`.
`apply.html` links back with "← Back to the full programme" and a link to
the FAQ. Keep both files at the same folder level (as they are here) and
these relative links resolve correctly with no further setup.

## Viewing it locally

There's nothing to build. Either:

- Open `index.html` directly in a browser, or
- Serve the folder locally so relative paths behave exactly as they will
  once hosted, e.g. `python3 -m http.server`, then visit
  `http://localhost:8000`.

## Deploying with GitHub Pages

1. Push this folder to a GitHub repository.
2. In the repo, go to **Settings → Pages**.
3. Under "Build and deployment", set **Source** to "Deploy from a branch",
   pick your default branch and the `/ (root)` folder, then save.
4. GitHub will publish the site at `https://<username>.github.io/<repo>/`,
   with the application page at `.../apply.html`, within a minute or two.

No custom domain, build step, or GitHub Action is required for this to work.
If you move `apply.html` into a subfolder later, update the four links on
`index.html` (search for `apply.html`) to match its new path.

## Things to do before this goes live

Everything below reads as real content on the page, but it's dummy data
standing in for the real thing:

- **Location, dates, fee, and deadline.** These appear in more than one
  place — the details strip on `index.html`, the fee box in its Contact
  section, several FAQ answers, and the facts list on `apply.html` — all
  currently: Lucknow, India; 7–27 June 2027; $2,200; 1 April 2027. They're
  written to be consistent with each other, so if you change one, change
  all of them (search each value across both HTML files).
- **The application form** (`#enquiry-form` on `apply.html`) is front-end
  only right now — submitting it shows a confirmation message but doesn't
  send anywhere. There's a marked spot in `js/script.js` (search for
  `enquiry-form`) to wire it to a real endpoint — Formspree and Netlify
  Forms are both drop-in options that need no backend of your own.
- The contact section on `index.html` also lists a placeholder address,
  `hello@persianatecollective.org` — swap that for the real one.
- **Faculty profiles** in the "Who's teaching" carousel are dummy content —
  four repeated "Faculty Name" cards with generic role labels and a
  bracketed prompt in place of a real bio. Replace the `data-name`,
  `data-role`, `data-gloss` and `data-bio` attributes on each
  `.faculty-card` button in `index.html`, and swap the placeholder portrait
  icon for a real photo if you want one.
- The "photograph" plates on `index.html` (About, Texture) and the cover
  banner on `apply.html` are illustrated placeholders, not real photography
  — a deliberate choice, so nothing that looks like a real photo of real
  people ends up on the live site without a proper license. Swap in real
  images once you have them.

## Notes on how it's built

- Typography: Instrument Serif for headings, Inter for body and UI text,
  Noto Nastaliq Urdu and Vazirmatn for the Persian script throughout.
- The hero's hanging words are physics-driven (a damped spring per string)
  and play a short synthesized chime on hover via the Web Audio API — not a
  sampled instrument. Most browsers block audio until the visitor has
  clicked somewhere on the page at least once; that's a browser autoplay
  policy, not a bug.
- Motion respects `prefers-reduced-motion`: the string field, scroll
  reveals, and the fluid-gradient sections all fall back to a static state.
- No frameworks, no build tools, no npm install — everything runs as
  authored.
