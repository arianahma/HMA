# HMA — UI Design System
**Human Mastery Architecture · Digital Platform**
Last updated: 2026-11-19

Clickable prototype: `../prototype/index.html`

---

## Design principles

1. **Restraint** — Negative space is the luxury. If a pixel isn't earning its place, remove it.
2. **Nature as architecture** — Environments feel like real places, not digital skins. Texture, light, depth.
3. **Warmth over polish** — The product is intimate and human. Gold, ivory, forest — not clinical white and grey.
4. **Presence** — The UI is a place you go to, not a tool you use. Every screen should feel like arrival.
5. **Less time, greater return** — No gamification. No streaks. No red badges. The product respects the user's attention.
6. **Private** — Nothing leaks between participants. Everything feels personal, not communal.

---

## Environments — the 4 time-aware worlds

The app reads device time and renders a matching environment. This is not a visual theme — it is the ambient world the participant inhabits during their practice.

### Dawn · 04:00–08:00
Mist rising. Amber light breaking through forest canopy. The world before it begins.

| Token | Value | Use |
|---|---|---|
| `--env-bg` | `#120D08` | Full bleed background |
| `--env-bg-2` | `#2E1A08` | Gradient end |
| `--env-glow` | `rgba(220,140,40,0.18)` | Radial glow centre |
| `--env-surface` | `rgba(255,220,150,0.07)` | Card backgrounds |
| `--env-border` | `rgba(220,170,80,0.15)` | Card borders |
| `--env-text` | `#F5E8C8` | Primary text |
| `--env-text-soft` | `rgba(240,220,170,0.55)` | Secondary text |
| `--env-accent` | `#E8A040` | Gold — CTA, highlights |
| `--env-accent-soft` | `rgba(232,160,64,0.15)` | Accent tint |
| `--env-phase-dot` | `#E8A040` | Phase indicator |

### Day · 08:00–17:00
Sunlit stone. Warm ivory. The world in full clarity.

| Token | Value | Use |
|---|---|---|
| `--env-bg` | `#F4F0E6` | Full bleed background |
| `--env-bg-2` | `#EDE7D8` | Gradient end |
| `--env-glow` | `rgba(180,150,80,0.08)` | Subtle warmth |
| `--env-surface` | `rgba(255,253,248,0.90)` | Card backgrounds |
| `--env-border` | `rgba(180,155,100,0.18)` | Card borders |
| `--env-text` | `#1C2820` | Primary text |
| `--env-text-soft` | `rgba(60,50,35,0.50)` | Secondary text |
| `--env-accent` | `#9A7B43` | Gold — CTA, highlights |
| `--env-accent-soft` | `rgba(154,123,67,0.12)` | Accent tint |
| `--env-phase-dot` | `#9A7B43` | Phase indicator |

### Dusk · 17:00–20:00
Bronze light on water. The day releasing itself. Warmth deepening.

| Token | Value | Use |
|---|---|---|
| `--env-bg` | `#1A0E08` | Full bleed background |
| `--env-bg-2` | `#3A1808` | Gradient end |
| `--env-glow` | `rgba(200,110,40,0.20)` | Warm radial |
| `--env-surface` | `rgba(220,140,60,0.07)` | Card backgrounds |
| `--env-border` | `rgba(200,130,60,0.18)` | Card borders |
| `--env-text` | `#F0DCC0` | Primary text |
| `--env-text-soft` | `rgba(230,200,150,0.55)` | Secondary text |
| `--env-accent` | `#C87838` | Bronze — CTA, highlights |
| `--env-accent-soft` | `rgba(200,120,56,0.15)` | Accent tint |
| `--env-phase-dot` | `#C87838` | Phase indicator |

### Night · 20:00–04:00
Deep pine. Moonlight on stone. Stars. The world at rest, alive.

| Token | Value | Use |
|---|---|---|
| `--env-bg` | `#080F0C` | Full bleed background |
| `--env-bg-2` | `#101C14` | Gradient end |
| `--env-glow` | `rgba(100,160,130,0.12)` | Cool forest glow |
| `--env-surface` | `rgba(100,160,130,0.07)` | Card backgrounds |
| `--env-border` | `rgba(120,170,145,0.14)` | Card borders |
| `--env-text` | `#E0EDE5` | Primary text |
| `--env-text-soft` | `rgba(200,230,210,0.50)` | Secondary text |
| `--env-accent` | `#88B8A0` | Moonstone — CTA, highlights |
| `--env-accent-soft` | `rgba(136,184,160,0.14)` | Accent tint |
| `--env-phase-dot` | `#88B8A0` | Phase indicator |

---

## ARCH phase colours

Each phase carries its own identity woven subtly through the day's experience.

| Phase | Days | Name | Colour | Hex |
|---|---|---|---|---|
| **A** | 1–7 | Awareness | Sage | `#A8C080` |
| **R** | 8–14 | Realign | Champagne | `#C8A060` |
| **C** | 15–21 | Capacity | Slate | `#7898B0` |
| **H** | 22–28 | Habits | Forest | `#6A9870` |

