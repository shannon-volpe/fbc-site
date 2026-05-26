# The Fuquay Business Coalition — Website Build Plan

A simple, one-page marketing site for **The Fuquay Business Coalition (FBC)**, a weekly
networking group in Fuquay-Varina, NC. Domain: **thefuquaybusinesscoalition.com**
(registered through Google Workspace).

The site does three things: says what FBC is, shows the meeting calendar, and lets a
visitor message the group right from the page.

---

## Status at a glance

**Done**
- Full single-page site built (`index.html`) — content, brand, layout, responsive.
- Building-art background pulled in and washed out ("window reflection" treatment).
- Logo wired in; brand colors and fonts applied.
- Live Google Calendar embed in place.
- Visitor form built with all fields + boldly colorful "art by faejays" credit.

**Remaining**
1. Make the FBC Google Calendar public so the embed displays.
2. Activate form delivery (add a Web3Forms access key) — currently falls back to email.
3. Connect GitHub, push the repo, enable GitHub Pages.
4. Point the domain (DNS) at GitHub Pages and verify the live site.

---

## 1. Brand & voice

| Token | Value |
|---|---|
| Yellow | `#F5C518` |
| Navy | `#1F3A6B` |
| Charcoal | `#4A4A4A` |
| Cream / paper | `#FFFCF2` |
| Heading font | Georgia |
| Body font | Calibri (stack: `Calibri, 'Segoe UI', system-ui, sans-serif`) |
| Display font | **October Owls** (FBC's preferred display font — not web-embeddable / not portable). Web stand-in: **Amarante** (Google Fonts). Swap freely. |

**Mission (always verbatim, no Oxford comma):**
> To empower growth through authentic connections, collaborations and accountability.

**Tagline:** It's as easy as FBC

**Voice:** A friend who runs a tight room. Direct, warm, real, founder-energy. Short
sentences, a little dry humor. Not corporate, not chamber-of-commerce, not BNI-scripted.
Avoid: "synergy," "ecosystem," "stakeholders," "leverage."

**Logo:** canonical variants live in the FBC folder at
`fbc-slides/assets/logo-variants/`. The site uses the full-color version
(`assets/fbc-logo-color.png`).

---

## 2. Page structure (single scrolling page)

1. **Hero** — washed building art behind: logo, "The Fuquay Business Coalition" (display
   font), tagline "It's as easy as FBC," mission verbatim, and the **Message Us** button.
2. **What we're about** — see copy below.
3. **When we meet** — Wednesdays 9 AM, The Citadel Event Space, Main Street, Fuquay-Varina;
   1st Wednesday = Visitors Day.
4. **Mark your Wednesdays** — embedded live Google Calendar.
5. **Come see what we're about** — the visitor form (`id="visit"`, the Message Us button
   target).
6. **Footer** — mission, location line, the colorful "art by faejays" credit, copyright.

### Final copy

**Hero**
- Title: The Fuquay Business Coalition
- Tagline: It's as easy as FBC
- Mission: "To empower growth through authentic connections, collaborations and accountability."
- Button: **Message Us and let us know you are visiting!**

**What we're about**
> We're a room full of Fuquay-Varina business owners who show up for each other every week… when we can. 😅
>
> Wednesday mornings are about breaking any ice that's built up and digging into the soil of our businesses to ensure we are all growing great roots together. We swap what's actually working, and hold each other to the goals we set. No stiff networking, only the occasional script in our circle of seats.

**When we meet**
> Wednesday mornings. Doors open at 9 AM, the music's on, and we catch up in a circle before we get into it — an ice breaker and intros, the week's topic, referrals and recommendations, what's happening around town, a little group business, then we close on our mission and head out to start the day.
>
> The first Wednesday of every month is Visitors Day — if you're thinking about checking us out, that's the perfect morning to walk in.

- When: Wednesdays, 9:00 AM
- Where: The Citadel Event Space, Main Street, Downtown Fuquay-Varina
- First-timers: Always welcome — especially the 1st Wednesday

---

## 3. Background art

