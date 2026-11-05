# Trevor Adair Photography — Website

A brand-new, from-scratch website for **Trevor Adair Photography** (a DBA of Adair Media LLC), built to be hosted on GitHub Pages. Editorial, light, and airy — a premium wedding/portrait feel that is its own design, not a copy of any reference site. Design *principles* were synthesized from sites Trevor likes (image-first heroes, bold typographic statements, alternating editorial sections, minimal text, contact visible immediately); no images, text, or layouts were copied from them.

**Status: pre-launch draft.** 42 of 57 image slots now use Trevor's real photos (November 4, 2026 batch); the remaining 15 slots are clearly labeled placeholders, and every unknown fact is a marked TODO (see the launch checklist below). Nothing on the site pretends to be finished work. Updated 2026-11-04: approved pricing, public contact details, planned domain, business social links, and one marked placeholder testimonial applied.

---

## Design system

### Color — all oklch, one warm family

Every color is a CSS custom property in `assets/css/style.css`, written in `oklch()`. The system has one rule: **shared warm hue, systematic lightness steps, one accent.**

- Neutrals all sit in the same warm hue family (~60–85): lightness steps run from near-white surfaces down to near-black text, with chroma kept very low (0.008–0.025) so surfaces, borders, and text read as one family.
- The single accent is a warm bronze/terracotta at hue 45 — adjacent to the neutrals, not a competing color. It is used sparingly: buttons, links, eyebrows, and rules.
- As elements darken, chroma rises slightly (0.02 → 0.11) so dark elements keep their warmth instead of going gray.

| Token | oklch | Used for |
|---|---|---|
| `--color-bg` | `oklch(0.985 0.008 85)` | Page background |
| `--color-surface` | `oklch(0.97 0.012 80)` | Cards, form fields |
| `--color-surface-warm` | `oklch(0.94 0.02 75)` | Warm section bands |
| `--color-accent-soft` | `oklch(0.95 0.025 60)` | CTA bands, form notes |
| `--color-border` | `oklch(0.88 0.015 80)` | Hairline borders |
| `--color-border-strong` | `oklch(0.78 0.02 75)` | Inputs, emphasis rules |
| `--color-heading` | `oklch(0.24 0.025 60)` | Headings |
| `--color-text` | `oklch(0.30 0.02 70)` | Body text |
| `--color-muted` | `oklch(0.52 0.02 70)` | Captions, secondary text |
| `--color-accent` | `oklch(0.50 0.11 45)` | Buttons, active states |
| `--color-accent-dark` | `oklch(0.42 0.10 45)` | Links, eyebrows, hover |
| `--color-on-accent` | `oklch(0.985 0.008 85)` | Text on accent buttons |
| `--color-dark` | `oklch(0.25 0.02 60)` | Footer band |
| `--color-dark-text` | `oklch(0.96 0.01 80)` | Footer text |
| `--color-dark-muted` | `oklch(0.76 0.012 80)` | Footer secondary text |

**Contrast (computed from the oklch values, WCAG 2.x ratios):** body text on background 13.1:1 · headings 15.8:1 · muted text 5.3:1 (4.6:1 on warm section bands — the tightest pair, still passing) · white-on-accent buttons 6.0:1 · accent-dark links 8.4:1 · footer text 14.3:1, footer muted 7.5:1. Every text/background pair passes WCAG AA for normal text (≥ 4.5:1). Note: `oklch()` needs a modern browser (2023+); that is an acceptable trade for a new site.

### Typography

- **Display:** Fraunces (serif, optical sizing) for headings — editorial, premium, wedding-appropriate.
- **Body:** Inter (sans) for everything else — clean and highly legible.
- Both load from Google Fonts with `display=swap` so text never blocks on font loading.
- **Fluid type scale** (`clamp()` — grows with viewport, no breakpoint jumps):
  - Display/hero: `clamp(2.75rem, 7vw, 5rem)`
  - H1: `clamp(2.5rem, 6vw, 4.25rem)`
  - H2: `clamp(1.875rem, 4vw, 2.75rem)`
  - H3: `clamp(1.375rem, 2.5vw, 1.75rem)`
  - Lead: `clamp(1.125rem, 1.5vw, 1.375rem)`
  - Body: `1.0625rem` at `1.7` line-height; body prose capped at `70ch` (target line length 65–75 characters).
- One `<h1>` per page. Eyebrow labels (small caps, letter-spaced) introduce every section.

### Layout system