---

## Typography

| Role | Font | Weight | Size | Letter-spacing |
|---|---|---|---|---|
| Display heading | Cormorant Garamond | 400 | 36–48px | -0.02em |
| Section heading | Cormorant Garamond | 500 | 24–28px | -0.01em |
| Greeting (italic) | Cormorant Garamond | 300 italic | 28–32px | 0 |
| Subheading | Inter | 500 | 13px | 0.08em uppercase |
| Body | Inter | 400 | 15–16px | 0 |
| Caption / label | Inter | 400 | 12px | 0.04em |
| CTA button | Inter | 500 | 14px | 0.06em |
| Wisdom quote | Cormorant Garamond | 400 italic | 20–22px | 0.01em |

**Rule:** Cormorant for Ariana's voice and the programme's soul. Inter for structure, navigation, and UI chrome. Never mix roles.

---

## Spacing system

Base unit: `8px`

| Token | Value | Use |
|---|---|---|
| `--space-xs` | 4px | Icon gap, tight labels |
| `--space-sm` | 8px | Inner card padding (tight) |
| `--space-md` | 16px | Standard gap, inner padding |
| `--space-lg` | 24px | Section gap, card padding |
| `--space-xl` | 40px | Major section break |
| `--space-2xl` | 64px | Screen top padding |

---

## Component library

### Glass card
The fundamental surface. Frosted glass over the environment background.

```
background: var(--env-surface)
backdrop-filter: blur(20px) saturate(1.4)
border: 1px solid var(--env-border)
border-radius: 20px
padding: 24px
```

Variants: `card--large` (28px radius, 32px padding), `card--compact` (16px radius, 16px padding), `card--flush` (no border-radius on one side for bottom sheet).

---

### Environment pill
The floating environment switcher. Developer/demo use and manual override.

Small pill, bottom-right, `position: fixed`. Shows current environment icon (dawn/day/dusk/night). Tap to cycle.

---

### ARCH phase badge
Inline badge showing current phase.

```
height: 22px
border-radius: 11px
background: var(--phase-colour) at 15% opacity
color: var(--phase-colour)
font: Inter 500 11px / 0.08em uppercase
padding: 0 10px
```

---

### Primary CTA button
Full-width on mobile, 56px height.

```
background: var(--env-accent)
color: #fff (dark environments) / #1C2820 (Day)
border-radius: 16px
font: Inter 500 14px / 0.06em uppercase
height: 56px
```

Hover/active: 6% darker. Disabled: 30% opacity. No box-shadow — the environment provides the depth.

---

### Ghost button
Secondary action. Outline only.

```
background: transparent
border: 1.5px solid var(--env-border)
color: var(--env-text)
border-radius: 16px
height: 48px
```

---

### Bottom navigation
Fixed, 5 destinations. Frosted glass.

```
height: 72px + safe area inset
background: var(--env-surface)
backdrop-filter: blur(24px)
border-top: 1px solid var(--env-border)
```

Tabs: Today · Journey · Library · Profile
Active tab: accent colour icon + label. Inactive: soft text colour, no label.

---

### Progress ring
28-segment arc. Used on Journey screen and Today view mini badge.

Each segment = 1 day. Completed: filled accent. Today: glowing accent with pulse. Future: faint border only. Phase breaks shown as slight gaps.

---

### Pillar chip
Selection chip for the 10 pillars.

```
height: 36px
border-radius: 18px
padding: 0 16px
font: Inter 400 13px
```

Unselected: `var(--env-surface)` bg + `var(--env-border)` border.
Selected: `var(--env-accent-soft)` bg + `var(--env-accent)` border + accent text.

---

### Step indicator
3-dot progress for the daily flow (Lesson → Reflect → Act → Observe).

```
4 dots × 6px each
Active: var(--env-accent) filled
Complete: var(--env-accent) at 40% opacity
Upcoming: var(--env-border)
```

---

### Wisdom card
Standalone card for daily wisdom.

```
Eyebrow: tradition + theme (Inter 400 11px uppercase)
Quote: Cormorant Garamond 400 italic 20px
Attribution: Inter 400 12px soft
Reflection: Inter 400 14px body
Save icon: top right
```

---

## Screen inventory

### 01 · Sign in
- Full bleed environment (Day by default)
- HMA mark centred, 48px
- "Good to meet you." in Cormorant italic below mark
- Google sign-in button (ghost style)
- Email/password link below
- No marketing copy. Trust through restraint.

### 02 · Waitlist
- Same environment shell
- "Your place is being confirmed." — Cormorant 28px
- "Ariana will reach out before your programme begins." — Inter 15px soft
- No CTA, no progress bar. Calm waiting.

### 03 · Onboarding — Welcome
- Ariana's name + "Welcome to your 28 days." — Cormorant italic 32px
- 3–4 lines of body copy (what the programme is)
- "Begin" primary CTA
- "What to expect" ghost button (opens a brief info sheet)

