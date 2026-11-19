# HMA Online Programme — Development Plan & Backlog
**Human Mastery Architecture · Digital Platform**
Last updated: 2026-11-19 · Owner: MetaTec R&D

---

## Vision recap

> *Less time on the platform. Greater transformation in life.*

A luxury digital sanctuary immersed in real nature — time-aware, personalised, and grounded in Ariana's proprietary 28-day ARCH™ methodology. The platform integrates the four things no competitor has combined: Lifebook's whole-life philosophy, GrowthDay's daily rhythm, Mindvalley's immersive learning, and Waking Up's wisdom and meditation depth.

---

## Tech stack decision

| Layer | MVP (Phase 1) | Full product (Phase 3+) |
|---|---|---|
| **Frontend** | React + Vite (PWA, mobile-first) | Native iOS (SwiftUI) + Android (Kotlin) |
| **Auth** | Firebase Auth (Google Sign-In + email) | Same + Apple Sign-In (required for iOS) |
| **Database** | Firestore | Firestore |
| **Storage** | Firebase Storage (audio/video refs) | Firebase Storage + CDN |
| **Video/audio** | Vimeo embed (Ariana records, uploads to Vimeo) | Vimeo + native HLS player |
| **Hosting** | Firebase Hosting | Firebase Hosting (web) + App Store |
| **Admin** | Simple React admin panel | Full advisor dashboard |
| **Firebase project** | New: `hma-programme` (separate from `hmasystem-47c7b`) | Same |

**Rationale:** Web PWA ships in 6–8 weeks. Ariana can start her first cohort while native apps are built in parallel. Everything runs on infrastructure already familiar to the team.

---

## Phases overview

| Phase | Name | Duration | Goal |
|---|---|---|---|
| **0** | Foundation | 2 weeks | Architecture, design system, content schema |
| **1** | MVP — First Cohort | 6–8 weeks | Ariana can run 5–10 paying participants |
| **2** | Content Library | 4–6 weeks | Wisdom library, meditation/breathwork, rituals |
| **3** | Immersive Environment | 4–6 weeks | Time-aware UI, nature soundscapes, luxury experience |
| **4** | Advisory Integration | 3–4 weeks | Session booking, session-linked unlocks, advisor portal v2 |
| **5** | Native Apps | 6–10 weeks | iOS SwiftUI + Android |
| **6** | Advanced Platform | Ongoing | AI layer, alumni community, post-28-day, analytics |

---

---

# PHASE 0 — Foundation
**Duration:** 2 weeks · **Goal:** Everything in place before a line of product code is written

## Epics

### F-1 · Architecture & Decisions

| ID | Feature / Story | Priority | Effort | Notes |
|---|---|---|---|---|
| F-1-01 | Decide: web PWA first vs native iOS first | P0 | XS | Recommendation = PWA first (ship in weeks, not months) |
| F-1-02 | Create new Firebase project `hma-programme` | P0 | XS | Separate from `hmasystem-47c7b` (marketing site) |
| F-1-03 | Define Firestore data model (users, days, entries, pillars, progress) | P0 | M | Schema drives everything downstream |
| F-1-04 | Define Firestore security rules (participant data is private; advisor can read own participants only) | P0 | M | No cross-participant data leakage |
| F-1-05 | Set up Firebase Storage bucket structure (`/lessons/`, `/audio/`, `/images/`) | P0 | S | |
| F-1-06 | Set up dev + staging + prod Firebase environments | P0 | S | |
| F-1-07 | Set up GitHub repo `SARIFIAAR/hma-programme` with branch strategy | P0 | XS | main = prod, dev branch, feature branches |

### F-2 · Design System

| ID | Feature / Story | Priority | Effort | Notes |
|---|---|---|---|---|
| F-2-01 | Extend HMA brand tokens into app design system (CSS custom props / Tailwind theme) | P0 | M | Use existing atelier palette as base; add dawn/day/dusk/night token sets |
| F-2-02 | Define the 4 time-aware colour environments (tokens only — implementation in Phase 3) | P0 | S | Dawn, Day, Dusk, Night — capture in `tokens.json` |
| F-2-03 | Typography setup (Cormorant Garamond + Inter, same as marketing site) | P0 | XS | |
| F-2-04 | Icon set selection (Phosphor or Lucide — clean, minimal, works in both light and dark) | P0 | XS | |
| F-2-05 | Component sketch: Today view, Day card, Journal entry, Progress arc | P0 | M | Wireframe-level only — align with Ariana before building |

