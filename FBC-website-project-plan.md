# FBC Website — Project Plan

**Project:** A simple website for The Fuquay Business Coalition (FBC)
**Domain:** thefuquaybusinesscoalition.com (claimed through Google Workspace)
**Prepared:** May 24, 2026
**Owner:** Shannon Volpe

---

## 1. The goal in one sentence

Build a simple, on-brand website at thefuquaybusinesscoalition.com that tells visitors what FBC is, shows the meeting calendar, and lets anyone message the group — without becoming another thing you have to babysit every week.

That's the whole job. Three things: **who we are**, **when we meet**, **how to reach us**. Everything in this plan serves those three.

---

## 2. What we're building (scope)

A single-page website with three clear sections, wrapped in FBC's existing brand:

1. **What FBC is** — the mission, the tagline, the short story of the group (Wednesday mornings at The Citadel, BNI-adjacent but warmer and looser), and what a visitor can expect if they show up.
2. **The calendar** — the live FBC Google Calendar embedded right on the page, so meeting dates, Visitors Days, and skip-weeks update automatically without anyone touching the site.
3. **Message us** — a contact form on the page that emails the group at yourneighbor@thefuquaybusinesscoalition.com.

**Explicitly out of scope for v1** (can come later): member directory, login/members-only area, online dues payment, blog, event ticketing, photo galleries. Keeping v1 tight is what makes it shippable and low-maintenance.

---

## 3. Decisions this plan assumes

These reflect the recommended path. Any of them can change — say the word and I'll revise the plan.

| Decision | Direction taken | Why |
|---|---|---|
| **Build & hosting** | Claude hand-builds a static site; host free on Cloudflare Pages; point the domain at it | Full control over FBC branding (logo, colors, fonts, voice), no monthly cost, fast and reliable |
| **Message us** | An on-page contact form that emails FBC | Cleanest experience for a visitor — no "open your email app" friction |
| **Scope** | One scrolling page | Fastest to build, easiest for visitors, least to maintain |
| **Calendar** | Embed the live Google Calendar | Auto-updates; nobody has to re-key meeting dates onto the site |

If you'd rather trade brand control for zero-maintenance simplicity, **Google Sites** (free with Workspace, native calendar embed) is the fallback — noted again in Section 11.

---

## 4. Technical approach (plain-English)

The site is a **static website** — just files (HTML/CSS, a little JavaScript). That makes it fast, cheap, secure, and nearly impossible to "break."