### 04 · Onboarding — Pillar selection
- "What matters most to you right now?" — section heading
- Soft intro line in body
- 10 pillar chips in 2-column grid
- Each chip: pillar name + 1-line descriptor
- "Choose 1–3" rule shown as soft caption
- Selected chips animate to accent
- "Continue" CTA activates when ≥1 selected

### 05 · Onboarding — Start date
- "When would you like to begin?" — heading
- Today (highlighted) + next 7 days shown as day chips
- "Begin today" pre-selected
- "Continue" CTA

### 06 · Today (main hub)
- **Greeting** — Cormorant italic 28px: "Good morning, [name]."
- **Date + day counter** — Inter 500 12px uppercase: "WEDNESDAY · DAY 7 OF 28"
- **Phase badge** — "A · AWARENESS" sage chip
- **Today's lesson card** — large glass card:
  - Day number eyebrow
  - Lesson title in Cormorant 24px
  - Duration + "Begin today's practice" CTA
- **Daily check-in** — 3-emoji row (mood / energy / intention). Optional, 1-tap.
- **Wisdom card of the day** — compact, expandable
- **Bottom nav**

### 07 · Lesson player
- Full-bleed environment behind
- Video player in upper 55% (Vimeo embed)
- Lesson title below in Cormorant 22px
- Phase badge
- 4-step progress dots (Lesson active)
- "Continue to Reflect →" CTA when video finishes
- Back chevron top left

### 08 · Reflect
- Step indicator (step 2 active)
- "Take a moment." — Cormorant italic 28px
- Reflect prompt text — Inter 15px
- Text area: glass card, placeholder text soft, min 120px
- "Save & continue" CTA (enabled once text entered)
- "Skip for now" ghost link (small, below CTA)

### 09 · Act
- Step indicator (step 3 active)
- "Your practice today." — Cormorant italic 28px
- Action prompt — Inter 15px, slightly larger than body
- Large checkbox (40×40) with label "I completed this"
- "Continue" CTA

### 10 · Observe
- Step indicator (step 4 active)
- "What did you notice?" — Cormorant italic 28px
- Observe prompt — Inter 15px
- Text area (optional — "Skip for now" always visible)
- "Complete day [N]" primary CTA

### 11 · Day complete
- Full bleed — environment glows slightly warmer
- HMA mark (small, centred)
- "Day [N] complete." — Cormorant 36px
- One-line reflection quote from the day's lesson — italic soft
- "The work continues in your life." — Inter 13px uppercase spaced, very soft
- "Return home" ghost button after 2s delay
- No confetti. No streak count. Quiet.

### 12 · Journey (28-day progress)
- "Your 28 days." — Cormorant 28px
- Phase arc — 4-section ring, current phase highlighted
- 28-day grid — 4 rows × 7 days
  - Completed: filled accent circle
  - Today: glowing ring
  - Future: empty faint circle
  - Phase breaks: slight vertical gap between weeks
- Tap a completed day: mini card — lesson title + whether reflect+act done
- Phase legend below grid

### 13 · Library (Phase 2 screen)
- "Wisdom & practice." — Cormorant 28px
- Two section cards: Wisdom library · Meditation & breathwork
- Each card: title, count, description, "Explore →" CTA
- In MVP: soft "Coming soon" label, no interaction

### 14 · Profile
- Name in Cormorant 24px
- Pillars selected — chips (read-only)
- Programme start date
- "Edit pillars" link
- Notifications setting toggle
- Sign out (ghost, bottom)
- Delete account (small red text link, very bottom)

---

## Motion & transitions

**Screen transitions:** 280ms ease-in-out horizontal slide. No bounces.
**Step transitions** (lesson → reflect → act): 220ms vertical slide up.
**Day complete entrance:** 400ms fade-up with gentle scale 0.96→1.
**Environment crossfade:** 2000ms linear when time window changes mid-session.
**Card press:** 100ms scale 0.98. Release: 150ms spring back.
**Check-in emoji:** 200ms pop scale on select.
**Checkbox complete:** 300ms fill animation + subtle haptic.

**Rule:** `prefers-reduced-motion` collapses all transitions to opacity fade ≤150ms.

---

## Accessibility

- All text meets WCAG AA contrast in all 4 environments
- Touch targets minimum 44×44px
- Focus rings: 2px `var(--env-accent)` offset 2px
- All interactive elements have `aria-label`
- Journal text areas have `aria-describedby` pointing to the prompt
- Video player has captions track (required before launch)
- Meditation audio has transcript link
- No colour as the sole indicator of meaning

---

## What this is NOT

- No gamification (no XP, coins, badges, leaderboards)
- No streak counters or shame mechanics
- No social feed or public activity
- No push-to-share any personal reflection
- No dark-mode toggle — environments replace it
- No loading spinners — skeleton screens in environment colour only
