# HMA Web Platform — Design Specification
**Human Mastery Architecture · Web (Desktop-first)**
Last updated: 2026-11-20
Reference image: `~/Downloads/Clear visual for the HMA program (1).png`
Prototype target: `prototype/web.html`

---

## 1. Design Philosophy

The web platform is **a place you arrive at**, not a tool you open. Every screen should feel like stepping into a private sanctuary — warm, still, unhurried. Nature is the structural metaphor: light through forest canopy, mountain stillness, the breath before dawn.

Six principles govern every decision:

1. **Nature as architecture** — Backgrounds are not wallpaper. They are the world the Architect inhabits. Forest, mountain, moonlit water, firelight. Full-bleed, atmospheric, alive.
2. **Warmth over polish** — Gold, ivory, deep forest green. Never clinical white, cold blue, or tech-grey.
3. **Restraint** — Negative space is the luxury. No crowding. Every element earns its place.
4. **Presence over pace** — No streaks, no gamification, no red badges. The platform respects attention.
5. **Private** — The experience feels personal and contained. Nothing looks communal or social.
6. **Quiet confidence** — Typography is serif and unhurried. CTAs are warm gold, never urgent orange or electric blue.

---

## 2. Colour System

### Core palette

| Token | Hex | Use |
|---|---|---|
| `--gold` | `#C8A96E` | Primary accent — headings, CTAs, icons, active states |
| `--gold-lt` | `#E8D090` | Large display headings (lighter, more luminous) |
| `--gold-soft` | `rgba(200,169,110,0.18)` | Hover states, selected card fills |
| `--gold-border` | `rgba(200,169,110,0.28)` | Card borders, dividers, input borders |
| `--text` | `#F5EDD8` | Primary body text — warm ivory |
| `--text-soft` | `rgba(245,237,216,0.58)` | Secondary text, descriptions, labels |
| `--text-muted` | `rgba(245,237,216,0.32)` | Placeholder text, disabled states |
| `--card` | `rgba(10,16,10,0.72)` | Card background — dark warm glass |
| `--card-2` | `rgba(15,22,12,0.88)` | Heavier card variant (video info, entry footers) |
| `--sidebar` | `rgba(6,12,6,0.90)` | Sidebar background |

### Colour rules
- **Never** use pure white `#FFFFFF` — use `--text` ivory instead.
- **Never** use cold blue or purple tones anywhere in the UI.
- Gold is the only accent. There is no secondary accent colour.
- Destructive actions (if any) use muted red-brown, never bright red.

---

## 3. Typography

### Typefaces

| Family | Role | Google Fonts import |
|---|---|---|
| **Cormorant Garamond** | Display, headings, card titles, section names, CTA labels | `wght@400;500;600` + italic `ital,wght@1,400;1,500` |
| **Inter** | UI labels, body text, navigation, metadata, form fields | `wght@300;400;500` |

### Type scale

| Name | Family | Size | Weight | Use |
|---|---|---|---|---|
| `t-display` | Cormorant | 52px / 4xl | 500 | Hero headings (splash, section heroes) |
| `t-h1` | Cormorant | 38px | 500 | Page titles |
| `t-h2` | Cormorant | 28px | 500 | Section headings, card headers |
| `t-h3` | Cormorant | 22px | 500 | Sub-section titles |
| `t-label` | Inter | 11px | 400 | Uppercase eyebrow labels — `letter-spacing: 0.14em`, `text-transform: uppercase`, colour `--gold` |
| `t-body` | Inter | 14–15px | 400 | Paragraph text, descriptions |
| `t-sm` | Inter | 13px | 400 | Secondary text, metadata |
| `t-xs` | Inter | 11.5px | 400 | Timestamps, duration, micro-labels |

### Typography rules
- Display and h1 headings always in `--gold-lt` on dark backgrounds.
- Body text in `--text`. Descriptive/secondary text in `--text-soft`.
- Eyebrow labels (`.t-label`) are always gold, uppercase, widely tracked.
- Line height: display `1.15`, headings `1.2`, body `1.65–1.75`.
- Letter spacing: display `0.01em`, labels `0.14em`, body `0`.

---

## 4. Background System

The background is not a colour — it is a scene. Each screen group uses a CSS gradient that approximates a specific natural environment. No external image dependencies in the prototype; production will use real photography.

