# Acadrez — Project Documentation

> Free aggregate calculator for Pakistani university admissions.

---

## Overview

**Acadrez** (formerly Acadify) is a free, browser-based aggregate calculator built for students applying to Pakistani universities. It eliminates the pain of hunting for scattered formulas and doing manual calculations by providing a single, fast, accurate tool.

- **Live URL:** https://acadrez.pages.dev/
- **Type:** Static website (no backend, no database, no login)
- **Target audience:** Pakistani students applying to NUST, FAST, UET, COMSATS, and 15+ other universities

---

## Problem Statement

Students struggle to calculate aggregates because formulas are scattered across university websites, Facebook groups, and WhatsApp chains. Manual calculations are error-prone. Acadrez solves this with one place, one tool, under 60 seconds.

---

## Core Features

- **Manual mode** — User selects 2–5 mark sources, enters total/obtained marks and custom weightages (must sum to 100%), and gets an instant aggregate.
- **By University mode** — User searches for a university, selects a program if applicable, and the weightage formula is pre-filled from verified data. Only marks need to be entered.
- **Fuzzy search** — Levenshtein distance–based search on both the homepage and the Universities page, tolerating typos and partial matches.
- **Program selector** — Universities with multiple admission formulas (e.g., Engineering vs. Non-Engineering) expose a dropdown that updates the formula live.
- **Additional marks field** — `allowAdditional: true` on specific sources adds a bonus marks input (e.g., for tests that allow extra credit).
- **Calculation history** — Last 5 calculations stored in-session with restore (↩) functionality.
- **Undo reset** — Reset button becomes an Undo button after clearing, allowing the user to recover their inputs.
- **Animated result** — Circular SVG progress indicator fills on result, color-coded green/orange/red based on score.
- **Share feature** — Web Share API on mobile, clipboard copy fallback on desktop, with user-agent detection to route correctly.

---

## University Directory (as of last update)

| University | Programs |
|---|---|
| National University of Science and Technology (NUST) | NET Basis, ACT/SAT Basis |
| National University of Computer and Emerging Sciences (FAST) | Computing/Business, Engineering |
| University of Engineering and Technology Lahore (UET Lahore) | Intermediate, Foreign Qualification, Diploma Holders, B.Sc. Engineering Technology, Non-ECAT |
| COMSATS University Islamabad | Engineering/Non-Engineering, B.Design/B.Fine Arts, B.Arch, Bachelor of Interior Design |
| Pakistan Institute of Engineering & Applied Sciences (PIEAS) | SSC/HSSC Basis |
| Ghulam Ishaq Khan Institute (GIKI) | Undergraduate Programs |
| Air University Islamabad | Engineering, Non-Engineering |
| NED University of Engineering and Technology | BS Programs |
| Quaid-i-Azam University (QAU) | LLB, Non-Engineering |
| Mehran University of Engineering and Technology (MUET) | BS Programs |
| Government College University Lahore (GCU Lahore) | BS Programs |
| National University of Technology (NUTECH) | BS Programs |
| University of Management and Technology (UMT) | Engineering, Non-Engineering |
| International Islamic University (IIUI) | BA/LLB (Hons) Shariah & Law, Undergraduate (PQM basis) |
| Abdul Wali Khan University Mardan (AWKUM) | Undergraduate Programs |

All formulas are sourced from official university prospectuses or admission policy pages. Source URLs are linked in the UI.

---

## Aggregate Formula

```
Aggregate = Σ (Obtained / Total) × Weightage
```

For each mark source, the percentage of marks obtained is multiplied by the source's weightage. All values are summed to produce the final aggregate percentage, rounded to 2 decimal places.

**Example:** Matric 950/1100 × 10% = 8.64 | FSc 900/1100 × 40% = 32.73 | Test 160/200 × 50% = 40.00 → Aggregate = **81.37%**

---

## Tech Stack

| Layer | Technology |
|---|---|
| Markup | Vanilla HTML5 |
| Styling | Tailwind CSS (CDN), custom CSS |
| Fonts | Lexend (display), Inter (body) — Google Fonts |
| Icons | Material Symbols Outlined (Google Fonts CDN) |
| Logic | Vanilla JavaScript (ES6+) |
| University data | `Universities.js` — static JS array |
| Calculator logic | `script.js` — embedded in `index.html` and `universities.html` |
| Search algorithm | Levenshtein distance fuzzy matching |
| Hosting | Cloudflare Pages |
| Version control | GitHub (web UI, drag-and-drop uploads) |
| SEO | Google Search Console, `sitemap.xml`, `robots.txt`, JSON-LD structured data |

No build tools, no npm, no bundlers. Pure static files.

---

## File Structure

```
/
├── index.html              # Homepage + Manual/University calculator
├── universities.html       # University directory + calculator modal
├── how-it-works.html       # Step-by-step guide (tabbed: By University / Manual)
├── about.html              # About page
├── 404.html                # Custom error page
├── Universities.js         # University data (formulas, programs, source URLs)
├── sitemap.xml             # XML sitemap for Google Search Console
├── robots.txt              # Crawler rules
└── googlee19e21a243fdb346.html  # Google site verification file
```

---

## Universities.js Data Structure

