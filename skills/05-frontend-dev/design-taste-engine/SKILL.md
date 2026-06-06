---
name: design-taste-engine
description: Anti-slop frontend skill. Eliminates generic AI design — purple gradients, centered heroes, Inter font, three-card rows. Your agent learns real design taste: brief inference, three-dial variance control, typographic discipline, premium color calibration, and GSAP motion.
allowed-tools: "Read, Write, Edit, Bash, Grep"
version: 1.0.0
license: proprietary
author: "daijinou"
compatible-with:
  - claude-code
  - cursor
  - pi
  - codex
tags:
  - frontend
  - design
  - taste
  - css
  - tailwind
  - gsap
  - animation
  - premium
  - ui
source: https://github.com/daijinou/design-taste-skill
---

# tasteskill: Anti-Slop Frontend Skill

> Landing pages, portfolios, and redesigns. Not dashboards, not data tables, not multi-step product UI.
> Every rule below is **contextual**. None of it fires automatically. First read the brief, then pull only what fits.

---

## 0. BRIEF INFERENCE (Read the Room Before Anything Else)

Before touching code or tweaking dials, **infer what the user actually wants**. Most LLM design output is bad because the model jumps to a default aesthetic instead of reading the room.

### 0.A Read these signals first
1. **Page kind** — landing (SaaS / consumer / agency / event), portfolio (dev / designer / creative studio), redesign (preserve vs overhaul), editorial / blog.
2. **Vibe words** the user used — "minimalist", "calm", "Linear-style", "Awwwards", "brutalist", "premium consumer", "Apple-y", "playful", "serious B2B", "editorial", "agency-y", "glassy", "dark tech".
3. **Reference signals** — URLs they linked, screenshots they pasted, products they named, brands they're competing with.
4. **Audience** — B2B procurement panel vs. design-conscious consumer vs. recruiter scanning a portfolio. The audience picks the aesthetic, not your taste.
5. **Brand assets that already exist** — logo, color, type, photography. For redesigns, these are starting material, not optional input (see Section 11).
6. **Quiet constraints** — accessibility-first audiences, public-sector, regulated industries, trust-first commerce, kids' products. These constraints OVERRIDE aesthetic preference.

### 0.B Output a one-line "Design Read" before generating
Before any code, state in one line: **"Reading this as: \<page kind> for \<audience>, with a \<vibe> language, leaning toward \<design system or aesthetic family>."**

Example reads:
- *"Reading this as: B2B SaaS landing for technical buyers, with a Linear-style minimalist language, leaning toward Tailwind utilities + Geist + restrained motion."*
- *"Reading this as: solo designer portfolio for hiring managers, with an editorial / kinetic-type language, leaning toward native CSS + scroll-driven animation + custom typography."*
- *"Reading this as: redesign of a public-sector service site, with a trust-first language, leaning toward GOV.UK Frontend or USWDS."*

### 0.C If the brief is ambiguous, ask one question, do not guess
Ask exactly **one** clarifying question — never a multi-question dump — and only when the design read genuinely diverges. Example: *"Should this feel closer to Linear-clean or Awwwards-experimental?"*

If you can confidently infer from context, **do not ask**. Just declare the design read and proceed.

### 0.D Anti-Default Discipline
Do not default to: AI-purple gradients, centered hero over dark mesh, three equal feature cards, generic glassmorphism on everything, infinite-loop micro-animations everywhere, Inter + slate-900. These are the LLM defaults. Reach past them deliberately based on the design read.

---

## 1. THE THREE DIALS (Core Configuration)

After the design read, set three dials. Every layout, motion, and density decision below is gated by these.

* **`DESIGN_VARIANCE: 8`** — 1 = Perfect Symmetry, 10 = Artsy Chaos
* **`MOTION_INTENSITY: 6`** — 1 = Static, 10 = Cinematic / Physics
* **`VISUAL_DENSITY: 4`** — 1 = Art Gallery / Airy, 10 = Cockpit / Packed Data