### Scene definitions

#### `bg-forest` — Forest at golden hour (default for most screens)
```css
background:
  radial-gradient(ellipse at 25% 65%, rgba(40,80,15,0.70) 0%, transparent 55%),
  radial-gradient(ellipse at 75% 30%, rgba(90,60,10,0.45) 0%, transparent 45%),
  radial-gradient(ellipse at 50% 100%, rgba(20,40,8,0.9) 0%, transparent 50%),
  linear-gradient(168deg, #0a1408 0%, #111f0a 30%, #0e1808 55%, #1a1005 80%, #0d0c05 100%);
```
*Use on: Splash, Experience picker, Atmosphere, Dashboard, Today, Meditations, Wisdom, Progress, Vision.*

#### `bg-warm` — Warm indoor / candlelight
```css
background:
  radial-gradient(ellipse at 40% 70%, rgba(80,45,8,0.65) 0%, transparent 55%),
  radial-gradient(ellipse at 60% 20%, rgba(30,55,10,0.60) 0%, transparent 50%),
  linear-gradient(160deg, #0a0f04 0%, #171208 45%, #1a1005 100%);
```
*Use on: Sign In, Journal, Private Sessions.*

#### `bg-moon` — Moonlit water / night completion
```css
background:
  radial-gradient(ellipse at 50% 15%, rgba(200,210,255,0.12) 0%, transparent 35%),
  radial-gradient(ellipse at 50% 90%, rgba(5,10,25,0.95) 0%, transparent 55%),
  linear-gradient(180deg, #04080f 0%, #080d1a 45%, #050810 100%);
```
*Use on: Day Complete screen only.*

### Overlay rule
All cards, sidebars, and content panels sit on top of these backgrounds. The background is always visible — bleed through the gaps between cards. Never cover the background entirely with solid panels.

### Production photography direction
When replacing gradients with real photos:
- Forest/mountain: golden hour, low angle sun through canopy, misty mornings
- Warm indoor: soft lamp light, wood, candle, contemplative desk
- Moonlit: calm water surface under full moon, distant fire on a beach
- **No stock-photo aesthetics** — all images should feel editorial, intimate, slightly cinematic

---

## 5. Component Library

### 5.1 Cards

#### Standard card `.card`
```
background: var(--card)        // rgba(10,16,10,0.72)
border: 1px solid var(--gold-border)
border-radius: 16px
padding: 28px 32px
```

#### Compact card `.card-sm`
```
background: var(--card)
border: 1px solid var(--gold-border)
border-radius: 12px
padding: 20px 24px
```

Cards never have drop shadows — the dark glass is contrast enough against the background.

---

### 5.2 Buttons

#### Primary `.btn-gold`
```
background: linear-gradient(135deg, #C8A96E, #A88040)
color: #1a0f05 (dark warm brown — NOT black)
font-family: Cormorant Garamond
font-size: 17px
font-weight: 600
letter-spacing: 0.04em
border-radius: 50px (pill)
padding: 14px 36px
border: none
cursor: pointer
```
Hover: `background: linear-gradient(135deg, #E8C980, #C8A96E)` + `translateY(-1px)`

#### Outline `.btn-outline`
```
background: transparent
color: var(--gold)
font-family: Cormorant Garamond
font-size: 16px
border: 1px solid var(--gold-border)
border-radius: 50px
padding: 12px 28px
```
Hover: `background: var(--gold-soft)` + `border-color: var(--gold)`

#### Ghost text `.btn-text`
```
background: none
border: none
color: var(--text-soft)
font-family: Inter
font-size: 13px
padding: 4px 0
```
Hover: `color: var(--text)`

---

### 5.3 Form Inputs

#### Text input `.form-input`
```
background: rgba(255,255,255,0.07)
border: 1px solid var(--gold-border)
border-radius: 10px
padding: 14px 16px 14px 44px  // 44px left = icon space
color: var(--text)
font-family: Inter
font-size: 14px
```
Focus: `border-color: var(--gold)` (no glow/shadow)
Placeholder: `--text-muted`
Icon: 16×16px SVG, left-anchored at 16px, `color: var(--text-soft)`

---

### 5.4 Toggle Switches