- **Source:** faejays illustration of the downtown Fuquay-Varina building (The Citadel).
  Canva design ID `DAHKUT5xcgU`, 2048×1349. Saved to `assets/building-art.png`.
- **Treatment:** pale, washed-out "window reflection" so text/content stays readable on top.
- **CSS controls** (in `index.html`):
  - Full-page layer: `--bg-opacity: 0.12; --bg-saturate: 0.6; --bg-brightness: 1.18;`
    over a cream veil gradient.
  - Hero layer: art at `opacity: 0.28` with a radial cream veil.
- **Credit:** small but boldly colorful "art by faejays" pill in the footer (rainbow
  gradient). Keep the credit — it's a requested, branded element.

---

## 4. Calendar (Google Calendar embed)

- **Calendar:** `yourneighbor@thefuquaybusinesscoalition.com` (primary calendar on the FBC
  Workspace account). Already populated with weekly meetings, Visitors Days, Member
  Spotlights, and holiday skip-weeks.
- **Embed used:**
  ```html
  <iframe
    title="FBC meeting calendar"
    src="https://calendar.google.com/calendar/embed?src=yourneighbor%40thefuquaybusinesscoalition.com&ctz=America%2FNew_York&mode=AGENDA&showTitle=0&showPrint=0&showCalendars=0"
    loading="lazy"></iframe>
  ```
- **REQUIRED before it displays publicly:** in Google Calendar → Settings → this calendar →
  **Access permissions** → check **"Make available to public."** (Sharing changes must be
  done by the owner.)

---

## 5. Message form

**Fields** (delivers to `yourneighbor@thefuquaybusinesscoalition.com`):
- Your name *(required)*
- Your business
- Email *(required — so we can reply)*
- How did you hear about FBC?
- What brings you in? Why are you visiting? *(textarea)*
- Hidden honeypot field `_gotcha` for spam protection
- Submit button: **Message Us and let us know you are visiting!**

**Delivery:** built for **Web3Forms** (free; no account needed on our side — just a free
access key tied to the FBC email). In `index.html`, replace:
```js
var WEB3FORMS_ACCESS_KEY = "REPLACE_WITH_ACCESS_KEY";
```
with the key from https://web3forms.com (enter the FBC email, get the key).
**Fallback:** until a key is added, submitting opens the visitor's email app pre-addressed
to the FBC inbox, so the form is never dead. A visible `mailto:` link is also shown.

---

## 6. Tech & hosting

- **Stack:** a single static `index.html` (all CSS and JS inline). No build step, no
  framework. Amarante loaded from Google Fonts CDN.
- **Host:** GitHub Pages (free), served from the existing GitHub repo.
- **Custom domain:** thefuquaybusinesscoalition.com (registered via Google Workspace).

### Repo layout
```
/
  index.html
  CNAME                      ← contains: thefuquaybusinesscoalition.com
  assets/
    building-art.png         ← faejays illustration (washed-out background)
    fbc-logo-color.png       ← hero logo (full color)
    fbc-logo-color-400.png
    fbc-logo-no-disc.png      ← alt logo (transparent disc)
```

### Deploy steps
1. Connect GitHub; create/confirm the repo; push the files above.
2. Repo → **Settings → Pages** → Source: deploy from branch (`main`, root). Save.
3. Add a `CNAME` file containing `thefuquaybusinesscoalition.com` (or set the custom
   domain in the Pages UI, which creates it).
4. **DNS** (in Google Workspace / Squarespace Domains for the domain):
   - Apex `@` → A records (GitHub Pages):
     `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
   - `www` → CNAME → `<github-username>.github.io`
   - *(Confirm current GitHub Pages IPs in GitHub's docs before saving.)*
5. In Pages settings, enable **Enforce HTTPS** once the cert provisions.

---

## 7. Verify before calling it done
- Calendar section shows real upcoming Wednesdays (not a "private" notice).
- Form submits and a test message lands in the FBC inbox.
- Logo, washed background, fonts, and the faejays credit all render.
- Looks right on a phone (responsive).
- `https://thefuquaybusinesscoalition.com` loads with a valid certificate.

---

*Built for Shannon Volpe. Keep it simple — that's the whole point.*