- **Mobile-first, single stylesheet** (`assets/css/style.css`), one tiny vanilla script (`assets/js/main.js`: mobile nav toggle + footer year). No frameworks, no build step, no tracking.
- **Container:** `min(1200px, 92vw)`, generous section padding (`clamp(3.5rem, 8vw, 6.5rem)`).
- **Hero:** full-bleed image slot (16:9) with an overlapping cream panel holding the headline and CTAs — text always sits on a solid panel, never over a busy photo.
- **Editorial splits:** alternating image/text two-column sections (image flips sides on alternate sections); single column on mobile.
- **Galleries:** grids with fixed aspect ratios per slot (`3:2` or `4:5`), location-keyword captions, `loading="lazy"` and explicit `width`/`height` on every image to prevent layout shift.
- **Sticky minimal nav** with a mobile menu; **skip link** and visible focus states for accessibility.
- **Cards** for services and journal posts; **native `<details>` FAQs** (no JS needed); **CTA band** closing every page.

---

## File map

This folder **is** the repository root (the file that deploys as the homepage is `index.html` here, not in a subfolder).

```
index.html                  Home
weddings/index.html         Wedding photography
portraits/index.html        Portrait photography
families/index.html         Family photography
proposals/index.html        Proposals & engagements
graduation/index.html   graduation photography
corporate-events/index.html Corporate & event photography
about/index.html            About Trevor
contact/index.html          Contact form + Instagram links
journal/index.html          Blog index shell (no posts yet)
assets/css/style.css        The entire design system (one file)
assets/js/main.js           Nav toggle + footer year (vanilla JS)
assets/favicon.svg          "TA" monogram mark
assets/placeholders/*.svg   Labeled placeholder images (see PHOTOS.md)
sitemap.xml                 All 10 pages (planned domain trevoradairphotography.com — see below)
robots.txt                  Allows all, points at the sitemap
.nojekyll                   Tells GitHub Pages not to run Jekyll
README.md                   This file
PHOTOS.md                   Every image slot + what to shoot for it
```

**URL structure:** one folder per page (`/weddings/`, `/portraits/`, …) so every service gets a clean, crawlable URL. Internal links are relative (not root-absolute) so the site works on both a custom domain and a `username.github.io/repo/` project URL.

**Where swappable things live** (static HTML has no build step, so these are disciplined search-and-replace targets, all marked with `TODO` comments in code):

- **Pricing (approved 2026-11-04):** weddings from $1,925; portraits from $280; families Mini $230 / Full $340 / Extended $360–$620; proposals from $280; graduation from $280; corporate events quote-based with headshots $180–$280. Each service page's `.investment` block holds its figure. Wedding $1,925 = top-10 typical $2,400 minus 20%.
- **Contact form endpoint:** one place — the `action` in `contact/index.html` (currently `https://formspree.io/f/YOUR_FORM_ID`).
- **Domain:** planned domain `trevoradairphotography.com` (not yet purchased; DNS not pointed) now appears in every page's `<link rel="canonical">` and JSON-LD, plus `sitemap.xml` and `robots.txt`. Acquire the domain, point DNS, and add a `CNAME` file at launch.
- **Public email/phone:** trevoradair2@gmail.com and 801-837-9308, published on `contact/index.html` and in Photographer JSON-LD on home, about, and contact.
- **Testimonials:** `.kind-words` sections on home and about hold one placeholder testimonial (Xandra Black — “Quite literally the perfect photographer for us”), explicitly marked as a placeholder. Replace with a real permitted testimonial before launch.
- **Social links:** Instagram https://www.instagram.com/trevoradair.portraits/ and Facebook https://www.facebook.com/trevoradair.portraits/, featured on the contact page and in footers; Photographer JSON-LD `sameAs` is exactly these two URLs. Note: the Facebook URL uses the handle the user supplied, and the user confirmed the page (Trevor Adair Portraits, Provo) via screenshot on 2026-11-04.
- **Personal bio:** `about/index.html` has a marked TODO for Trevor's own bio text.
- **Header/footer nav:** repeated in every page (no templating in plain HTML). If a link changes, update it in all 10 pages — or add a build step later.
- **Photos:** 42 of 57 slots filled with real photos (Nov 4 batch); see PHOTOS.md for the per-slot manifest.

---

## Swapping placeholders for real photos