### F-3 · Content Schema

| ID | Feature / Story | Priority | Effort | Notes |
|---|---|---|---|---|
| F-3-01 | Define lesson schema (day #, phase, title, videoUrl, reflectPrompt, actPrompt, observePrompt, pillarsTagged[]) | P0 | S | |
| F-3-02 | Define wisdom card schema (tradition, theme, quote, attribution, reflection, pillarsTagged[]) | P0 | S | |
| F-3-03 | Define meditation schema (title, intention, duration, audioUrl, type: guided/unguided/breathwork) | P0 | S | |
| F-3-04 | Define pillar schema (id, name, description, colour, icon) | P0 | XS | 10 pillars from programme blueprint |
| F-3-05 | Seed Firestore with 28-day lesson structure (titles + phases, no content yet — placeholders) | P0 | S | Gives Ariana a template to record against |
| F-3-06 | Seed all 10 pillar definitions | P0 | XS | |

---

---

# PHASE 1 — MVP: First Cohort
**Duration:** 6–8 weeks · **Goal:** Ariana can invite her first 5–10 paying participants and run a full 28-day cohort end-to-end

**What MVP includes:** Auth · Onboarding · Daily experience core (lesson + reflect + act + observe) · 28-day progress view · Basic admin for Ariana
**What MVP excludes:** Wisdom library · Meditation library · Time-aware environments · Sounds · 1:1 booking · Native apps

---

## Epic MVP-1 · Authentication & Access

| ID | Feature / Story | Priority | Effort | Notes |
|---|---|---|---|---|
| MVP-1-01 | Sign in with Google (Firebase Auth) | P0 | S | |
| MVP-1-02 | Sign in with email/password | P0 | S | For participants without Google accounts |
| MVP-1-03 | Invite-only access gate — only accounts in `hmaParticipants/{email}` can access the app | P0 | M | Ariana adds emails; random signups land on a waitlist screen |
| MVP-1-04 | Waitlist / access-pending screen (friendly, on-brand) | P0 | S | "Your place is being confirmed. Ariana will be in touch." |
| MVP-1-05 | Sign out | P0 | XS | |
| MVP-1-06 | Delete my account + data (GDPR) | P1 | M | Required before any real users |
| MVP-1-07 | Password reset flow | P1 | S | |

## Epic MVP-2 · Onboarding Flow

| ID | Feature / Story | Priority | Effort | Notes |
|---|---|---|---|---|
| MVP-2-01 | Welcome screen — Ariana's voice, what to expect in 28 days | P0 | S | Simple copy + brand visuals, no cinematic yet |
| MVP-2-02 | Pillar selection screen — choose 1–3 from the 10 pillars | P0 | M | Cards with name, short description, icon; selection persists to profile |
| MVP-2-03 | Programme start date selection — "begin today" or choose a date up to 7 days ahead | P0 | S | Drives which day number the participant is on |
| MVP-2-04 | Name / preferred name entry | P0 | XS | Used in greetings ("Good morning, [name]") |
| MVP-2-05 | Notification permission request (with reason explained) | P1 | S | Web push for PWA; explain what notifications are for |
| MVP-2-06 | Onboarding can be re-entered to change pillars at any time | P1 | S | Per blueprint: "can change at any time" |

## Epic MVP-3 · Daily Experience Core

| ID | Feature / Story | Priority | Effort | Notes |
|---|---|---|---|---|
| MVP-3-01 | Today view — greeting ("Good morning, [name]"), current day, current ARCH phase | P0 | M | Time-aware greeting text only (not visual environment yet) |
| MVP-3-02 | Today's lesson card — title, phase, estimated time | P0 | S | Tappable to enter the day's experience |
| MVP-3-03 | Lesson player — embedded Vimeo player + lesson title + ARCH phase | P0 | M | Vimeo used because Ariana records and uploads videos herself |
| MVP-3-04 | Reflect step — daily prompt displayed, free-text journal entry, save | P0 | M | Private to participant; end-to-end encrypted at rest |
| MVP-3-05 | Act step — action prompt displayed, checkbox to mark complete | P0 | S | Simple checkbox; no gamification |
| MVP-3-06 | Observe step — optional short reflection on the action | P0 | S | Optional; "skip for now" is fine |
| MVP-3-07 | Day complete state — quiet affirmation, no badge or streak pressure | P0 | S | On-brand: "Day [N] complete. The work continues in your life." |
| MVP-3-08 | Day locked state — future days are not accessible until their day arrives | P0 | S | Day N unlocks on Day N of participant's programme |
| MVP-3-09 | Day missed / catch-up — if participant missed a day, the day is available but doesn't auto-advance | P1 | M | No guilt; no forced skip |
| MVP-3-10 | Resume mid-day — if lesson was started but not completed, resume from last step | P1 | M | Persist progress per day in Firestore |
| MVP-3-11 | ARCH phase header — visual label showing which phase the participant is in (A/R/C/H) | P0 | S | Phase changes at days 1, 8, 15, 22 |

## Epic MVP-4 · 28-Day Progress View

| ID | Feature / Story | Priority | Effort | Notes |
|---|---|---|---|---|
| MVP-4-01 | Programme calendar — 28-day grid, completed days marked, today highlighted, future days muted | P0 | M | No streak counter; show completion not consistency pressure |
| MVP-4-02 | ARCH phase arc — visual indicator of which of the 4 phases is active, days remaining in phase | P0 | S | |
| MVP-4-03 | Pillar progress — simple indicator showing which pillars have been covered so far | P1 | M | |
| MVP-4-04 | Journal history — read back past reflect + observe entries by day | P1 | M | Private; participant-only |
| MVP-4-05 | Programme complete screen — Day 28 done: quiet, premium celebration | P0 | S | No confetti; "The 28 days are behind you. What you built lives ahead." |

## Epic MVP-5 · Navigation & Shell

| ID | Feature / Story | Priority | Effort | Notes |
|---|---|---|---|---|
| MVP-5-01 | App shell — bottom navigation: Today · Journey (progress) · Library (placeholder) · Profile | P0 | M | Library is locked/greyed in MVP |
| MVP-5-02 | Profile screen — name, pillars selected, programme start date, sign out, delete account | P0 | S | |
| MVP-5-03 | Offline state — graceful message if no connectivity; journal entries queue for sync | P1 | M | Critical for trust with premium users |
| MVP-5-04 | PWA install prompt — "Add to Home Screen" prompt at appropriate moment | P1 | S | Improves mobile UX significantly |
| MVP-5-05 | App icon + splash screen (PWA manifest) | P0 | S | Use HMA mark |

## Epic MVP-6 · Admin Panel (Ariana)

| ID | Feature / Story | Priority | Effort | Notes |
|---|---|---|---|---|
| MVP-6-01 | Ariana's admin login (Firebase Auth, separate from participant auth) | P0 | S | Same auth system, different role |
| MVP-6-02 | Participant list — name, email, start date, current day, completion % | P0 | M | |
| MVP-6-03 | Add / remove participants (by email) | P0 | S | |
| MVP-6-04 | Lesson management — view all 28 lessons, add/update Vimeo video URL per day | P0 | M | Ariana uploads video to Vimeo, pastes URL here |
| MVP-6-05 | Lesson content editor — edit reflect/act/observe prompts per day | P0 | M | Rich text or simple text field per step |
| MVP-6-06 | Participant progress view — see which days a specific participant has completed | P1 | S | Useful for 1:1 session prep |

## Epic MVP-7 · Infrastructure & Security

| ID | Feature / Story | Priority | Effort | Notes |
|---|---|---|---|---|
| MVP-7-01 | Firestore security rules — participants read/write own data only; advisor reads all in their cohort | P0 | M | No cross-participant leakage |
| MVP-7-02 | Firebase Storage security rules — lesson video refs are authenticated-read only | P0 | S | |
| MVP-7-03 | Privacy policy + terms of service pages (linked from app) | P0 | M | Required before first real user |
| MVP-7-04 | Journal entries encrypted at rest (Firestore field-level encryption or note in privacy policy) | P1 | L | High bar for private reflection data |
| MVP-7-05 | Firebase Hosting deploy pipeline (GitHub Actions → dev + prod) | P0 | M | |
| MVP-7-06 | Error tracking (Sentry or Firebase Crashlytics) | P1 | S | |
| MVP-7-07 | Analytics (Firebase Analytics — no PII, page views + step completion rates only) | P1 | S | |

---

---

# PHASE 2 — Content Library
**Duration:** 4–6 weeks · **Goal:** The wisdom, meditation, and ritual layers are live; content personalises to selected pillars

---

## Epic LIB-1 · Wisdom Library

| ID | Feature / Story | Priority | Effort | Notes |
|---|---|---|---|---|
| LIB-1-01 | Wisdom card data model — seed first 50 cards across 6 traditions + 8 themes | P0 | L | Bible, Stoicism, Buddhism, Taoism, Shaolin/Zen, Islam — per blueprint |
| LIB-1-02 | Daily wisdom card on Today view — one card surfaced daily, pillar-weighted | P0 | M | Rotates; different each day |
| LIB-1-03 | Wisdom library screen — browse by tradition or by theme | P0 | M | Filter chips: Tradition · Theme |
| LIB-1-04 | Wisdom card detail — full quote, attribution, interpretation, reflection prompt | P0 | S | |
| LIB-1-05 | Save wisdom card to favourites | P1 | S | Saved to participant profile in Firestore |
| LIB-1-06 | Pillar-weighted surfacing — wisdom cards tagged to pillars; selected pillars increase weight | P1 | M | Soft weighting, not hard filter |
| LIB-1-07 | Admin: add wisdom cards (tradition, theme, quote, attribution, reflection, pillars) | P0 | M | Ariana or content team can add cards |

## Epic LIB-2 · Meditation & Breathwork Library

| ID | Feature / Story | Priority | Effort | Notes |
|---|---|---|---|---|
| LIB-2-01 | Meditation schema seed — first 20 audio tracks across 8 intentions | P0 | L | Intentions: abundance/vision · presence/joy · fear/anxiety · confidence · love/connection · spiritual · physical relaxation · sleep/recovery |
| LIB-2-02 | Meditation library screen — browse by intention (cards with intention name + duration) | P0 | M | No tradition filter at this stage |
| LIB-2-03 | Audio player — play/pause, scrub, volume, background audio support | P0 | L | Must keep playing when screen locks (PWA limitation — handle gracefully) |
| LIB-2-04 | Meditation detail — title, intention, duration, type (guided/unguided/breathwork), save/favourite | P0 | S | |
| LIB-2-05 | Breathwork timer — simple configurable timer (inhale/hold/exhale counts) | P1 | M | For unguided breathwork tracks |
| LIB-2-06 | Safety note on breathwork cards ("Not a medical treatment. Stop if uncomfortable.") | P0 | XS | Non-negotiable per programme rules |
| LIB-2-07 | Pillar-surfaced meditation suggestion — "Based on your pillars, you might try…" | P1 | M | |
| LIB-2-08 | Admin: upload meditation audio files to Firebase Storage, create library entries | P0 | M | |

## Epic LIB-3 · Daily Rituals

| ID | Feature / Story | Priority | Effort | Notes |
|---|---|---|---|---|
| LIB-3-01 | Morning Arrival ritual — intention, breath, wisdom card, vision reminder | P0 | M | Triggered by time (5–6am) or manual |
| LIB-3-02 | Afternoon Reset ritual — mindful eating prompt, hydration, movement, return to present | P1 | S | |
| LIB-3-03 | Evening Return ritual — gratitude, brief journal, relaxation, tomorrow's intention | P0 | M | |
| LIB-3-04 | Ritual notification settings — per ritual: on/off, time, quiet hours | P1 | M | No guilt; full opt-in |
| LIB-3-05 | Ritual screen — 3 ritual cards, each launches its own micro-flow | P0 | M | Separate from the main daily lesson |
| LIB-3-06 | Ritual completion — quiet confirmation, no streaks | P0 | XS | |

## Epic LIB-4 · Pillar Personalisation Engine

| ID | Feature / Story | Priority | Effort | Notes |
|---|---|---|---|---|
| LIB-4-01 | Daily check-in (60-second) — mood/energy/intention on Today view | P0 | M | 3 emoji sliders; feeds adaptive weighting |
| LIB-4-02 | Check-in visibly adjusts content — wisdom card pool and meditation suggestion shift based on check-in | P1 | M | "You feel low energy → surface a physical vitality or presence wisdom card" |
| LIB-4-03 | Pillar badge on content — all library content shows which pillar(s) it relates to | P1 | S | Small coloured dot or label |

---

---

# PHASE 3 — Immersive Environment
**Duration:** 4–6 weeks · **Goal:** The luxury digital sanctuary is fully realised — time-aware, nature-sound, cinematic

---

## Epic ENV-1 · Time-Aware Visual Environments

| ID | Feature / Story | Priority | Effort | Notes |
|---|---|---|---|---|
| ENV-1-01 | Detect device time and map to environment: Dawn (4–8am), Day (8am–5pm), Dusk (5–8pm), Night (8pm–4am) | P0 | S | |
| ENV-1-02 | Dawn environment — mist, rising amber light, soft green; warm light palette | P0 | L | CSS theme token swap + background texture/image |
| ENV-1-03 | Day environment — sunlit trees, warm stone, clear water; bright, grounded | P0 | L | |
| ENV-1-04 | Dusk environment — bronze light, glowing horizon, reflective water | P0 | L | |
| ENV-1-05 | Night environment — deep pine, moon, stars, firelight, near-black | P0 | L | |
| ENV-1-06 | Smooth environment transition — 2-second crossfade when time window changes mid-session | P1 | M | |
| ENV-1-07 | Manual environment override — participant can lock to any environment | P1 | S | Preference saved to profile |
| ENV-1-08 | Environment respects reduced-motion system preference | P0 | XS | Accessibility non-negotiable |

## Epic ENV-2 · Nature Soundscapes

| ID | Feature / Story | Priority | Effort | Notes |
|---|---|---|---|---|
| ENV-2-01 | Audio OFF by default — sounds never autoplay | P0 | XS | Non-negotiable per programme rules |
| ENV-2-02 | Nature sound layer — ambient audio per environment (birds, breeze, water, fire, rain, insects) | P0 | M | Separate Web Audio toggle from meditation audio |
| ENV-2-03 | Sound layer controls — master toggle, volume dial | P0 | S | |
| ENV-2-04 | Individual sound layer toggles — birds on/off, water on/off, etc. | P1 | M | |
| ENV-2-05 | Sounds respect device silent mode | P0 | S | |
| ENV-2-06 | Sound fades when switching to meditation audio (duck/crossfade) | P1 | M | |

## Epic ENV-3 · Optional Binaural Audio

| ID | Feature / Story | Priority | Effort | Notes |
|---|---|---|---|---|
| ENV-3-01 | Binaural audio layer — available as a toggle within meditation/ambient audio | P1 | M | |
| ENV-3-02 | Binaural tracks labelled as "listening preference, not proven treatment" | P0 | XS | Non-negotiable disclaimer per programme rules |
| ENV-3-03 | Recommend headphones prompt when binaural is enabled | P0 | XS | |
| ENV-3-04 | Normal ambient alternative always offered alongside binaural | P0 | S | |

## Epic ENV-4 · Cinematic Transitions

| ID | Feature / Story | Priority | Effort | Notes |
|---|---|---|---|---|
| ENV-4-01 | App entrance animation — calm fade-in, no blocking splash | P0 | S | 0–3s max; skip-able |
| ENV-4-02 | Optional arrival cinematic (3–8s) — nature reveal for the environment | P1 | L | Modelled on film7/film8 from marketing site; skip button always visible |
| ENV-4-03 | Day complete transition — gentle ambient animation, not a celebration | P0 | S | |
| ENV-4-04 | Lesson-to-reflect step transition — breathing space between content and reflection | P0 | S | |
| ENV-4-05 | Motion respects `prefers-reduced-motion` | P0 | XS | |

---

---

# PHASE 4 — Advisory Integration
**Duration:** 3–4 weeks · **Goal:** The optional 1:1 advisory tier is fully integrated — session booking, session-linked content, advisor view

---

## Epic ADV-1 · Session Booking

| ID | Feature / Story | Priority | Effort | Notes |
|---|---|---|---|---|
| ADV-1-01 | Calendly embed (or native booking) for 90-min session booking | P0 | M | Calendly is fastest path; native booking is Phase 5+ |
| ADV-1-02 | Session calendar on participant profile — upcoming and past sessions | P0 | S | |
| ADV-1-03 | Pre-session brief — participant prompted to note what they want to bring | P1 | S | Saved to Firestore; Ariana can read it |
| ADV-1-04 | Post-session reflection — prompted within 24 hours of a completed session | P1 | S | |
| ADV-1-05 | 8-session tracker — progress bar showing sessions 1/8 through 8/8 | P0 | S | |

## Epic ADV-2 · Session-Linked Content Unlocks

| ID | Feature / Story | Priority | Effort | Notes |
|---|---|---|---|---|
| ADV-2-01 | Mark session as confirmed (Ariana action in admin) | P0 | S | Triggers content unlock |
| ADV-2-02 | Session-linked days — certain days unlock only after the linked session is confirmed | P1 | M | For premium advisory tier only |
| ADV-2-03 | Standalone participants bypass session locks — they progress by day independently | P0 | XS | Two-tier model: online-only vs online+advisory |

## Epic ADV-3 · Advisor Portal v2

| ID | Feature / Story | Priority | Effort | Notes |
|---|---|---|---|---|
| ADV-3-01 | Full participant dashboard — name, start date, day, pillars, check-in trend | P0 | M | Upgrade of MVP-6 |
| ADV-3-02 | Participant journal entries — read-only access to reflect + observe entries (participant-consented) | P1 | M | Consent gate: "Allow Ariana to read your journal to personalise sessions?" |
| ADV-3-03 | Per-participant notes (Ariana's private notes — participants cannot see) | P0 | M | |
| ADV-3-04 | Session history per participant | P0 | S | |
| ADV-3-05 | Content assignment — assign specific wisdom cards or meditations to a participant | P1 | M | |

---

---

# PHASE 5 — Native Apps
**Duration:** 6–10 weeks · **Goal:** Proper native iOS app on the App Store; Android to follow

---

## Epic NAT-1 · iOS App (SwiftUI)

| ID | Feature / Story | Priority | Effort | Notes |
|---|---|---|---|---|
| NAT-1-01 | SwiftUI port of full web app feature set (Phases 1–4) | P0 | XL | Feature parity with web |
| NAT-1-02 | Apple Sign-In (required for App Store with social login) | P0 | M | |
| NAT-1-03 | Native audio player with background playback (AVFoundation) | P0 | L | Proper lock-screen controls |
| NAT-1-04 | Push notifications (APNs via Firebase Cloud Messaging) | P0 | M | Ritual reminders |
| NAT-1-05 | Native time-aware environments with live UIKit/SwiftUI theming | P0 | L | |
| NAT-1-06 | HealthKit opt-in — optional mood/energy correlation with sleep/HRV | P2 | L | Phase 6 candidate |
| NAT-1-07 | App Store submission — privacy labels, medical declaration (not SaMD), screenshots | P0 | M | |
| NAT-1-08 | Apple Watch companion — today's wisdom card + day status glanceable complication | P2 | L | |

## Epic NAT-2 · Android App (Kotlin)

| ID | Feature / Story | Priority | Effort | Notes |
|---|---|---|---|---|
| NAT-2-01 | Kotlin/Jetpack Compose port | P1 | XL | After iOS ships |
| NAT-2-02 | Google Sign-In + biometric auth | P1 | M | |
| NAT-2-03 | Health Connect integration (optional) | P2 | L | |
| NAT-2-04 | Play Store submission — data safety form | P1 | M | |

---

---

# PHASE 6 — Advanced Platform
**Duration:** Ongoing · **Goal:** Competitive moat deepens — AI layer, community, post-programme, outcome data

---

## Epic ADV-AI · "Ask Ariana" AI Layer

| ID | Feature / Story | Priority | Effort | Notes |
|---|---|---|---|---|
| ADV-AI-01 | AI assistant trained on Ariana's voice, frameworks, and ARCH methodology | P1 | XL | Claude API + Ariana's transcribed sessions as training corpus |
| ADV-AI-02 | Available between sessions — text + voice input | P1 | L | Bridges the 2am gap |
| ADV-AI-03 | AI never replaces Ariana's judgement — escalation to Ariana for sensitive topics | P0 | M | Safety guardrail; always offer "book a session" |
| ADV-AI-04 | AI responses labelled as AI-generated | P0 | XS | Transparency non-negotiable |

## Epic ADV-COM · Alumni Community

| ID | Feature / Story | Priority | Effort | Notes |
|---|---|---|---|---|
| ADV-COM-01 | Private alumni network (Circle or Slack) — invitation after Day 28 complete | P1 | M | No building a social network; use an existing platform |
| ADV-COM-02 | Curated CEO/founder-only membership — Ariana approves members | P1 | S | Exclusivity is the value |
| ADV-COM-03 | Monthly live group session for alumni (Zoom + recording in app) | P1 | M | |

## Epic ADV-SUSTAIN · Post-28-Day Sustainment

| ID | Feature / Story | Priority | Effort | Notes |
|---|---|---|---|---|
| ADV-SUSTAIN-01 | 90-Day Architecture product — post-programme daily micro-habits | P1 | L | Referenced in Day 28 of ARCH curriculum |
| ADV-SUSTAIN-02 | Lifetime wisdom library access tier — ongoing access after programme ends | P1 | M | Revenue: one-time lifetime IAP |
| ADV-SUSTAIN-03 | Programme repeat — restart ARCH with updated pillars | P1 | M | |
| ADV-SUSTAIN-04 | Annual renewal nudge at 90 days post-completion | P1 | S | |

## Epic ADV-DATA · Outcome Analytics

| ID | Feature / Story | Priority | Effort | Notes |
|---|---|---|---|---|
| ADV-DATA-01 | Anonymised outcome report — aggregate mood/energy trends across cohorts | P1 | L | Evidence base for premium pricing defence |
| ADV-DATA-02 | Personal progress report — participant receives a private PDF at Day 28 | P1 | M | Journey map of their 28 days |
| ADV-DATA-03 | Mastery Assessment score — benchmark at start and end of programme | P1 | L | "You moved from 4.2 to 7.8 on Clarity & Decisions" |

---

---

## Backlog summary

| Phase | Items | P0 | P1 | P2 | Est. dev weeks |
|---|---|---|---|---|---|
| **Phase 0** Foundation | 20 | 20 | 0 | 0 | 2 |
| **Phase 1** MVP | 51 | 36 | 15 | 0 | 6–8 |
| **Phase 2** Content Library | 32 | 20 | 12 | 0 | 4–6 |
| **Phase 3** Immersive Env | 25 | 18 | 7 | 0 | 4–6 |
| **Phase 4** Advisory | 18 | 10 | 8 | 0 | 3–4 |
| **Phase 5** Native Apps | 14 | 8 | 4 | 2 | 6–10 |
| **Phase 6** Advanced | 15 | 1 | 13 | 1 | Ongoing |
| **Total** | **175** | **113** | **59** | **3** | **~26–36 weeks** |

## Critical path to first paying cohort

1. Phase 0 complete
2. MVP-1 through MVP-5 complete (participant-facing)
3. MVP-6 complete (Ariana can manage content + participants)
4. MVP-7-01 through MVP-7-05 complete (security + deployment)
5. Privacy policy live
6. Ariana has recorded Days 1–28 videos and uploaded to Vimeo
7. Ariana's email added to admin role
8. First cohort invited → programme begins

**Minimum calendar time:** ~8–10 weeks from Phase 0 start, assuming Ariana records content in parallel.

---

## Open decisions (CEO)

- [ ] Web PWA first vs native iOS first (recommendation: PWA first)
- [ ] Vimeo for video hosting vs self-hosted vs Mux vs Firebase Storage directly
- [ ] Pricing model for MVP cohort (private beta pricing vs full price)
- [ ] Calendly vs build native session booking (recommendation: Calendly for MVP)
- [ ] Journal encryption approach (field-level vs application-level vs "trust Firebase")
- [ ] Repo: new `hma-programme` repo or subfolder of `arianahma/HMA`
