---
title: "Personal Portfolio — UI Analysis &amp; Improvement Roadmap"
site: "SteveWufeng.github.io"
author: "Yiyuan (Steve) Wufeng"
status: draft
analyzed: 2026-06-03
---

# UI Analysis: SteveWufeng.github.io

> Answering: *"Is this too bland? What is the better format?"*

---

## 1. Executive Summary

**Verdict: Yes, the site is bland — but it has good bones.**

The current design is functionally complete and structurally sound. The HTML
semantics are correct, the scroll-spy sidebar works, the IntersectionObserver
animations are smooth, and the timeline layout is readable. A recruiter could
find all the information they need.

**The problem is that the design does not leave an impression.** The content
is strong (diverse experiences, clear narrative, impressive GPA/timeline), but
the visual presentation undersells it. The site looks like a vanilla HTML
template from 2020 — it doesn't reflect the sophistication of someone who
architects full-stack e-commerce platforms and trains computer vision models.

---

## 2. Six-Dimension Quality Audit

### 2.1 Visual Hierarchy — FAIL

| Issue | Severity | Detail |
|-------|----------|--------|
| No visual distinction between section content types | **High** | Work, Projects, Education, Community all use the exact same `.timeline` layout. The user's eye gets no break in rhythm — it's wall-to-wall left-aligned text. |
| Hero section lacks visual weight | **High** | Profile pic + one-liner + bio + links. No background treatment, no gradient, no visual hook. The hero is the most important real estate — it should feel like a landing. |
| Section titles are centered but content is left-aligned | **Medium** | Creates a visual disconnect. Titles float disconnected from their content blocks. |
| Skills grid is raw text | **Medium** | 7 categories, each as bold-label + comma-list. No visual hierarchy within — all skills look equally weighted. |

### 2.2 Typography & Readability — FAIL

| Issue | Severity | Detail |
|-------|----------|--------|
| **Poppins font is NOT loaded** | **Critical** | `font-family: 'Poppins', sans-serif` is declared in CSS, but there is no `@import`, `<link>`, or `@font-face` loading Poppins anywhere. The site renders entirely in the system fallback (Arial/Helvetica). |
| No font-size scale defined | **Medium** | Only `.section-title` has an explicit `font-size: 1.8rem`. Body text, tags, dates, and labels all inherit the browser default (~16px) — no systematic scale. |
| Poor reading line-length | **Low** | `.container` is `max-width: 800px` which is fine, but timeline descriptions can be 300+ characters wide. That's at the upper limit of readability (~75 chars per line). |
| No font weight contrast in body | **Low** | Headings inside `.content h3` have no font-weight rule — they inherit `body` default. All text feels the same weight. |

### 2.3 Color & Contrast — FAIL

| Issue | Severity | Detail |
|-------|----------|--------|
| Color palette is too muted | **High** | `--bg: #faf9f6` + `--accent: #5e6472` + `--line: #e0e0e0`. This is a beige-gray scale with zero personality. There is no brand color, no energy, no emotional signal. |
| Accent color has inadequate contrast on dark backgrounds | **Medium** | `#5e6472` (slate) on `#f0efec` (light beige) in `.sidebar-link.active` is ~2.8:1 contrast — fails WCAG AA for text. |
| Stub-answer text is too light | **Medium** | `color: #777777` (the italic answer text) falls to ~4.6:1 on white — barely passing AA for normal text. Combined with italic + dashed border, it looks like a placeholder, not finalized content. |
| No dark mode | **Medium** | In 2026, a portfolio without dark mode feels unfinished. |
| No semantic color signals | **Medium** | All interactive elements use the same slate accent. Links, buttons, tags, active states — one color for everything. No green for "success", no blue for "information". |

### 2.4 Layout & Spacing — MIXED