```
Track size: 48×26px
Border-radius: 13px
Off state: rgba(255,255,255,0.12)
On state: var(--gold)
Knob: 20×20px white circle, top/left offset 3px
Transition: transform 0.22s, background 0.22s
Knob-on: translateX(22px)
```

Sound rows that contain toggles:
```
padding: 14px 18px
border-radius: 10px
border: 1px solid var(--gold-border)
background: rgba(10,16,8,0.6)
```
On state border: `rgba(200,169,110,0.5)`

---

### 5.5 Range Slider (Volume)

```
height: 3px
background: rgba(255,255,255,0.15)
border-radius: 2px
Thumb: 18×18px circle, var(--gold), box-shadow 0 2px 6px rgba(0,0,0,0.3)
```

---

### 5.6 Navigation — Sidebar

```
Width: 220px
Background: rgba(6,12,6,0.90)
Border-right: 1px solid var(--gold-border)
Padding: 28px 0 20px
Position: fixed left, full viewport height
```

**Logo area** (top):
```
padding: 0 22px 28px
border-bottom: 1px solid var(--gold-border)
HMA leaf SVG (28×28) + "HMA" in Cormorant Garamond 18px gold
```

**Nav items**:
```
padding: 11px 22px
font-size: 13.5px
color: var(--text-soft)
icon: 16×16 SVG, opacity 0.7
gap: 12px
```
Active state: `color: var(--gold)`, `background: rgba(200,169,110,0.12)`, `border-right: 2px solid var(--gold)`
Hover: `color: var(--text)`, `background: rgba(200,169,110,0.08)`

**Nav items (8 total)**:
1. Home — house icon
2. My Journey — clock icon
3. Meditations — music note icon
4. Journal — open book icon
5. Wisdom Cards — heart icon
6. Progress — bar chart icon
7. Resources (Life Vision) — play circle icon
8. My Sessions — calendar icon

**Avatar** (bottom):
```
padding: 0 22px
36×36px circle, var(--gold-soft) fill, gold border
Name label in Inter 12.5px, --text-soft
```

---

### 5.7 ARCH™ Phase Boxes

4-column grid, equal widths:
```
background: var(--card)
border: 1px solid var(--gold-border)
border-radius: 12px
padding: 20px 16px
text-align: center
```
Active phase: `background: var(--gold-soft)`, `border-color: var(--gold)`

Contents:
- Letter: Cormorant 36px 600 `--gold`, line-height 1
- Phase name: Cormorant 15px `--text`
- Day range: Inter 11px uppercase `--text-soft`, letter-spacing 0.08em

---

### 5.8 Day Progress Ring

SVG circle, 100×100px:
- Track circle: `rgba(200,169,110,0.15)`, stroke-width 6
- Fill arc: `var(--gold)`, stroke-linecap round, stroke-dasharray 263.9
- Rotate -90deg (start at top)
- Inner label: day number (Cormorant 28px 600 gold) + "/28" (Inter 11px soft)

---

### 5.9 Checklist Items

```
padding: 16px 20px
border-radius: 10px
border: 1px solid var(--gold-border)
background: rgba(10,16,8,0.6)
display: flex, align-items: center, gap: 14px
```
Done state: `background: var(--gold-soft)`, `border-color: rgba(200,169,110,0.5)`

Check circle: 28×28px, border 1.5px, `--gold-border`
Done circle: `background: var(--gold)`, `border-color: var(--gold)` + white checkmark SVG inside

---

### 5.10 Filter Tabs

```
padding: 7px 16px
border-radius: 50px (pill)
border: 1px solid var(--gold-border)
background: transparent
color: var(--text-soft)
font-size: 12.5px
```
Active / hover: `background: var(--gold-soft)`, `border-color: var(--gold)`, `color: var(--gold)`

---

### 5.11 Progress Bars

Row layout: label (140px fixed width) + track (flex 1):
```
Track: height 4px, background rgba(255,255,255,0.1), border-radius 2px
Fill: background linear-gradient(90deg, var(--gold), var(--gold-lt))
Transition: width 0.6s ease
```

---

## 6. Layout System

### 6.1 Full-screen onboarding (Screens 1–4)

No sidebar. Content centred in the full viewport.

```
Splash / Sign In: single centred column, max-width 400–480px
Experience picker: max-width 900px, 3-column card grid
Atmosphere: max-width 720px, 2-column toggle grid
```