**Baseline:** `8 / 6 / 4`. Use these unless the design read overrides them. Do not ask the user to edit this file — overrides happen conversationally.

### 1.A Dial Inference (design read → dial values)
| Signal | VARIANCE | MOTION | DENSITY |
|---|---|---|---|
| "minimalist / clean / calm / editorial / Linear-style" | 5-6 | 3-4 | 2-3 |
| "premium consumer / Apple-y / luxury / brand" | 7-8 | 5-7 | 3-4 |
| "playful / wild / Dribbble / Awwwards / experimental / agency" | 9-10 | 8-10 | 3-4 |
| "landing page / portfolio / marketing site (default)" | 7-9 | 6-8 | 3-5 |
| "trust-first / public-sector / regulated / accessibility-critical" | 3-4 | 2-3 | 4-5 |
| "redesign — preserve" | match existing | +1 | match existing |
| "redesign — overhaul" | +2 | +2 | match existing |

### 1.B Use-Case Presets
| Use case | VARIANCE | MOTION | DENSITY |
|---|---|---|---|
| Landing (SaaS, mainstream) | 7 | 6 | 4 |
| Landing (Agency / creative) | 9 | 8 | 3 |
| Landing (Premium consumer) | 7 | 6 | 3 |
| Portfolio (Designer / studio) | 8 | 7 | 3 |
| Portfolio (Developer) | 6 | 5 | 4 |
| Editorial / Blog | 6 | 4 | 3 |
| Public-sector service | 3 | 2 | 5 |
| Redesign — preserve | match | match+1 | match |
| Redesign — overhaul | +2 | +2 | match |

### 1.C How the Dials Drive Output
Use these (or user-overridden values) as global variables. Cross-references throughout this document refer to these exact variable names — never invent aliases like `LAYOUT_VARIANCE` or `ANIM_LEVEL`.

---

## 2. BRIEF → DESIGN SYSTEM MAP

Once you have the design read (Section 0) and dials (Section 1), pick the right foundation. Do not invent CSS for things that have an official package. Do not pretend an aesthetic trend is an official system.

### 2.A When to reach for a real design system (use official packages)
| Brief reads as… | Reach for | Why |
|---|---|---|
| Microsoft / enterprise SaaS / dashboards | `@fluentui/react-components` or `@fluentui/web-components` | Official Fluent UI, Microsoft tokens, accessibility done |
| Google-ish UI, Material-flavored product | `@material/web` + Material 3 tokens | Official, theme-able via Material Theming |
| IBM-style B2B / enterprise analytics | `@carbon/react` + `@carbon/styles` | Official Carbon, mature data-density patterns |
| Shopify app surfaces | `polaris.js` web components / Polaris React | Required for Shopify admin UI |
| Atlassian / Jira-style product | `@atlaskit/*` + `@atlaskit/tokens` | Official Atlassian DS |
| GitHub-style devtool / community page | `@primer/css` or `@primer/react-brand` | Official Primer; Brand variant for marketing |
| Public-sector UK service | `govuk-frontend` | Legally / regulatorily expected |
| US public-sector / trust-first | `uswds` | Same |
| Fast local-business / agency MVP | Bootstrap 5.3 | Boring, fast, works |
| Modern accessible React foundation | `@radix-ui/themes` | Primitives + polished theme |
| Modern SaaS where you own the components | shadcn/ui (`npx shadcn@latest add ...`) | You own the code, easy to customise; never ship default state |
| Tailwind-based modern SaaS / AI marketing | Tailwind v4 utilities + `dark:` variant | Default for indie + small team builds |

**Honesty rule:** if the brief reads as one of the systems above, install and use the **official** package. Do not recreate its CSS by hand. Do not import a system's tokens but then override 90% of them.

**One system per project.** Do not mix Fluent React with Carbon in the same tree. Do not import shadcn/ui components into a Material 3 app.

### 2.B When the brief is an aesthetic, not a system
For these directions, there is **no single official package**. Build with native CSS + Tailwind + a maintained component library. Be honest in code comments about what is borrowed inspiration vs. official material.

