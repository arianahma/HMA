# CLAUDE.md — HMA · The Human Mastery Architecture

Project brain. Load this in every session working in `~/Websites/sites/hma/`.
Knowledge files: `knowledge/hma-online-vision.txt` · `knowledge/hma-online-blueprint.txt`

---

## 1. What this is

**Client:** Ariana Ciuca — private advisor. 13+ years study, 15,000+ hours, 2,000+ pages of research, 200+ clients across Europe, UK, USA, UAE.
**Live domain:** `arianaciuca.com`
**Products:**
1. **Marketing site** (`arianaciuca.com`) — the live brand/enquiry site (this repo)
2. **HMA Online Programme** — private 28-day digital experience (prototype only, not yet built)

**North star:** *HMA does not demand more of an Architect's attention. It repeatedly returns their attention to their life.*

HMA is explicitly NOT therapy, NOT generic coaching, NOT corporate consulting. The Architect already possesses experience, intelligence and capacity.

---

## 2. Brand & Design

### Identity
- **Client ("Architect")** — the person enrolled in the programme
- **Tone** — quiet luxury, private, warm, premium, never flashy, never generic-coaching
- **Never use:** "fix", "heal", "transform", "guru", "coaching", "therapy", invented testimonials, unverified statistics

### Colour system (from Vision PDF)

| Role | Daylight | Night |
|---|---|---|
| Base | Ivory `#F6F2E8` | Midnight `#101E26` |
| Nature | Forest `#183B30` | Pine `#1B3938` |
| Accent | Sage `#A8B9A0` | Moonstone `#B8C8C7` |
| Warmth | Champagne `#D6BE91` | Muted bronze `#AD9068` |
| Text | Ink `#23342F` | Mist `#EDF1EB` |

**Current live site tokens (atelier theme):**

| Token | Value |
|---|---|
| `--accent` | `#9a7b43` |
| `--accent-ink` | `#7c6233` |
| `--bg` | `#f6f1e9` |
| `--surface` | `#fbf8f2` |
| `--ink` | `#211d18` |
| `--ink-soft` | `#5b5248` |
| `--line` | `#ddd2c0` |
| `--font-display` | Cormorant Garamond |
| `--font-body` | Inter |

### Visual motifs
Forest canopy, living leaves, soft wind, birds, water ripples, sunlight, warm firelight, natural stone, distant horizons, clouds, stars and moonlight. Restrained cinematic motion, generous negative space. Avoid fantasy overload, glitter, constant animations, stock-coaching clichés.

### Theme variants
| Name | Mood | Description |
|---|---|---|
| **Botanical Light** | Softer | Ivory, sage, warm gold, organic textures |
| **Architectural Forest** | More masculine | Deep forest, charcoal stone, bronze, strong geometry |
| **Balanced Nature** | Neutral | Neutral green and stone |

Any Architect can choose any theme. Content and outcomes are identical across all three.

---

## 3. The Marketing Site

**Source:** `~/arianahma/` (canonical clone of `arianahma/HMA`)
**Deploy:** `cd ~/arianahma && npx firebase-tools deploy --only hosting --project hmasystem-47c7b`
**CEO must approve every deploy.**
**Push:** always `git push origin main` from `~/arianahma` after any change.

### Page sections (in order)
1. Hero — cinematic selector (3 options)
2. For Whom — audience paragraph + tag pills
3. 01 · The Advisory — what 28 days is
4. 02 · Why it is different — not therapy/coaching/consulting
5. 03 · The Approach — 13+ yrs / 15,000+ hrs / 2,000+ pages / 4 regions
6. 04 · The 28-Day Advisory — 8 × 90-min sessions, 2/week, ∞ direct access
7. 05 · What You Receive — 4 cards
8. 06 · The Experience — "Private. Personal. Intelligent. Human. Premium."
9. 07 · The Online Programme — 10-item list
10. 08 · About Ariana — portrait, 13+ years, 200+ people
11. 09 · Investment — by application, price withheld
12. 10 · Apply — enquiry form → `hello@humanmasteryarchitecture.com`
13. Footer — "Private advisory for founders & leaders · Europe · UK · USA · UAE"

