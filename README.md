# The Withered Key

A forensic, statistics-first reading of the **Voynich Manuscript** (Beinecke MS 408), presented as an interactive report styled after a botanical dichotomous key.

**Live:** _(add your URL here after deploy)_

## What this is

A single self-contained `index.html` — no build step, no dependencies to install. It renders a twelve-experiment investigation that tests four hypotheses about the manuscript to destruction or survival:

1. **Random gibberish** — ruled out
2. **A simple cipher** (incl. the 2025 Naibbe card-cipher claim) — ruled out
3. **An enciphered natural language** — strongly doubted
4. **A hand-executable generative artefact** — best fit, with one open door

The page walks each fork step by step in both plain-English and (via a header toggle) full technical detail, with 12 live Chart.js figures, a held-out reconstruction table, a five-step "how a scribe did this in 1420" recipe, an adversarial six-channel hidden-message audit, and a tappable glossary.

### Tech notes
- Pure static HTML/CSS/JS. Chart.js and Google Fonts load from CDN.
- No cookies, no storage, no server. Works offline once the CDN assets are cached.
- Anonymous, cookie-less page-view counts via Cloudflare Web Analytics — no personal data, no
  cross-site tracking. Shared catalog-wide token; feeds the hub's Trending / Popular rankings.
- `_headers` sets long cache lifetimes for Cloudflare Pages and sane security headers.

## Deploy

See **[DEPLOY.md](./DEPLOY.md)** for the copy-paste runbook (GitHub + Cloudflare Pages + custom domain). A$0/month on Cloudflare's free tier.

## Provenance

Produced from a multi-turn computational investigation. All figures were computed from the Takahashi EVA transliteration of MS 408, with eight control corpora and a re-implementation of the Naibbe cipher used as ground truth. This is a research record, not a peer-reviewed claim — nothing here decodes the manuscript; the contribution is a narrowing of the space and a precise naming of the one residual doubt.