1. Shoot or select photos per the slot list in **PHOTOS.md** (page, slot, recommended content, aspect ratio, dimensions).
2. Export web-ready files (JPEG, sRGB, max ~1600px wide for heroes, ~1200px for galleries, compressed — aim under ~200KB each) into a new `assets/photos/` folder. Do **not** overwrite the placeholder SVGs until every slot is replaced.
3. In the page HTML, change the `<img src="…">` from `assets/placeholders/….svg` to `assets/photos/….jpg`, update the `alt` text to describe the real photo (drop the "Placeholder:" prefix), and update `width`/`height` to the real image's dimensions.
4. Keep the same aspect ratio the slot was designed for (or update the CSS ratio class on that image) so the layout doesn't shift.
5. Delete a placeholder SVG only after no page references it anymore.

---

## SEO foundation (built in, not bolted on)

- Unique `<title>` + meta description per page, using Provo / Utah keywords naturally — no stuffing.
- Semantic HTML5 (`header`, `main`, `section`, `footer`, `figure`/`figcaption`), one H1 per page, descriptive internal links between related pages (every service page links to the others, to contact, and to relevant siblings like weddings ↔ proposals).
- JSON-LD on every page: `Photographer` LocalBusiness on home / about / contact; `FAQPage` on all six service pages (answers match the visible FAQ text exactly); `BreadcrumbList` everywhere.
- `sitemap.xml` + `robots.txt` (planned domain trevoradairphotography.com, not yet purchased — see checklist).
- Performance by construction: no libraries, one small CSS file, one tiny JS file, system-friendly font loading (`display=swap`), lazy-loaded below-fold images, explicit image dimensions.

**What this does not do (honestly):** no amount of on-page SEO guarantees page 1 — that also needs real photos, real testimonials, a Google Business Profile, local citations, and published journal posts over time. This site lays the correct foundation for all of that.

---

## Launch-blocker checklist

Do not launch publicly until every item is resolved or consciously deferred:

- [ ] **Real domain** — planned domain `trevoradairphotography.com` is not yet purchased; acquire it, point DNS, and add a `CNAME` file at launch.
- [ ] **Real photos (partially done)** — 42 of 57 slots now use real photos (Nov 4 batch; see PHOTOS.md). Still placeholders: all 8 wedding slots, both about slots, all 3 journal slots, home-service-weddings, home-about. Never launch with placeholders presented as work.
- [ ] **Formspree endpoint** — create the form, set the real endpoint in `contact/index.html`, and test a submission end-to-end.
- [x] **Public contact details** — trevoradair2@gmail.com and 801-837-9308 published on the contact page and in JSON-LD.
- [ ] **Personal bio** — write Trevor's bio for the about page.
- [ ] **Testimonials** — replace the Xandra Black placeholder in the home/about `.kind-words` sections with real client words (with permission).
- [ ] **Pre-launch QA** — click every nav/footer link, submit the form, check mobile + desktop, and re-run the validation checks below.

Optional (launch-safe to defer): first journal posts (the journal shell is honest as-is), a custom domain, Google Search Console + Analytics.

**Validation already run on this draft (re-run after the 2026-11-04 updates):** every internal link resolves to an existing file; every page has exactly one H1, a title, and a meta description; every image has non-empty alt text; no lorem ipsum filler anywhere; no invented experience, awards, or counts. Prices, contact details, and the single testimonial are the user-approved items listed above. Re-run these checks after any edit (a link checker + a quick grep for `lorem` and for `TODO` will do).

---

## Deploy to GitHub Pages

1. Create a new GitHub repository (e.g. `trevoradair-photography`).
2. Push the **contents** of this folder (not the folder itself) to the repository's default branch, so `index.html` sits at the repo root.
3. In the repository: **Settings → Pages → Build and deployment → Source: Deploy from a branch**, select the default branch and `/ (root)`.
4. `.nojekyll` is already included, so Pages serves the files as-is (including folders that start with an underscore, if any are added later).
5. Your site will be live at `https://<username>.github.io/<repo>/` (or at your user site if the repo is named `<username>.github.io`).
6. **Optional custom domain:** add a `CNAME` file containing just the domain (e.g. `www.trevoradairphotography.com`), point the domain's DNS at GitHub Pages (A records / CNAME per GitHub's docs), enable "Enforce HTTPS" in Pages settings, then confirm the planned domain `trevoradairphotography.com` is live and resubmit the sitemap in Google Search Console.

---

## Copy policy

All copy is written from confirmed facts only: Provo-based, serving throughout Utah, travel as far as Farmington for photo work, the six services, the two Instagram accounts, and the Adair Media LLC DBA relationship. Where a fact was unknown, the site says so (form pending connection, testimonial marked as a placeholder) instead of inventing it. No years of experience, awards, press features, or booking counts appear anywhere in this code. The prices, contact details, and single testimonial on the site are the user-approved items listed above.
