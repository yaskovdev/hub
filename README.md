# yaskov.dev — project hub

A single, dependency-free static page that links to my live pet projects and a few
articles. It replaces the old (broken) URL shortener at the apex of `yaskov.dev`.

- `index.html` — the whole site (inline CSS + a tiny theme-toggle script, no build step)
- `CNAME` — custom domain for GitHub Pages (`yaskov.dev`)
- `.nojekyll` — serve files as-is (skip Jekyll processing)

## Preview locally

Any static server works, e.g.:

```powershell
python -m http.server 8080
# then open http://localhost:8080
```

## Deploy with GitHub Pages

This repo is served straight from the default branch — no build, no Actions.

1. Push to GitHub (`yaskovdev/hub`).
2. **Settings → Pages → Build and deployment**: Source = *Deploy from a branch*,
   Branch = `master` / `/ (root)`, Save.
3. The `CNAME` file sets the custom domain to `yaskov.dev`. Under **Pages → Custom domain**
   it should already read `yaskov.dev`; tick **Enforce HTTPS** once the certificate is issued.

## Point yaskov.dev at GitHub Pages

At your DNS provider for `yaskov.dev`, add the apex records:

| Type | Name | Value |
| ---- | ---- | ----- |
| A    | @    | 185.199.108.153 |
| A    | @    | 185.199.109.153 |
| A    | @    | 185.199.110.153 |
| A    | @    | 185.199.111.153 |
| AAAA | @    | 2606:50c0:8000::153 |
| AAAA | @    | 2606:50c0:8001::153 |
| AAAA | @    | 2606:50c0:8002::153 |
| AAAA | @    | 2606:50c0:8003::153 |

(Optional, recommended) verify the domain for your account with the `_github-pages`
`TXT` record GitHub shows under **Settings → Pages → Verified domains**.

`.dev` is on the HSTS preload list, so HTTPS is mandatory — GitHub Pages issues a free
Let's Encrypt certificate automatically once DNS resolves.

## Notes

- Security headers: GitHub Pages can't set response headers, so the Content-Security-Policy
  is delivered via a `<meta http-equiv>` tag in `index.html` instead.
- The old URL shortener stays "Coming soon"; when revived, give it its own subdomain
  (e.g. `short.yaskov.dev`) and flip that card's button to the live link.
- To add a project: copy an `<article class="card">…</article>` block in `index.html`.
- To add an article: copy an `<a class="post">…</a>` row in the *Writing* section.
- The `variants/` folder (local-only, git-ignored) holds the design explorations.
