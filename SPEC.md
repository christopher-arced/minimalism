# Religious App — Product Spec

## Overview

A multi-faith, fully pluralistic spiritual reflection app. No primary tradition is assumed. The app serves users across faiths through a daily prompt + journaling loop, powered by AI-adapted content from a curated public domain corpus. Pure user-app interaction — no scholars, no community layer.

---

## Core Loop

1. User opens the app to a single full-screen daily prompt card (verse + reflection question)
2. User reflects and writes in the journal
3. Journal entry is encrypted client-side and never leaves the device

The home screen shows one card only — nothing else competes for attention.

---

## Content Pipeline

### Corpus
- Public domain texts only (e.g. Project Gutenberg, sacred-texts.com)
- Fixed set ingested at launch, expanded manually on a quarterly basis
- English and Spanish corpora curated separately

### AI Content Adaptation
- AI is retrieval-grounded — it never free-generates religious claims
- AI adapts tone (meditative, conversational) on top of verbatim source text; source is always cited
- Guardrails: retrieval-grounding + strict prompt engineering + user flagging with auto-rollback threshold + acceptance of residual risk

### Reflection Questions
- Human-written queue: AI drafts candidates, human editors refine and approve
- Free tier: shared daily question (same for all users on a given day)
- Premium tier: AI-personalized question (see Personalization)

### Content Tagging
- Controlled vocabulary of themes (e.g. silence, devotion, community, justice) defined by internal editorial
- AI auto-tags content against the fixed vocabulary; human editor confirms before publish

---

## Personalization

### Cold Start (Onboarding)
- 3–5 screens, short and secular-feeling (not a religion picker)
- Users select spiritual themes (e.g. silence, community, grief, gratitude) as interests
- Onboarding quietly forks the experience into different content mode defaults

### Tradition Rotation
- Users set a weighted slider rotation across traditions (e.g. Christianity 50%, Buddhism 30%, Sufism 20%)
- Hard cap: up to 3 traditions recommended before the experience becomes noise
- Daily prompt is drawn from the tradition whose weight wins that day's weighted random draw

### AI Adaptation Signals (Premium)
- Tradition rotation weights and theme preferences
- Engagement patterns (cards tapped, lingered on, dismissed)
- Explicit prompt ratings ("meaningful" / "not for me")
- **Never**: journal content (zero-knowledge — server never sees it)

### Timing Adaptation
- AI infers when the user is most receptive using behavioral metadata (open times, session length)
- Runs on behavioral signals only; no content inference

---

## Journal

- Zero-knowledge: entries encrypted client-side before any transmission
- Ephemeral by design — if the user loses their device, entries are gone. This is intentional ("like a prayer said aloud")
- No recovery path, seed phrase, or backup
- Journaling works fully offline (React Native local storage + encryption)
- Safety intervention: out of scope. A persistent, unobtrusive "need support?" link points to crisis resources

---

## Subscriptions

**Free tier**
- Daily prompt with shared human-written reflection question
- Up to 2 traditions in weighted rotation
- Opt-in streaks and history (private, never shared)

**Premium tier (tradition-specific)**
- AI-personalized reflection questions based on full signal set
- Weighted slider control and up to 3+ traditions in rotation
- Deeper tradition content (commentaries, practice context)

No ads. No paywalling of canonical texts.

---

## Gamification

- Off by default
- Users can opt in to streaks and personal stats
- All data is private — never surfaced to others, never ranked

---

## Notifications

- Standard push notifications (screen time APIs are not used)
- Two copy strategies, rotated:
  - Theme-based: "Today's reflection is about silence."
  - Randomized contemplative phrases from a human-written bank
- Users set their own notification time during onboarding

---

## Tech Stack

- **Platform**: React Native or Flutter
- **Offline**: Journal works fully offline; content feed requires a connection
- **AI model**: Claude (Anthropic) — fixed choice at launch, API-based
- **Languages**: English and Spanish at launch
- **Localization note**: RTL support is deferred (Arabic/Hebrew traditions are post-launch)

---

## Go-to-Market

Three primary beachhead audiences:

1. **Spiritual-but-not-religious millennials ("nones")** — left organized religion, still crave transcendence. Discovery via lifestyle/wellness social content.
2. **Devout practitioners** — already religious, frustrated by existing apps being too shallow or too denominationally narrow. Reached through faith communities.
3. **Bilingual Latino Catholics** — served by English+Spanish launch, culturally specific content depth. Reachable and sizable initial market.

The common value proposition across all three: **curiosity and intentional reflection**, not doctrine.

---

## App Store Strategy

- Establish contact with an Apple rep early to get soft approval on concept before investing in build
- Internal content policy (no proselytizing, no exclusionary doctrinal claims) enforced at the human editor step

---

## Open Tensions

- **AI personalization quality will be uneven across traditions** — Claude has significantly stronger training signal on Christianity and major world religions than on minority or indigenous traditions. Premium users in underrepresented traditions will get weaker personalization.
- **Opt-in gamification discoverability** — it's off by default, but the UX path for users to discover and enable it needs to be defined.
- **Spanish corpus quality** — not all public domain texts have high-quality Spanish versions; curation effort is non-trivial.