### CMS layer
- **`content.json`** — single source of truth for all text + theme tokens; editable via admin
- **`content-loader.js`** — fetches content.json, sets CSS vars, fills `data-cms` attributes, rebuilds array sections

### Opening cinematic variants
| Selector | File | Type |
|---|---|---|
| Ⅰ · Atmosphere (default) | `film7/` | Dark WebGL — orbiting core + atmosphere shells |
| Ⅱ · Solar | `film6b/` | Dark WebGL — particles → core, dimension-planets |
| Ⅲ · Ivory | `ivory/` | Full-page LIGHT design, no cinematic, champagne palette |
| Ⅳ · Ariana | `ariana/` | Light, man-led hero variant |

### Key files
| File | Purpose |
|---|---|
| `index.html` | Main page, all sections, `data-cms` wired |
| `styles.css` | Design system, CSS custom props, two themes |
| `script.js` | IntersectionObserver, mailto form, footer year |
| `content-loader.js` | CMS: fetch → apply |
| `content.json` | All text + theme tokens |
| `firebase.json` | Hosting config (`cleanUrls: true`) |
| `.firebaserc` | Project: `hmasystem-47c7b` |
| `admin/index.html` | Admin panel |
| `img/ariana.jpg` | Ariana's portrait (§08) |

---

## 4. The Admin Panel (`arianaciuca.com/admin`)

**Auth:** Firebase Google Sign-In
**Content writes:** GitHub Contents API → `arianahma/HMA` repo → `content.json`
**Users:** Firestore `hmaUsers/{email}`
**GitHub config:** Firestore `hmaConfig/main`

### Firebase project
| Key | Value |
|---|---|
| Project ID | `hmasystem-47c7b` |
| Auth domain | `hmasystem-47c7b.firebaseapp.com` |
| API key | `AIzaSyBoHcMQgNVr36tlVOufsR7_EoXEfrvM1ig` |
| App ID | `1:54790202950:web:699c803e86461da1870c47` |
| Measurement ID | `G-9EPK2YH4XF` |

### Firestore security rules
```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    function isEditor() {
      return request.auth != null &&
             exists(/databases/$(database)/documents/hmaUsers/$(request.auth.token.email));
    }
    match /hmaConfig/main { allow read, write: if isEditor(); }
    match /hmaUsers/{email} {
      allow read: if request.auth != null;
      allow write, delete: if isEditor();
    }
  }
}
```

### Adding the first user (bootstrap)
Firestore Console → `hmaUsers` collection → document ID = Google email → field `email` (string). After that, manage from admin → Users section.

### Admin sections
- **Users** — add/remove editors by Google email
- **GitHub Settings** — repo/branch/token (stored in Firestore)
- **14 content sections** — all site text
- **Design & Colours** — CSS tokens + font names

---

## 5. The HMA Online Programme (separate product, not yet built)

**Status: prototype only.** Full-featured front-end demo at `/Users/MetaTec/Downloads/index.html`. Vision + blueprint PDFs extracted to `knowledge/`.

### Framework: ARCH™ Journey

| Phase | Days | Theme |
|---|---|---|
| **A — Awareness** | 1–7 | See yourself clearly |
| **R — Realign** | 8–14 | Remove what creates friction |
| **C — Capacity** | 15–21 | Build the human behind the results |
| **H — Habits** | 22–28 | Bring mastery into everyday life |

### Full 28-day curriculum

**A — Awareness (Days 1–7)**
1. Reality and Life Audit
2. Values and Life Vision
3. Energy and Wellbeing
4. Relationships and Connection
5. Leadership and Work
6. Patterns and Beliefs
7. Personal Architecture™