| Aesthetic | Honest implementation |
|---|---|
| Glassmorphism / "frosted glass" | `backdrop-filter`, layered borders, highlight overlays. Provide solid-fill fallback for `prefers-reduced-transparency`. |
| Bento (Apple-style tile grids) | CSS Grid with mixed cell sizes. No single library owns this. |
| Brutalism | Native CSS, monospace, raw borders. No library. |
| Editorial / magazine | Serif type, asymmetric grid, generous whitespace. No library. |
| Dark tech / hacker | Mono + accent neon, terminal motifs. No library. |
| Aurora / mesh gradients | SVG or layered radial gradients. No library. |
| Kinetic typography | Native CSS animations, scroll-driven animations, GSAP for hijacks. No library. |
| **Apple Liquid Glass** | Apple documents this for Apple platforms only. **There is no official `liquid-glass.css`.** Web implementations are approximations using `backdrop-filter` + layered borders + highlights. Label clearly as approximation. |

---

## 3. DEFAULT ARCHITECTURE & CONVENTIONS

Unless the design read picks a real design system (Section 2.A), these are the defaults:

### 3.A Stack
* **Framework:** React or Next.js. Default to Server Components (RSC).
  * **RSC SAFETY:** Global state works ONLY in Client Components. In Next.js, wrap providers in a `"use client"` component.
  * **INTERACTIVITY ISOLATION:** Any component using Motion, scroll listeners, or pointer physics MUST be an isolated leaf with `'use client'` at the top. Server Components render static layouts only.
* **Styling:** **Tailwind v4** (default). Tailwind v3 only if the existing project demands it.
  * For v4: do NOT use `tailwindcss` plugin in `postcss.config.js`. Use `@tailwindcss/postcss` or the Vite plugin.
* **Animation:** **Motion** (the library formerly known as Framer Motion). Import from `motion/react` (`import { motion } from "motion/react"`). The `framer-motion` package still works as a legacy alias — prefer `motion/react` in new code.
* **Fonts:** Always use `next/font` (Next.js) or self-host with `@font-face` + `font-display: swap`. Never link Google Fonts via `<link>` in production.

### 3.B State
* Local `useState` / `useReducer` for isolated UI.
* Global state ONLY for deep prop-drilling avoidance — Zustand, Jotai, or React context.
* **NEVER** use `useState` to track continuous values driven by user input (mouse position, scroll progress, pointer physics, magnetic hover). Use Motion's `useMotionValue` / `useTransform` / `useScroll`. `useState` re-renders the React tree on every change and collapses on mobile.

### 3.C Icons
* **Allowed libraries (priority order):** `@phosphor-icons/react`, `hugeicons-react`, `@radix-ui/react-icons`, `@tabler/icons-react`.
* **Discouraged:** `lucide-react`. Acceptable only when the user explicitly asks for it or the project already depends on it.
* **NEVER hand-roll SVG icons.** If a glyph is missing, install a second library or compose from primitives — do not draw icon paths from scratch.
* **One family per project.** Do not mix Phosphor with Lucide in the same component tree.
* **Standardize `strokeWidth` globally** (e.g. `1.5` or `2.0`).

### 3.D Emoji Policy
Discouraged by default in code, markup, and visible text. Replace symbols with icon-library glyphs. **Override:** allow emojis only when the user explicitly asks for a playful / chat-style / social-native vibe — and even then use them sparingly with intent.

### 3.E Responsiveness & Layout Mechanics
* Standardize breakpoints (`sm 640`, `md 768`, `lg 1024`, `xl 1280`, `2xl 1536`).
* Contain page layouts using `max-w-[1400px] mx-auto` or `max-w-7xl`.
* **Viewport Stability:** NEVER use `h-screen` for full-height Hero sections. ALWAYS use `min-h-[100dvh]` to prevent layout jumping on mobile (iOS Safari address bar).
* **Grid over Flex-Math:** NEVER use complex flexbox percentage math (`w-[calc(33%-1rem)]`). ALWAYS use CSS Grid (`grid grid-cols-1 md:grid-cols-3 gap-6`).

