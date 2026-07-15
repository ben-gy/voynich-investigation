# Deploy runbook

Static single-page site. Target: **Cloudflare Pages** (free tier, A$0/month), matching your existing CF stack. The repo is already `git init`'d with a first commit — you only need to add a remote and push.

Replace placeholders:
- `<GH_USER>` — your GitHub username/org
- `<REPO>` — e.g. `voynich-investigation`
- `<DOMAIN>` — the hostname you want it live on, e.g. `voynich.ben.gy`

---

## 1. Push to GitHub

Using the GitHub CLI (already authenticated in your Claude Code environment):

```bash
# from the repo root
gh repo create <GH_USER>/<REPO> --public --source=. --remote=origin --push
```

Or manually if the repo already exists:

```bash
git remote add origin git@github.com:<GH_USER>/<REPO>.git
git branch -M main
git push -u origin main
```

---

## 2. Get it live on your domain

### Path A — Wrangler direct (fastest, ~60 seconds)

```bash
# one-time: create the Pages project
npx wrangler pages project create <REPO> --production-branch main

# deploy the current directory
npx wrangler pages deploy . --project-name <REPO>

# attach your custom domain (domain must be on your Cloudflare account)
npx wrangler pages domain add <DOMAIN> --project-name <REPO>
```

Cloudflare auto-creates the CNAME and provisions the TLS cert. If `<DOMAIN>`'s zone is already on Cloudflare (yours are), it's live within a minute or two.

### Path B — Git-connected (auto-deploy on every push)

1. Cloudflare dashboard → **Workers & Pages** → **Create** → **Pages** → **Connect to Git**
2. Pick `<GH_USER>/<REPO>`, branch `main`
3. Build settings: **Framework preset = None**, **Build command = (blank)**, **Output directory = `/`**
4. Save & deploy
5. **Custom domains** tab → **Set up a custom domain** → enter `<DOMAIN>`

After this, every `git push` to `main` redeploys automatically.

---

## 3. Verify

```bash
curl -sI https://<DOMAIN> | head -n 5
```

Expect `HTTP/2 200` and `cf-cache-status` present.

---

## Notes
- No secrets, env vars, or bindings needed — it's a plain static file.
- `_headers` is respected by Pages automatically (caching + security headers).
- To roll back: `wrangler pages deployment list --project-name <REPO>` then promote a previous deployment in the dashboard.