| Issue | Severity | Detail |
|-------|----------|--------|
| Monotonous section rhythm | **High** | 7 sections, all identical structure: `h2 + timeline/paragraphs`. No alternation between wide/narrow, no card grid, no visual variety. |
| Sidebar consumes 220px on desktop | **Low** | 220px is reasonable, but the sidebar links use only `#888` color for inactive — very low contrast for secondary navigation. |
| Tab system has 1 active tab | **Medium** | The "Who Am I?" tab nav has 3 commented-out siblings. The tab UI implies multiple panels but only one exists. Either remove the tab system or build out the other panels. |
| Mobile horizontal nav works | **Positive** | The responsive sidebar-to-horizontal-nav conversion is clean. |
| Skills grid uses inline styles | **Low** | `style="display: grid; ..."` works but should be moved to the stylesheet. |

### 2.5 Interaction & Feedback — MIXED

| Issue | Severity | Detail |
|-------|----------|--------|
| Profile pic float animation is unnecessary | **Low** | The `@keyframes float` on the profile photo feels like a template artifact. It doesn't add meaning and can be disorienting. |
| Scroll reveal animations are smooth | **Positive** | `opacity 0.65s + translateY 28px` is well-timed. The staggered cardSlideIn on stubs is a nice touch. |
| No hover state for timeline dots | **Low** | The circular bullets in the timeline don't respond to hover. |
| Resume button hover is abrupt | **Low** | Transitions to accent color but the button itself has no subtle state between rest and hover. |
| No loading states or skeleton screens | **Low** | Not applicable for a static site, but worth noting. |

### 2.6 Consistency — MIXED

| Issue | Severity | Detail |
|-------|----------|--------|
| Inline styles in HTML | **Medium** | `.skills-grid`, `.timeline`, `#education div` all use `style="..."` attributes while the rest of the styling is in CSS. Scattered approach. |
| `.content` cards have no consistent height | **Low** | Some timeline items have short descriptions, some long — creates uneven visual rhythm. |
| Education section breaks the timeline pattern | **Low** | Education uses `padding-left: 40px` on the timeline-item directly, while other sections use `.timeline` parent class. Different approach for the same visual. |
| Project links style matches tab-btn style | **Low** | Both use accent color but tab-btn has border + rounded, while project-links are plain text. Inconsistent interaction affordance. |

---

## 3. Why It Feels "Bland" (Root Causes)

| # | Root Cause | Manifests As |
|---|------------|--------------|
| 1 | **No brand color** | The slate accent is safe but forgettable. A portfolio should have a color that *means something* — blue for trust, warm orange for energy, deep purple for creativity. |
| 2 | **No project visuals** | The most impressive content (E-Commerce platform with 74 commits, Docker CI/CD, live Railway deployment) has zero visual representation. A screenshot of the app would be worth 1000 words. |
| 3 | **Identical section treatments** | Work, Projects, Education, Community all use the `.timeline` pattern. The brain registers this as "same thing again" and stops paying attention. |
| 4 | **Flat hero section** | The hero is a white rectangle with text centered in it. No background texture, no visual weight, no sense of arrival. First impression is "simple page" instead of "I want to hire this person." |
| 5 | **Font not loaded** | The entire site renders in the browser's default sans-serif because Poppins was never imported. This alone makes the site look like it wasn't finished. |
| 6 | **No micro-interactions** | Beyond scroll-reveal, nothing responds to the user. No link hover effects, no skill-group hover states, no timeline-item animations on scroll. |

---

## 4. Recommended Format & Layout Alternatives

For a CS portfolio, here are the most effective format directions, ranked by impact:

### Option A: Card-Based Portfolio (Recommended)

```
┌────────────────────────────────────────────┐
│  HERO — gradient bg, large avatar, tagline │
│  [Email] [LinkedIn] [GitHub] [Resume]      │
├────────────────────────────────────────────┤
│  ABOUT — brief paragraph, 3 stat cards     │
│  (years XP / projects / GPA highlights)    │
├────────────┬───────────────────────────────┤
│  Work      │  ┌─── Card ─────────────────┐ │
│  Timeline  │  │ Screenshot / icon   Date │ │
│  (condensed│  │ Title + description      │ │
│   vertical)│  │ Tags: [Python] [Docker]  │ │
│            │  └──────────────────────────┘ │
│            │  ┌─── Card ─────────────────┐ │
│            │  │ ...                      │ │
├────────────┴───────────────────────────────┤
│  PROJECTS — Card grid with screenshots     │
│  ┌──────┐ ┌──────┐ ┌──────┐               │
│  │ img  │ │ img  │ │ img  │               │
│  │ desc │ │ desc │ │ desc │               │
│  └──────┘ └──────┘ └──────┘               │
├────────────────────────────────────────────┤
│  SKILLS — Visual tag groups / progress     │
│  [Python] [TS] [React] [Docker] [C++]     │
├────────────────────────────────────────────┤
│  FOOTER                                    │
└────────────────────────────────────────────┘
```