### 6.2 App shell (Screens 5–12)

```
Layout: flex-row
Sidebar: 220px fixed left
Main content: flex-1, overflow-y auto, scrollbar hidden
```

Main content panels use:
```
min-height: 100%
padding: 40px 48px
```

### 6.3 Panel grid patterns

| Panel | Layout |
|---|---|
| Dashboard | Full-width header row + 4-col ARCH grid + 3-col quick links |
| Today's Experience | 2-col: checklist (1fr) · video+side-panel (1.3fr) |
| Meditation Library | Filter tabs + 4-col card grid |
| Journal | Single column, max-width 640px |
| Wisdom Cards | 3-col card grid |
| Progress | 2-col: ring (180px) · bar charts (flex 1) |
| Life Vision | Centred, min-height 60vh |
| Private Sessions | Single column, max-width 520px |

### 6.4 Spacing tokens

| Token | Value | Use |
|---|---|---|
| `gap-sm` | 8px | Tight icon+label rows |
| `gap-md` | 16px | Card grids, button groups |
| `gap-lg` | 24px | Section gaps |
| `mt-sm` | 12px | Tight vertical rhythm |
| `mt-md` | 24px | Standard section gap |
| `mt-lg` | 40px | Major section break |

---

## 7. Screen Inventory

### Screen 1 — Splash / Landing

**Background:** `bg-forest`
**Layout:** Centred, single column

| Element | Spec |
|---|---|
| HMA leaf logo SVG | 64×64px, gold stroke |
| Eyebrow label | "The Human Mastery Architecture™" · `.t-label` |
| Display heading | "HMA" · `.t-display` · `--gold-lt` |
| Tagline | "Your Human Mastery Architecture™" · Cormorant 19px italic · `--text-soft` |
| Descriptor | "A 28-Day Private Online Journey / to Clarity · Capacity · Mastery · Legacy" · Inter 13.5px · `--text-soft` |
| CTA | "Begin Your Journey →" · `.btn-gold` → `s-signin` |

---

### Screen 2 — Sign In

**Background:** `bg-warm`
**Layout:** Centred card, max-width 400px

| Element | Spec |
|---|---|
| Small logo | 36px leaf SVG above heading |
| Heading | "Welcome, Architect" · `.t-h1` · `--gold-lt` |
| Email field | Icon: envelope SVG · placeholder "Email" |
| Password field | Icon: lock SVG · placeholder "Password" · show/hide eye icon right |
| Primary CTA | "Log In" · `.btn-gold` full-width → `s-experience` |
| Ghost links | "Forgot password?" · "Create Account" · `.btn-text` centred |

---

### Screen 3 — Choose Your Experience

**Background:** `bg-forest`
**Layout:** Centred, max-width 900px

| Element | Spec |
|---|---|
| Eyebrow | "Step 1" |
| Heading | "Choose Your Experience" |
| Sub-label | "A personalised environment for your 28-day journey" |
| Card grid | 3 columns, equal width |

**Experience cards (3):**

| Card | Photo gradient | Title | Description |
|---|---|---|---|
| Immersive *(default selected)* | Deep forest green radial | Immersive | Nature-rich, sensory and fully immersive |
| Neutral | Soft grey-green | Neutral | Clean, calm and focused |
| Masculine | Dark grey-blue | Masculine | Strong, grounded and performance-led |

Card states: Default / Selected (gold border + glow). Radio circle bottom of info panel.

CTA: "Continue →" `.btn-gold` centred + "← Back" `.btn-text` below → `s-atmosphere`

---

### Screen 4 — Set Your Atmosphere

**Background:** `bg-forest`
**Layout:** Centred, max-width 720px, 2-column toggle grid

**Left column — Nature Sounds (5 rows):**

| Sound | Icon | Default |
|---|---|---|
| Forest & Birds | 🌿 | ON |
| Waterfall & River | 💧 | off |
| Ocean & Waves | 🌊 | off |
| Fire & Hearth | 🔥 | off |
| Night & Stars | 🌙 | off |

Volume slider below (range input, `var(--gold)` thumb).

**Right column — Binaural Focus (4 rows):**