### 3.F Dependency Verification (mandatory)
Before importing ANY 3rd-party library, check `package.json`. If the package is missing, output the install command first. **Never** assume a library exists.

---

## 4. DESIGN ENGINEERING DIRECTIVES (Bias Correction)

LLMs default to clichés. Override these defaults proactively. Each rule has a context-aware override path.

### 4.1 Typography
* **Display / Headlines:** Default `text-4xl md:text-6xl tracking-tighter leading-none`.
* **Body / Paragraphs:** Default `text-base text-gray-600 leading-relaxed max-w-[65ch]`.
* **Sans font choice:**
  * **Discouraged as default:** `Inter`. Pick `Geist`, `Outfit`, `Cabinet Grotesk`, `Satoshi`, or a brand-appropriate serif first.
  * **Override:** Inter is acceptable when the user explicitly asks for a neutral / standard / Linear-style feel, or when the brief is a public-sector / accessibility-first site.
* **Pairings to know:** `Geist` + `Geist Mono`, `Satoshi` + `JetBrains Mono`, `Cabinet Grotesk` + `Inter Tight`, `GT America` + `IBM Plex Mono`.

* **SERIF DISCIPLINE (VERY DISCOURAGED AS DEFAULT):**
  * Serif is **very discouraged as the default font for any project.** "It feels creative / premium / editorial" is NOT a reason to reach for serif.
  * **Serif is only acceptable when ONE of these is explicitly true:**
    - The brand brief literally names a serif font, OR
    - The aesthetic family is genuinely editorial / luxury / publication / manuscript / heritage / vintage AND you can articulate why this specific serif fits this specific brand
  * For everything else (creative agency, design studio, modern brand, premium consumer, portfolio, lifestyle), **default sans-serif display**.
  * **Specifically BANNED as defaults:** `Fraunces` and `Instrument_Serif` (the two LLM-favorite display serifs).
  * **If a serif is justified** (rare, per the above), rotate from this pool, do NOT reuse the same serif across consecutive projects: PP Editorial New, GT Sectra Display, Cardinal Grotesque, Reckless Neue, Tiempos Headline, Recoleta, Cormorant Garamond, Playfair Display, EB Garamond, IvyPresto, Migra, Editorial Old, Saol Display, Söhne Breit Kursiv, Domaine Display, Canela, Schnyder, Tobias, NB Architekt, ITC Galliard.

* **ITALIC DESCENDER CLEARANCE (mandatory):** When italic is used in display type and the word contains a descender letter (`y g j p q`), `leading-[1]` or `leading-none` will clip the descender. Use `leading-[1.1]` minimum and add `pb-1` or `mb-1` reserve on the wrapping element.

### 4.2 Color Calibration
* Max 1 accent color. Saturation < 80% by default.
* **THE LILA RULE:** The "AI Purple / Blue glow" aesthetic is discouraged as a default. No automatic purple button glows, no random neon gradients. Use neutral bases (Zinc / Slate / Stone) with high-contrast singular accents (Emerald, Electric Blue, Deep Rose, Burnt Orange, etc.).
* **One palette per project.** Do not fluctuate between warm and cool grays within the same project.
* **PREMIUM-CONSUMER PALETTE BAN (mandatory, second-most-recurring AI-tell):**
  * Banned default hex families: `#f5f1ea` / `#f7f5f1` / `#fbf8f1` / `#efeae0` / `#ece6db` / `#faf7f1` / `#e8dfcb` (warm beige backgrounds) and `#b08947` / `#b6553a` / `#9a2436` / `#9c6e2a` / `#bc7c3a` / `#7d5621` (brass/clay/oxblood accents).
  * **Default alternatives:** Cold Luxury, Forest, Black-and-Tan, Cobalt+Cream, Terracotta+Slate, Olive+Brick+Paper, Pure Monochrome.

### 4.3 Layout Diversification
* **ANTI-CENTER BIAS:** Centered Hero / H1 sections are avoided when `DESIGN_VARIANCE > 4`. Force "Split Screen" (50/50), "Left-aligned content / right-aligned asset", "Asymmetric white-space", or scroll-pinned structures.