**Why this works:** Alternates between vertical timeline (for chronology) and card grid (for visual impact). Breaks the visual rhythm. Projects get screenshots. Skills become scannable tags instead of comma lists.

### Option B: Split-Screen / Dashboard Layout

```
┌───────── ⅓ sidebar ─────────┬────── ⅔ main ──────────────┐
│  Avatar                      │  CONTENT AREA              │
│  Name / Title                │  (changes on nav click)    │
│  [Social links]              │                            │
│                              │  Each section is a full    │
│  ── Nav ────                 │  page or panel:            │
│  About                       │  - Work: expanded view     │
│  Work (3)                    │  - Projects: gallery grid  │
│  Projects (3)                │  - Skills: visual layout   │
│  Education                   │                            │
│  Skills                      │  Single page scroll or     │
│  Community                   │  SPA-style navigation      │
│                              │                            │
│  Resume [↓]                  │                            │
└──────────────────────────────┴────────────────────────────┘
```

**Why this works:** Makes the visitor feel like they're using a tool, not reading a document. Stronger visual separation of concerns. Better for showcasing multiple projects without overwhelming.

### Option C: Minimalist Long-Form (Refine Current)

The lowest-effort improvement — keep the single-column scroll but:
- Add project screenshots inline
- Use alternating left/right image-text blocks
- Add background color bands between sections
- Increase font scale and spacing

---

## 5. Specific Actionable Recommendations

### 5.1 Critical Fixes (Do these first)