| Option | Default |
|---|---|
| Deep Focus 40 Hz | ON |
| Creativity 12 Hz | off |
| Calm & Balance 8 Hz | off |
| Sleep & Recovery 4 Hz | off |

CTA: "Continue →" → `s-app / p-dashboard` + "← Back" → `s-experience`

---

### Screen 5 — Dashboard (Home)

**Panel:** `p-dashboard` · **Background:** `bg-forest`

**Header row (flex, space-between):**
- Left: eyebrow date label + "Good Morning, Architect" h1 + descriptor text
- Right: Day progress ring (Day 7/28)

**ARCH™ Journey card:**
- Label: "ARCH™ Journey"
- 4-column phase grid (A active = Awareness Days 1–7)
- CTA below: "Continue Today's Experience →" `.btn-gold` → `p-today`

**Quick-links row (3-col grid):**
- My Journal: "Today's reflection awaits"
- Wisdom Cards: "Daily inspiration"
- Private Sessions: "Next session: Thursday"

---

### Screen 6 — Today's Experience

**Panel:** `p-today` · **Background:** `bg-forest`

**Header:**
- Eyebrow: "Day 7 of 28"
- h1: "Today's Experience – Day 7" · `--gold-lt`
- Sub-label: "AWARENESS — See Yourself Clearly" · uppercase · `--text-soft`

**2-column body:**

Left column — Checklist (5 items):

| Item | Duration | Default state |
|---|---|---|
| Arrival & Breath | 5 min | Done ✓ |
| Daily Insight | 10 min | — |
| Reflection | 10 min | — |
| Today's Action | 5 min | — |
| Integration | 5 min | — |

Right column:
- Video player mock (16:9, `bg-forest` gradient, gold play button, timestamp "10:24")
- Today's Focus card (`.card-sm`):
  - Label: "Today's Focus"
  - Question: "What part of me is ready to be seen, healed or released?"
  - Divider
  - Gold checkmark label: "Action for Today"
  - Action text: "Take one conscious action that brings me closer to who I truly am."

---

### Screen 7 — Meditation Library

**Panel:** `p-meditations` · **Background:** `bg-forest`

Filter tabs row: All · Energy · Focus · Emotional Balance · Sleep · Abundance

4-column meditation card grid:

| Card | Thumbnail gradient | Title | Duration |
|---|---|---|---|
| 1 | Deep green radial | Inner Clarity | 12 min |
| 2 | Olive-green | Resilience | 15 min |
| 3 | Warm amber | Abundance | 18 min |
| 4 | Deep navy | Sleep & Recovery | 20 min |

Each card: thumbnail (130px) + play icon overlay + info panel (title + duration).

---

### Screen 8 — My Journal

**Panel:** `p-journal` · **Background:** `bg-warm`
**Max-width:** 640px

- Eyebrow: "Private Space"
- h1: "My Journal"
- Descriptor: "A private space to reflect, release and realign."
- CTA: "New Entry  +" `.btn-gold`

Journal entry list (5 rows, chevron right):
1. Today's Reflection *(with sub-label "Day 7 · Awareness")*
2. Gratitude
3. What I Noticed
4. What I'm Releasing
5. My Next Step

---

### Screen 9 — Wisdom Cards

**Panel:** `p-wisdom` · **Background:** `bg-forest`

- Eyebrow: "Daily Inspiration"
- h1: "Wisdom Cards"
- Descriptor: "Daily inspiration from timeless wisdom."

3-column wisdom card grid:

| Card | Photo gradient | Icon | Title | Sub |
|---|---|---|---|---|
| Bible | Dark forest green | ✦ | Bible | Guidance & Strength |
| Stoic | Warm dark olive | ◎ | Stoic | Perspective & Clarity |
| Islamic | Deep navy | ◇ | Islamic | Surrender & Trust |

CTA below: "More Traditions →" `.btn-outline`

---

### Screen 10 — My Progress

**Panel:** `p-progress` · **Background:** `bg-forest`

- Eyebrow: "Your Growth"
- h1: "My Progress"
- Descriptor: "A clear view of your growth across the 28-day journey."

2-column layout:
- Left: 160×160px progress ring — **62%** completion (stroke-dashoffset calculated from 414.7 circumference)
- Right: 6 progress bars