```javascript
const universities = [
  {
    id: "unique-string-id",
    name: "Full University Name",
    sourceUrl: "https://official-prospectus-or-policy-url",
    programs: [
      {
        label: "Program Name (shown in dropdown)",
        sources: [
          { label: "SSC / Matric", weightage: 10 },
          { label: "HSSC / FSc", weightage: 40 },
          { label: "Entry Test", weightage: 50, allowAdditional: true }
          // allowAdditional: true → shows a bonus marks input field
        ]
      }
    ]
  }
];
```

**Key rules:**
- `programs` is always an array. Single-program universities skip the program dropdown automatically.
- Weightages across all sources in a program **must sum to 100** — broken/zero-weightage entries cause silent calculation errors.
- `allowAdditional: true` is optional and only added where the university formula supports bonus marks.
- `sourceUrl` is optional but strongly recommended for trust signals.

---

## Pages

### index.html — Homepage
- Hero section with tagline, stats strip (15+ universities, 60s, 100% accurate)
- Mode toggle: Manual / By University
- Manual mode: source count selector (2–5), dynamic input cards (name, total, obtained, weightage per source)
- University mode: fuzzy search → dropdown select → optional program selector → formula display sidebar → mark input cards
- Calculate button, Reset/Undo button
- Animated circular result display (color-coded)
- Calculation history (last 5, in-session only, restorable)
- Share button (Web Share API / clipboard fallback)

### universities.html — University Directory
- Grid of all university cards (sorted alphabetically)
- Search bar with fuzzy dropdown
- Click any card → modal panel slides up with formula sidebar + calculator
- Program dropdown inside modal if university has multiple programs
- Same calculation and result display logic as homepage

### how-it-works.html — Guide
- Tabbed layout: By University / Manual
- Step-by-step instructions for each mode
- Formula explanation section
- JSON-LD HowTo structured data for Google rich results

### about.html — About
- What is Acadrez
- Why trust us (formula sourcing, transparency, no data collection, mobile support)
- Limitations notice (formulas can change, not all universities supported, no quota/extra factors)
- The idea section

### 404.html — Error Page
- Custom 404 with floating animation
- Quick links back to homepage, Universities, Calculator, How it Works, About

---

## SEO Setup

- **Google Search Console:** Verified via HTML file (`googlee19e21a243fdb346.html`)
- **Sitemap:** `sitemap.xml` (lowercase filename — case-sensitive on Cloudflare Pages)
- **robots.txt:** Allows all crawlers, disallows `404.html`, references sitemap
- **Canonical URLs:** Set on each page
- **JSON-LD structured data:**
  - `index.html` → `WebApplication` + `FAQPage`
  - `universities.html` → `ItemList`
  - `how-it-works.html` → `HowTo`
  - `about.html` → `Organization`
- **Open Graph + Twitter Card:** Set on all pages for WhatsApp/Facebook/LinkedIn previews
- **Meta description + keywords:** Optimized for Pakistani university admission search queries

---

## Hosting & Deployment

- **Platform:** Cloudflare Pages (connected to GitHub repo)
- **Deployment method:** Drag-and-drop file uploads via GitHub web UI → auto-deploys via Cloudflare Pages
- **Build config:** None required — Cloudflare Pages serves static files directly
- **Domain:** `acadrez.pages.dev` (Cloudflare Pages default domain)

**Why Cloudflare Pages (not alternatives):**
- Netlify free tier was exhausted quickly
- Cloudflare Workers doesn't auto-serve static files cleanly
- Cloudflare Pages handles static files with zero config

---

## Known Gotchas & Key Learnings

- **Sitemap case sensitivity:** `sitemap.xml` must be lowercase. `Sitemap.xml` causes a fetch error in Google Search Console on Cloudflare Pages.
- **Domain consistency:** All HTML files, `robots.txt`, `sitemap.xml`, and JSON-LD blocks must reference the same domain. Migrating domains requires a bulk find-and-replace across all files.
- **Zero-weightage entries:** A source with `weightage: 0` causes silent calculation errors (contributes 0 to aggregate but no error is thrown). Remove such entries from the data.
- **allowAdditional:** Only flag sources where the university officially allows bonus marks. Incorrect flagging adds confusing UI fields.
- **Web Share API:** Only works on mobile browsers (Android/iOS Chrome/Safari). Desktop falls back to clipboard. User-agent detection routes correctly.
- **Result labels:** "High/Low chance of admission" language was removed — cutoff data is unavailable and university-specific, so results use neutral score labels only.

---

## Distribution Channels

Primary reach for the Pakistani student audience:
- **WhatsApp groups** (student groups, FSc/Matric result seasons)
- **Facebook groups** (university admissions, student communities)
- **Reddit**

Admission season (May–August) is the critical traffic window.

---

## Development Principles

- No login, no backend, no database — pure static
- All calculations run client-side in JavaScript
- Iterative, approval-based development — no changes without review
- Surgical edits — only touch files directly relevant to the task
- GitHub web UI only (drag-and-drop) — no terminal/CLI
- Bulk find-and-replace for any domain-wide URL updates

---

## Vision & Roadmap

The immediate product is an aggregate calculator. The broader vision for Acadrez is a wider educational services platform for Pakistani students — the name was chosen to allow expansion beyond just calculators. High-priority next steps:

1. **Expand university directory** — highest-leverage product improvement
2. **Custom domain** — move off `acadrez.pages.dev` to a branded domain
3. **Cutoff data** — if obtainable, show historical merit cutoffs alongside the calculated aggregate
4. **Broader platform expansion** — admissions guidance, test prep resources, and other educational tools

---

*Last updated: July 2026*