| Priority | Fix | Effort |
|----------|-----|--------|
| P0 | **Load Poppins font** — add `<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;600;700&display=swap" rel="stylesheet">` in `<head>` | 1 min |
| P0 | **Remove or populate tab system** — either uncomment the 3 hidden tabs or remove the tab-nav entirely and just show the content. An empty tab UI signals "under construction." | 5 min |
| P1 | **Replace the dashed border on stub-answers** with a solid left border or no border. The dashed + italic + gray combo looks like a wireframe. | 2 min |
| P1 | **Add project screenshots** — at minimum, a screenshot of the E-Commerce platform (it's deployed, take a screenshot) and a photo of the drone or NeuralCube robot. | 20 min |

### 5.2 Medium Impact

| Recommendation | Rationale |
|---------------|-----------|
| **Choose a vibrant accent color** | Pick 1-2 colors that have energy. Candidates: `#2563eb` (blue), `#7c3aed` (purple), `#059669` (emerald), or `#d97706` (amber). The current `#5e6472` is too neutral for a personal brand. |
| **Add a hero background** | A subtle gradient, a mesh pattern, or even just a tinted overlay photo. The white hero blends into the white page. |
| **Convert skills grid to tag cloud** | Use styled `<span>` pills instead of comma-separated text. Bonus: group by category with category headers. |
| **Show timeline dots as interactive indicators** | The circular bullets are positioned but have no hover state. Make them pulse, change color, or reveal extra info on hover. |
| **Add "last updated" context** | Footer says "Updated June 02, 2026" but it's isolated. Pair it with a subtle "site built with [tech used]" note. |
| **Dark mode toggle** | Add a preference-driven dark mode. The color palette needs very few changes: `--bg: #1a1a1a`, `--text: #e5e5e5`, `--accent: #94a3b8`. |

### 5.3 High Impact (Redesign-adjacent)

| Recommendation | Rationale |
|---------------|-----------|
| **Split Work & Projects into different layouts** | Keep the timeline for Work (chronology matters). Switch Projects to a 2-column card grid with screenshots (visual impact matters). |
| **Add a stats/impact strip** | "3 internships · 4 research positions · 3.85 GPA · 3 languages" — social proof numbers above the fold. |
| **Reconsider the sidebar** | Sidebars work for dashboards, not for portfolio sites. A fixed-top nav is more conventional and gives you back 220px of content width. If you keep the sidebar, make it dark-themed so it visually separates. |
| **Add a "Featured Work" section** | Before the full timeline, show 1-2 highlighted experiences with more visual treatment (larger card, screenshot, key outcomes). |
| **Use numbered stats** | "Reduced manual inspection overhead" is good. "Reduced manual inspection overhead by 40%" is better. Quantify where possible. |

---

## 6. Design Contract Blueprint (If Rebuilding)

If you decide to rebuild rather than retrofit, here is the recommended design contract:

### Color
| Role | Value | Usage |
|------|-------|-------|
| Dominant (60%) | `#ffffff` / `#0f172a` (dark) | Page background |
| Secondary (30%) | `#f8fafc` / `#1e293b` (dark) | Cards, sidebar |
| Accent (10%) | `#2563eb` (blue) | Links, buttons, active states, timeline dots |
| Destructive | `#dc2626` | *(not used on this site)* |
| Muted text | `#64748b` | Tags, dates, secondary info |

### Typography
| Role | Size | Weight | Line Height |
|------|------|--------|-------------|
| Body | 16px | 400 | 1.6 |
| Small/Label | 14px | 500 | 1.4 |
| H3 (card titles) | 18px | 600 | 1.3 |
| H2 (section) | 28px | 700 | 1.2 |
| H1 (hero) | 48px | 700 | 1.1 |

*Font: Poppins (body) + JetBrains Mono (code snippets, tags)*

### Spacing (8-point scale)
| Token | Value | Usage |
|-------|-------|-------|
| xs | 8px | Tag padding, icon gaps |
| sm | 16px | Card padding |
| md | 24px | Section gaps |
| lg | 32px | Major section padding |
| xl | 48px | Page section breaks |
| 2xl | 64px | Hero padding |

---

## 7. Quick Wins (30 min total)

If you want to make the site look significantly better in a single sitting:

1. **Load Poppins** — add the `<link>` tag (1 min)
2. **Remove float animation** on profile pic (30 sec)
3. **Replace tab system** — either show all stub-cards without tabs, or uncomment the other panels and fill them in (10 min)
4. **Change accent color** to something vibrant — swap `--accent` in `:root` (1 min)
5. **Fix stub-answer styling** — remove dashed border, use solid left accent border instead (2 min)
6. **Add one project screenshot** — take a screenshot of the E-Commerce live demo, add it as an `<img>` in the project card (10 min)
7. **Tighten timeline descriptions** — aim for 2-3 lines max per entry, move details to a "read more" or trust the resume PDF (5 min)

After these 7 changes (~30 min), the site will look **dramatically** more polished.

---

## 8. Competitive Context

For context, here's how this site compares to peers applying to similar roles:

| Aspect | Current | Typical CS Portfolio (2026) |
|--------|---------|----------------------------|
| **First impression** | "Clean but basic" | "Impressive / shows personality" |
| **Project presentation** | Text-only timeline | Screenshots + links + architecture diagrams |
| **Color** | Muted slate | Brand color (blue/purple/green) + accent |
| **Typography** | System default (Poppins not loaded) | Loaded font with scale |
| **Interactivity** | Scroll-reveal only | Hover states, micro-animations, maybe dark mode |
| **Mobile** | Functional | Often responsive-first |
| **Performance** | Excellent (static HTML) | Varies (many use heavy frameworks for portfolio) |

This site is not bad — it's just not memorable. For a graduating CS senior with a
3.85 GPA, Waygate/Tive/Tufts experience, and a deployed e-commerce platform,
the site should *feel* as capable as the person behind it.

---

*End of UI Analysis. Produced 2026-06-03.*