### 4.4 Materiality, Shadows, Cards
* Use cards ONLY when elevation communicates real hierarchy. Otherwise group with `border-t`, `divide-y`, or negative space.
* When a shadow is used, tint it to the background hue. No pure-black drop shadows on light backgrounds.
* **SHAPE CONSISTENCY LOCK (mandatory):** Pick ONE corner-radius scale for the page and stick to it.

### 4.5 Interactive UI States
* **Loading:** Skeletal loaders matching the final layout's shape. Avoid generic circular spinners.
* **Empty States:** Beautifully composed; indicate how to populate.
* **Error States:** Clear, inline (forms), or contextual (toasts only for transient).
* **Tactile Feedback:** On `:active`, use `-translate-y-[1px]` or `scale-[0.98]`.
* **BUTTON CONTRAST CHECK (mandatory, a11y):** WCAG AA min (4.5:1 for body, 3:1 for large text 18px+).
* **CTA BUTTON WRAP BAN (mandatory):** Button text MUST fit on one line at desktop.
* **NO DUPLICATE CTA INTENT (mandatory):** Pick ONE label per intent and use it everywhere on the page.

### 4.6 Data & Form Patterns
* Label ABOVE input. Error text BELOW input. Standard `gap-2` for input blocks.
* No placeholder-as-label. Ever.

### 4.7 Layout Discipline (Hard Rules)

* **Hero MUST fit in the initial viewport.** Headline max 2 lines on desktop, subtext max **20 words** AND max 3-4 lines, CTAs visible without scroll.
* **Hero font-scale discipline.** Default sensible range: `text-4xl md:text-5xl lg:text-6xl` for most heroes; `text-6xl md:text-7xl` only when the headline is 3-5 words.
* **HERO TOP PADDING CAP (mandatory):** Max `pt-24` (≈6rem) at desktop.
* **HERO STACK DISCIPLINE (max 4 text elements).** Allowed: Eyebrow OR brand strip (pick zero or one), Headline (max 2 lines), Subtext (max 20 words), CTAs (1 primary + max 1 secondary).
* **"Used by" / "Trusted by" logo wall belongs UNDER the hero, never inside it.**
* **Navigation MUST render on a single line on desktop.** Height max 80px, default 64-72px.
* **Bento grids MUST have rhythm, not one-sided repetition.** Vary the composition.
* **BENTO CELL COUNT RULE (mandatory):** EXACTLY as many cells as you have content for.

---

## 5. MOTION CHOREOGRAPHY

### 5.A GSAP ScrollTrigger
| Brief reads as… | Recommended preset |
|---|---|
| Portfolio, editorial, long-scroll narrative | **Pinned sections** — pin a section title while gallery scrolls beside/through it |
| B2B SaaS, feature-heavy landing | **Tiled reveals** — each bento cell fades+scales in on scroll |
| Premium consumer, product launch | **Scrubbed opacity** — images start dark/small, scrub to full opacity/scale |
| Agency, creative studio | **Horizontal scroll** — pinned horizontal gallery with snap points |
| Devtool, technical | **Minimal, purposeful** — subtle slide-up on key nodes, no decorative fluff |

### 5.B Hover Physics
Every interactive element (cards, buttons, images) MUST have a reactive state:
- **Cards + Images:** `transition-all duration-700 ease-[cubic-bezier(0.32,0.72,0,1)]` with `group-hover:scale-[1.02]` inside overflow-hidden containers.
- **Magnetic Buttons:** On hover, the nested icon circle translates diagonally — `group-hover:translate-x-1 group-hover:-translate-y-[1px]` and scales slightly.

### 5.C Entry Animation
Elements should not appear statically on load. Use IntersectionObserver or Motion's `whileInView`:
- **Default:** `translate-y-16 opacity-0` → `translate-y-0 opacity-100` over 800ms with `ease-[cubic-bezier(0.32,0.72,0,1)]`.
- **Staggered lists:** `staggerChildren: 0.08` per item.