**R — Realign (Days 8–14)**
8. Conscious Priorities
9. Stress and Emotional Regulation
10. Sleep, Nutrition and Movement
11. Environment and Daily Influences
12. Boundaries and Relationships
13. Identity and Values Alignment
14. Personal Realignment Review

**C — Capacity (Days 15–21)**
15. Focus and Cognitive Capacity
16. Conscious Decision-Making
17. Resilience
18. Presence and Awareness
19. Responding Under Pressure
20. Leadership Capacity
21. Capacity Integration

**H — Habits (Days 22–28)**
22. Morning Architecture
23. Evening Architecture
24. Intentional Habit Systems
25. Accountability and Consistency
26. Personal Metrics
27. Sustainable Life Integration
28. 90-Day Architecture

### Daily experience template (15–20 min)
1. **Discover** — 10–15 min video/audio lesson (Ariana's recording)
2. **Reflect** — meaningful exercise or journal prompt
3. **Act** — one real-world action achievable that day
4. **Observe** — optional tracker check-in + short reflection

### First 60 seconds (login → arrival)
- 0–3 s: HMA mark + calm gradient, no blocking animation
- 3–8 s: Optional cinematic nature reveal (sunlit woodland / moonlit landscape)
- 8–12 s: Time-aware greeting — "Good morning, Architect." / "Welcome back, Architect."
- 12–20 s: Optional 20–40 s grounding breath, or skip to Today's Architecture
- Fast re-entry on return: no forced meditation, no splash, no autoplay audio

### Time-aware environments
| Time | Visual mood |
|---|---|
| Dawn | Mist, rising amber light, birdsong, dew, gentle green movement |
| Day | Sunlit trees, warm stone, clear water, fresh foliage, subtle breeze |
| Dusk | Bronze light, glowing horizon, softer birds, reflective water |
| Night | Deep pine, moon, stars, silhouettes, firelight, crickets |

### Navigation (home screen IA)
Greeting → Today's Architecture → one primary action.
Secondary: Morning Arrival · Afternoon Reset · Evening Return · My Journal · Meditations · Wisdom Cards · My Architecture / Progress

### Personal Pillars (10 — chosen at onboarding)
1. **Mind Mastery** — patterns, beliefs, awareness, emotional regulation
2. **Clarity and Decisions** — focus, discernment, purposeful action
3. **Love and Relationships** — self-connection, family, parenting, intimacy
4. **Joy and Presence** — gratitude, awe, being fully where you are
5. **Physical Vitality** — movement, strength, nourishment, recovery
6. **Body and Emotional Balance** — stress awareness, body signals
7. **Courage and Resilience** — fear, guilt, pressure, uncertainty
8. **Spiritual Connection** — faith, meaning, chosen worldview
9. **Freedom and Abundance** — relationship with money, possibility, choice
10. **Leadership and Legacy** — contribution, influence, human impact

Chosen pillar informs wisdom, meditations, exercises, reminders, progress reflections. Architect can change at any time.

### Daily rituals & notifications
| Ritual | Default time | Content |
|---|---|---|
| **Morning Arrival** | 5–6 a.m. | Intention + breath + wisdom card + vision reminder |
| **Afternoon Reset** | Lunchtime | Mindful eating, hydration, movement, return to present |
| **Evening Return** | Bedtime | Gratitude, brief journal, relaxation, tomorrow's intention |

Notifications: opt-in by ritual, configurable time/theme/frequency/quiet hours. No guilt-based streaks.

### Wisdom library
Sources: Bible/Christianity · Islam · Stoicism · Buddhism · Taoism · Shaolin/Zen · Hinduism · Judaism + others.
Themes: courage · fear/anxiety · love · forgiveness · faith · abundance · gratitude · resilience · purpose · peace.
Card structure: attributed teaching → 1–2 sentence interpretation → reflection prompt. Never paraphrases as direct quotes.

### Meditation & breathwork library
Browse by intention: abundance/vision · presence/joy · fear/anxiety · confidence (interviews, public speaking, first dates) · love/connection · spiritual connection · physical relaxation · sleep/recovery · emotional balance.
Each: title, intention, duration, audio/video, optional soundscape, safety note, save/favourite.
**No medical claims. No unsafe breath-holding.**

### Sound design rules
- Audio OFF by default. Separate toggles: nature ambience / music / guided voice.
- Nature layers: birds, breeze, water, fire, rain, nocturnal insects.
- Binaural tracks: labelled as listening preference, NOT proven treatment. Normal ambient alternative always offered.
- Respect device mute, reduced motion, bandwidth, battery. Never auto-restart.

### Progress & data
- Track: day completed, real-world actions, mood/energy/focus (optional), private reflections.
- Optional: sleep, hydration, movement, nutrition, outdoor light from consented sources.
- Display personal baselines and trends. **No fabricated transformation scores, no diagnostic claims.**
- Private journal entries: not visible to others by default.

### Private advisory tier
- 8 × 90-min 1:1 sessions in 28 days
- Session-linked content unlocks (unlock only after session confirmed by advisor)
- Standalone online learners progress by day independently

### Key product rules (from Vision PDF)
- Separate `arianaciuca.com` (marketing) from authenticated programme access
- Replace Unsplash reference photos with licensed imagery before launch
- Implement secure auth, server-side storage, encrypted journal access, consent + privacy controls
- Wearable data integration: explicit opt-in, clear data access/retention/export/deletion explanation
- Mobile-first, accessible (keyboard nav, captions/transcripts, contrast)

---

## 6. DNS & Hosting

| Layer | Detail |
|---|---|
| Domain | `arianaciuca.com` (registrar: GoDaddy) |
| Hosting | Firebase Hosting · `hmasystem-47c7b` |
| Staging | `https://hmasystem-47c7b.web.app` |
| Analytics | GTM-NB5RJTVV · GA4 `G-9EPK2YH4XF` |

### DNS changes in progress (GoDaddy)

| Action | Type | Value |
|---|---|---|
| ❌ Remove | A | `15.197.148.33` |
| ❌ Remove | A | `3.33.130.190` |
| ✅ Add | A | `199.36.158.100` |
| ✅ Add | TXT | `hosting-site=hmasystem-47c7b` |

---

## 7. Repos

| Repo | Purpose |
|---|---|
| `arianahma/HMA` | **Canonical repo** — all work, commits, and deploys go here. Cloned at `~/arianahma`. |
| `SARIFIAAR/hma-site` | ~~RETIRED~~ — was the old working copy. No longer used. |

GitHub token for API writes (admin panel → content.json): stored in Firestore `hmaConfig/main`. Never hardcode.

---

## 8. Open items

- [ ] DNS cutover in GoDaddy (remove old IPs, add new Firebase IP + TXT)
- [ ] Confirm old `/lander` site at `arianaciuca.com` can be fully replaced
- [ ] Add Ariana's email to Firestore `hmaUsers` so she can self-manage the admin
- [ ] Build the actual HMA Online Programme platform (auth, server storage, lessons)
- [ ] Ariana records 28 video/audio lessons + meditation library + Life Vision film
- [ ] Investment page: confirm whether to show price or keep "by application"
- [ ] Confirm `hello@humanmasteryarchitecture.com` is active, or update enquiry email
- [ ] Licensed photography to replace Unsplash references in programme (pre-launch)

---

## 9. Standing rules

- **CEO approves every deploy** — `npx firebase-tools deploy` only after sign-off
- **No outcome/diagnostic claims** — HMA makes no therapeutic, medical, or diagnostic claims
- **No invented testimonials** — only real quotes approved by Ariana
- **Investment figure withheld** — price discussed privately; never publish without approval
- **Version iterations as separate files** — never overwrite a live option; new filename per iteration
- **Admin content writes → `arianahma/HMA`** via GitHub API — that is the source of truth for content.json
