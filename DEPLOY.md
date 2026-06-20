# Deploy & Update Cheat-Sheet

Your site is a static HTML/CSS site hosted on **GitHub Pages** at
**https://raghavchalapathy.ai** (repo: `raghavchalapathy/raghavchalapathy.github.io`).

There is **no build step**. Editing = pushing. That's it.

---

## Make an edit and publish (the 90% case)

```bash
cd "/Users/raghav/Documents/AppliedAIFab/appliedAI/AI Engineer/projects/profileWebsite"

# 1. edit index.html / style.css / swap an image in assets/ ...

# 2. preview locally first (recommended)
python3 -m http.server 8000
#    open http://localhost:8000  -> check it, Ctrl-C to stop the server

# 3. ship it
git add -A
git commit -m "Describe what you changed"
git push
```

GitHub rebuilds automatically. Changes go live in ~30-60 seconds.
Hard-refresh your browser (Cmd-Shift-R) if you don't see the update.

---

## Files in this repo

| File | Purpose |
|------|---------|
| `index.html` | All page content/markup |
| `style.css` | All styling (hand-rolled 12-col grid + timeline) |
| `assets/me.jpeg` | Profile photo |
| `CNAME` | Custom domain — **do not delete** (`raghavchalapathy.ai`) |
| `.nojekyll` | Tells Pages to skip Jekyll processing |
| `README.md` | Repo description |
| `DEPLOY.md` | This file |

**Deliberately NOT published** (kept local / out of git):
`CV_Raghav_Chalapathy_Resume.pdf`, `assets/urls.txt`, `plan.txt`.
They contain personal info. Keep them out of commits.

---

## Common edits

**Change the tagline:** edit the `<h2>` in `index.html`.

**Add a timeline entry:** copy a `<div class="entry row">...</div>` block in the
`#history` section and edit the `.timespan` + `.desc`.

**Add a publication:** copy a `<div class="pub">...</div>` block in `#publications`.

**Swap the photo:** replace `assets/me.jpeg` (keep the same filename, or update
the `src` in `index.html` and the `og:image` meta tag).

**Change a social link:** edit the `<a href="...">` entries inside `<div id="dico">`.

---

## DNS / domain (already configured — for reference only)

Namecheap -> Advanced DNS for `raghavchalapathy.ai`:

| Type | Host | Value |
|------|------|-------|
| A | @ | 185.199.108.153 |
| A | @ | 185.199.109.153 |
| A | @ | 185.199.110.153 |
| A | @ | 185.199.111.153 |
| CNAME | www | raghavchalapathy.github.io. |

No URL-redirect/parking records on `@`. Nameservers = Namecheap BasicDNS.

---

## Useful checks

```bash
# Is DNS pointing at GitHub? (want four 185.199.x.x)
dig +short raghavchalapathy.ai A

# Is the live site up?
curl -s -o /dev/null -w "%{http_code}\n" -L https://raghavchalapathy.ai/

# GitHub Pages status (needs: gh auth login)
gh api repos/raghavchalapathy/raghavchalapathy.github.io/pages \
  --jq '{cname, https_enforced, status}'
```

## Enforce HTTPS

After the TLS cert provisions (first time only), enforce HTTPS:

- UI: repo -> Settings -> Pages -> tick **Enforce HTTPS**, or
- CLI: `gh api -X PUT repos/raghavchalapathy/raghavchalapathy.github.io/pages -F https_enforced=true`