- **Hosting: Cloudflare Pages.** Free tier is more than enough for a group site. It serves the files, gives us HTTPS automatically, and is fast everywhere.
- **Domain: point thefuquaybusinesscoalition.com at Cloudflare.** This is a DNS step. It requires access to wherever the domain is currently registered (see the prerequisite in Section 8 — the registrar is listed as "TBD" in your tracker and we need to pin it down).
- **Calendar: a Google Calendar embed.** Google provides an embed snippet for any calendar set to "public." We drop that into the calendar section. The one setup detail: the calendar's timezone currently shows UTC and should be flipped to Eastern so dates/times read correctly (this is already noted in your master tracker).
- **Contact form: two clean options**, both keep the form on the page and email FBC:
  - **Option A — Cloudflare Pages Function + email API** (e.g., Resend's free tier). Everything lives in one place (Cloudflare). Slightly more setup; one API key to store.
  - **Option B — a form service** (e.g., Formspree free tier). Paste a snippet, point it at the FBC email, done. Least setup; relies on a third party.
  - *Recommendation:* start with **Option B** to ship fast, migrate to Option A later if you want everything under Cloudflare. Either way, we add a spam honeypot so the inbox stays clean.

---

## 5. Page layout (the one-page structure)

Top to bottom, as a visitor scrolls:

1. **Header / hero** — FBC logo, the tagline *"Empowering Growth — Authentic Connections, Collaborations & Accountability,"* and a one-line "what this is." A "Visit a meeting" button that jumps to the calendar.
2. **What FBC is** — the mission (verbatim), a short warm paragraph in FBC's voice, and the practical facts: Wednesday mornings, 9 AM arrival, The Citadel Event Space on Main Street in Fuquay-Varina.
3. **What a Wednesday looks like** — a short, friendly version of the standard agenda so a first-timer knows what they're walking into (hang out, ice breaker + intros, the topic, referrals, community happenings, group business, close on the mission).
4. **Calendar** — the embedded Google Calendar, with a one-liner: "We meet most Wednesdays — here's what's coming up."
5. **Message us** — the contact form (name, email, message) plus the FBC email shown as a fallback.
6. **Footer** — logo mark, location line, FBC email, and a small "© The Fuquay Business Coalition."

---

## 6. Content plan (what the words actually say)

All copy is drawn from your existing materials so the site sounds like FBC, not like a chamber-of-commerce brochure.

- **Mission — always verbatim, no Oxford comma:** *"To empower growth through authentic connections, collaborations and accountability."*
- **Tagline:** *"Empowering Growth — Authentic Connections, Collaborations & Accountability."*
- **Voice:** a friend who runs a tight room — direct, warm, real, founder-energy, short sentences, a little dry humor. Not corporate, not BNI-scripted. (Avoid "synergy / ecosystem / stakeholders / leverage.")
- **Facts to feature:** weekly Wednesday cadence; 9 AM arrival with music and circular seating; The Citadel Event Space, Main Street, Fuquay-Varina, NC; first-timers welcome (especially on Visitors Days).

I'll draft the actual section copy as the first build step and you approve it before it goes live.

---

## 7. Brand application

Everything is already defined in your `fbc-slides` system — the site just reuses it.

| Element | Value | Web note |
|---|---|---|
| Yellow | `#F5C518` | Accents, buttons |
| Navy | `#1F3A6B` | Headers, primary text on light |
| Charcoal | `#4A4A4A` | Body text |
| Cream / paper | `#FFFCF2` | Page background |
| Header font | Georgia | Web-safe — works everywhere as-is |
| Body font | Calibri | Not universal on the web; use Calibri with a clean sans-serif fallback (or load a close web font) |

**Logo:** use the canonical variants in `fbc-slides/assets/logo-variants/` — `fbc-logo-color-400.png` (and the 1600 for retina) on cream/white backgrounds, and `fbc-logo-no-disc-*` if we place it on a yellow band. (Per your README: do **not** use the retired "Copy of FBC Logo" Canva design.) A small future nicety: a true vector (SVG) logo would render crispest on the web — we can auto-trace or rebuild it from the source art if you want it.

---

## 8. Prerequisites — what I need from you before "go live"

These are the things only you can unlock. None are hard; a couple just need a login.

1. **Domain registrar access (the big one).** Your tracker lists the registrar as "TBD — fill in where the domain is registered." Domains claimed via Google Workspace are usually managed through Squarespace (which took over Google Domains) or another registrar. We need to log in there to point DNS at Cloudflare. **First action: confirm where the domain lives.**
2. **Confirm the FBC Google Calendar is set to "public"** (so it can be embedded) and **switch its timezone to Eastern** (currently shows UTC).
3. **Confirm the contact email destination** — defaulting to yourneighbor@thefuquaybusinesscoalition.com unless you'd prefer it route elsewhere.
4. **Pick the contact-form option** (A: Cloudflare-native, or B: form service to start). I recommend B for speed.
5. **A Cloudflare account** (free) to host the Pages project — quick to set up if you don't already have one.

---

## 9. Build phases & milestones

A realistic path from nothing to live. Each phase ends in something you can look at.

**Phase 0 — Setup & access (½ day, mostly yours)**
- Confirm domain registrar and gather logins.
- Create/confirm Cloudflare account.
- Confirm calendar is public + set to Eastern.

**Phase 1 — Content & design draft (1 day)**
- I draft all section copy in FBC's voice for your approval.
- I produce a visual mockup (a working HTML preview you can open) so you see the look before we wire anything up.

**Phase 2 — Build the page (1 day)**
- Build the one-page site with the approved copy and brand styling.
- Wire in the live Google Calendar embed.
- Add the contact form (chosen option) with spam protection.
- Make it look right on phones (most visitors will be on mobile).

**Phase 3 — Test (½ day)**
- Submit the form end-to-end and confirm it lands in the FBC inbox.
- Confirm the calendar shows correct dates/times in Eastern.
- Check on phone, tablet, and desktop; check the links and buttons.

**Phase 4 — Go live (½ day)**
- Deploy to Cloudflare Pages.
- Point thefuquaybusinesscoalition.com at it (DNS) and confirm HTTPS.
- Final once-over on the real domain.

**Total working time:** roughly **3–4 focused days** of build, spread across whenever access pieces land. Realistically a **1–2 week calendar window** depending on how fast the domain/registrar piece comes together.

---

## 10. Ongoing maintenance (deliberately near-zero)

Because the calendar is embedded live, **the part that changes most often — meeting dates — updates itself.** You manage meetings in Google Calendar (as you already do), and the site reflects them automatically.

The static page itself only changes when FBC's *story* changes (new tagline, new meeting location, etc.) — rare, and a quick edit when it happens. Contact-form messages arrive as email; nothing to log into.

---

## 11. Risks & considerations

- **Domain/DNS is the critical path.** Everything else can be built in parallel, but "go live on the real domain" is blocked until we know the registrar and can edit DNS. If that turns into a wall, the **Google Sites fallback** sidesteps most DNS pain (Workspace can map the domain more directly) at the cost of brand control.
- **Overlap with The Citadel website.** Your tracker notes the FBC site overlaps with Citadel website work. Worth a moment's thought: keep them fully separate, cross-link them, or share a template. Doesn't block FBC v1, but good to decide early.
- **Email deliverability.** Whichever form option we use, we'll send a test and confirm messages don't land in spam before launch.
- **Calendar privacy.** Only put on the *public* calendar what's meant to be public (meetings, Visitors Days, socials). Dues, member contact info, and founding dates stay private per your existing public/private rule — the embed only ever shows the public calendar.
- **Font fidelity.** Calibri isn't guaranteed on every visitor's device; we'll set a graceful fallback so body text always looks clean.

---

## 12. Open questions for you

1. Where is the domain registered? (Unblocks go-live.)
2. Contact form: start with the quick form-service option (recommended), or go Cloudflare-native from day one?
3. Anything beyond the three core sections you want in v1 — e.g., a short "How to join" line, member logos, a photo of a meeting?
4. Should the FBC site and The Citadel site cross-link?

---

## 13. Recommended next step

Give me the green light and I'll start **Phase 1**: draft the site copy in FBC's voice and build a visual mockup you can open and react to — before we commit to anything technical. In parallel, the one thing worth chasing down on your side is **where the domain is registered**, since that's the only true blocker to going live.