| Metric | Fill % |
|---|---|
| Clarity | 78% |
| Energy | 62% |
| Focus | 70% |
| Emotional Balance | 55% |
| Resilience | 68% |
| Wellbeing | 72% |

---

### Screen 11 — Life Vision

**Panel:** `p-vision` · **Background:** `bg-forest`
**Layout:** Centred column, min-height 60vh

- Eyebrow: "Your Blueprint"
- Display heading: "Life Vision"
- Descriptor: "Revisit, refine and bring your vision to life."
- CTA: "My Vision →" `.btn-gold`

---

### Screen 12 — Private Sessions

**Panel:** `p-sessions` · **Background:** `bg-warm`
**Max-width:** 520px

- Eyebrow: "1:1 Advisory"
- h1: "Private Sessions"
- Descriptor: "Your 1:1 advisory sessions and key milestones."

3 stacked buttons:
1. "Book a Session" — `.btn-gold` full-width left-aligned
2. "My Schedule" — `.btn-outline` full-width left-aligned
3. "Session Notes" — `.btn-outline` full-width left-aligned

---

### Screen 13 — Day Complete

**Background:** `bg-moon` · **No sidebar**
**Layout:** Centred, single column

- Small HMA leaf SVG (40px)
- Headline: "The day is complete. / Return to yourself." · Cormorant 28px · `--gold-lt` · line-height 1.6
- Tagline: "Rest. Integrate. Rise." · Cormorant 22px · `--text-soft` · letter-spacing 0.08em
- CTA: "Return Home" `.btn-outline` → Dashboard

---

## 8. Navigation Map

```
s-splash
  └─ Begin Your Journey → s-signin
       └─ Log In → s-experience
            └─ Continue → s-atmosphere
                 └─ Continue → s-app (p-dashboard)
                      ├─ Home          → p-dashboard
                      ├─ My Journey    → p-today
                      ├─ Meditations   → p-meditations
                      ├─ Journal       → p-journal
                      ├─ Wisdom Cards  → p-wisdom
                      ├─ Progress      → p-progress
                      ├─ Resources     → p-vision
                      └─ My Sessions   → p-sessions
                           └─ (Day end) → s-complete
                                └─ Return Home → p-dashboard
```

---

## 9. Interaction Patterns

### Transitions
- Screen-to-screen: `opacity 0.4s ease` (fade only — no slides, no scale)
- Hover on cards/buttons: `transform: translateY(-1px)` + colour shift, `0.2s ease`
- Toggle on/off: `0.22s ease`
- Progress bar fill: `0.6s ease` (animate on panel enter)

### Selection states
- Experience cards: gold border + subtle glow (`box-shadow: 0 0 0 1px var(--gold), 0 8px 32px rgba(200,169,110,0.2)`)
- Checklist items: gold-soft background fill
- Filter tabs: gold-soft background + gold border + gold text
- Nav items: gold text + right-side gold bar + gold-soft background

### Focus / accessibility
- Focus rings: `outline: 2px solid var(--gold)`, offset 2px
- Interactive elements minimum 44×44px touch target
- Contrast: `--text` on `--card` background passes WCAG AA

---

## 10. HMA Logo / Mark

The HMA leaf mark is a simple hand-drawn SVG:
- Outer leaf shape: two mirrored arcs meeting at top and bottom points
- Centre vein: single vertical line, 60% opacity
- Side veins: two short angled lines, 50% opacity
- Stroke: `var(--gold)`, stroke-width 1.5, fill none
- Sizes used: 64px (splash), 36px (sign-in), 28px (sidebar)

---

## 11. Responsive Behaviour (Post-MVP)

The current spec targets **desktop (1280px+)**. Future breakpoints:

| Breakpoint | Behaviour |
|---|---|
| ≥1280px | Full sidebar + multi-column panels |
| 768–1279px | Sidebar collapses to icons only (48px) |
| <768px | Sidebar becomes bottom nav · panels go single-column · falls back to mobile prototype (`index.html`) |

---

## 12. What This Design Is NOT

- Not the existing mobile glass prototype (`prototype/index.html`) — that is a separate system (blue glass, dark env, cqw units)
- Not the marketing site (`sites/hma/`) — that is brand/landing content
- Not cold, blue, or clinical
- Not gamified — no streaks, no badges, no points
- Not cluttered — maximum 2–3 elements per row; white space is intentional
