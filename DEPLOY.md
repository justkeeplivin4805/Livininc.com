# LiViN Website — Launch & Iteration Plan

This is the operational playbook for getting the site live today and keeping it easy to iterate on as you bring more tools online (Mac Mini + Gemini + Codex + Claude).

---

## Phase 1 — Go Live Today (15 minutes)

You don't need a custom domain or a Git repo to launch. You can be live on a public URL in under 15 minutes using Netlify's drag-and-drop.

### Step 1 — Final placeholder swaps
Open `index.html` and search/replace:

| Find | Replace with |
|---|---|
| `procurement@livin-inc.com` | The email you want briefs sent to (e.g. `livin4069@gmail.com` for now, or a branded address later) |
| `+1 (000) 000-0000` | Your real phone number (format with parentheses: `+1 (404) 555-0123`) |
| `tel:+10000000000` | Same number, digits only with country code: `tel:+14045550123` |

Already wired and live:
- Formspree form action → `https://formspree.io/f/xdaboodj`
- Calendly link → `https://calendly.com/livin4069/30min`

### Step 2 — Activate Formspree
Open `index.html` in your browser, fill out the contact form once with a test entry, submit it. Formspree will send a one-time confirmation email to `livin4069@gmail.com` — click the link inside to activate the form. After that, every submission emails you directly. (Free tier: 50/month.)

### Step 3 — Deploy to Netlify
1. Go to **netlify.com**, sign up free (use your Google account for fastest setup).
2. From the dashboard click **Sites → Add new site → Deploy manually**.
3. Drag the `website` folder onto the upload zone.
4. You get a live URL within seconds — something like `https://thoughtful-procurement-1234.netlify.app`.
5. In **Site settings → Change site name**, rename it to something you like (e.g. `livin-procurement`) — gives you `https://livin-procurement.netlify.app`.

### Step 4 (optional, anytime) — Custom domain
1. Buy a domain on **Cloudflare Registrar** (cheapest, no upsells) or **Namecheap**. Suggested options: `livin-inc.com`, `livinprocurement.com`, `livin.co`.
2. In Netlify: **Domain settings → Add custom domain** → follow the DNS instructions. SSL is free and automatic.

You're live. That's Phase 1 done.

---

## Phase 2 — Iteration Infrastructure (do this when Mac Mini arrives)

The goal: any AI agent on your machine — Claude, Gemini, Codex, whichever — can edit the site, you can preview the change, and a `git push` deploys it automatically. No more drag-and-drop.

### The setup (one-time, ~30 min)

**1. Install the basics on the Mac Mini:**
```bash
# Xcode command-line tools (gives you git)
xcode-select --install

# Homebrew (gives you everything else)
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Optional but recommended:
brew install gh           # GitHub CLI
brew install --cask visual-studio-code  # editor any AI tool can drive
```

**2. Initialize the repo:**
```bash
cd "/Users/matthewme@backbase.com/My Drive/LiViN/website"
git init
git add .
git commit -m "Initial site"
gh repo create livin-website --private --source=. --push
```

**3. Connect Netlify to the repo (replaces drag-and-drop):**
- In Netlify: **Site settings → Build & deploy → Link site to Git**.
- Pick `livin-website` from GitHub.
- Build command: leave blank. Publish directory: leave blank (root).
- Save.

From now on, any commit to `main` auto-deploys in ~30 seconds. Branch deploys give you preview URLs for testing changes before merging.

### The iteration workflow (any AI tool)

Once the repo + Netlify are linked, the loop becomes:

```
1. AI agent edits index.html (or styles.css if you split it later)
2. Open the file locally to preview the change
3. git commit -m "<what changed>"
4. git push
5. Netlify auto-deploys; live in ~30 seconds
6. If anything's wrong, git revert and push again
```

This works identically whether the agent is Claude, Gemini, Codex, Cursor, or you editing directly.

### Multi-agent best practices
- **One commit per change.** Easier to revert one thing than five.
- **Use branches for big edits.** `git checkout -b new-vertical-section`, then merge to `main` once you've previewed it. Netlify will give you a preview URL on the branch automatically.
- **Read `ITERATION.md` before editing.** Every agent should be pointed at that file first — it's the map of what's where in the code.

---

## What's already wired

| Element | Status |
|---|---|
| Hero, capabilities, verticals, cross-border/LATAM, why, process, contact, footer | Built |
| Formspree contact form | Live (`xdaboodj`) — needs one-time activation |
| Calendly booking | Live (`livin4069/30min`) |
| Trust bar | Updated — no EIN, no entity type displayed |
| Footer copyright | Updated — no entity type displayed |
| Mobile responsive | Yes, tested down to 375px |

---

## What still needs your input
1. Real phone number to display
2. The procurement email address (today: `livin4069@gmail.com` is the simplest, since it matches Formspree/Calendly)
3. Custom domain (when you're ready)