### 5.D Reduced Motion
Always respect `prefers-reduced-motion`. Provide a static fallback for all animations.

---

## 6. RESPONSIVE & MOBILE

* **Mobile Override (Universal):** Any asymmetric layout above `md:` MUST aggressively fall back to `w-full`, `px-4`, `py-8` on viewports below 768px.
* **Never use `h-screen` for full-height sections** — always `min-h-[100dvh]`.
* **Overlap Ban on Mobile:** Remove all rotations (`rotate-2`, `-rotate-2`) and negative-margin overlaps below 768px. They cause touch-target conflicts.
* **Bento Grid Collapse:** Reset all `col-span-N` / `row-span-N` to `col-span-1` on mobile.

---

## 7. MOBILE-SPECIFIC RULES (Desktop rules do not apply verbatim)

### 7.A Touch Target Sizing (minimum 44×44px)
* All interactive elements (buttons, links, icon taps, filter chips) must have a minimum touch target of 44×44 CSS pixels, per Apple HIG and Material Design guidelines.
* Adjacent touch targets must have minimum 8px gap between their bounding boxes.
* **Icon-only buttons** (hamburger menus, close buttons, search icons) must include invisible padding to meet 44×44px even if the visible icon is smaller.

### 7.B Bottom Navigation Bar (mobile-navigation)
* Default to bottom tab bar for primary navigation on mobile (thumb-reachable), not top nav.
* Bottom bar height: 56-64px (tab icons + labels).
* Bottom bar must include safe area inset padding for notched phones.

---

## 8. ACCESSIBILITY (A11Y)

* All interactive elements must have visible focus indicators.
* Skip-to-content link must be the first focusable element on the page.
* All images must have `alt` text (empty `alt=""` for decorative images).
* Color contrast must meet WCAG AA (4.5:1 body, 3:1 large text).
* Motion must respect `prefers-reduced-motion`.
* Forms must have proper `label` associations, error states, and ARIA attributes.
* Heading hierarchy must be semantic (`h1` → `h2` → `h3`, no skipping).

---

## 9. PRE-FLIGHT CHECKLIST (Before Shipping)

Before calling a page complete, verify:

- [ ] Design Read declared (Section 0.B)
- [ ] Three Dials set (Section 1)
- [ ] Design system or aesthetic declared (Section 2)
- [ ] Font ≠ Inter (unless explicitly justified)
- [ ] No AI-purple gradients (unless brand demands it)
- [ ] No warm-beige+brass premium-consumer default (Section 4.2)
- [ ] Hero fits viewport, headline ≤ 2 lines, subtext ≤ 20 words
- [ ] CTA contrast passes WCAG AA
- [ ] CTA text fits one line
- [ ] Navigation single-line on desktop
- [ ] Bento grid has no empty cells
- [ ] Mobile layout collapses correctly
- [ ] Touch targets ≥ 44×44px on mobile
- [ ] `prefers-reduced-motion` respected
- [ ] Form labels above inputs (not placeholders)
- [ ] One CTA intent per page (no duplicate labels)

---

## 10. REDESIGN RULES

### 10.A Preserve Mode
* **Preserve the spirit of the original.** If the original site has a distinct visual identity, keep its core.
* Keep the exact colors, spacing, typography, and tone. Refresh only interaction quality, motion, and responsive behavior.

### 10.B Overhaul Mode
* The original is a starting point, not a constraint. Keep the brand name, logo, and core value prop — everything else is up for change.
* Do a full re-read of brief (Section 0). Treat it as a new project.
* Three Dials can be adjusted. Layout can be restructured. Motion can be upgraded.

---

## 11. BRAND ASSET INTEGRATION

When the user provides existing brand assets (logo, colors, typeface, photography):
1. Use exact brand colors, not approximations.
2. Use the brand's typeface if provided. If not available and cannot be loaded, pick the closest match from the font pool.
3. If brand photography exists, use it. If not, use high-quality stock imagery consistent with the brand tone.
4. Never override brand guidelines with generic aesthetic preferences.
