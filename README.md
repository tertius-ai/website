# tertius.cc

Static site for tertius.cc. Plain HTML/CSS, no build step.

## Local preview

```sh
python3 -m http.server 8000 --directory .
# open http://localhost:8000
```

## Deployment (GitHub Pages)

1. Propose changes in a pull request to `tertius-ai/website`; the protected `main`
   branch requires approval before merge.
2. The `Website Pages` workflow prepares a static-site artifact on pull requests
   and deploys it after changes merge into `main`. Manual deployment also uses
   `main`. The Pages source is **GitHub Actions**.
3. Set the custom domain to `tertius.cc` in the repository's Pages settings.
   Workflow-based Pages publishing manages this setting independently of the
   protected branch; GitHub ignores the repository's `CNAME` file in this mode.
4. Configure DNS at Cloudflare:
   - `A` records for `tertius.cc` pointing to GitHub Pages IPs:
     - `185.199.108.153`
     - `185.199.109.153`
     - `185.199.110.153`
     - `185.199.111.153`
   - `AAAA` records (IPv6):
     - `2606:50c0:8000::153`
     - `2606:50c0:8001::153`
     - `2606:50c0:8002::153`
     - `2606:50c0:8003::153`
   - `CNAME` for `www` → `tertius-ai.github.io`
5. In GitHub Pages settings, enable **Enforce HTTPS** once DNS propagates.

### Switching from branch publishing

After this workflow's pull request is approved, change Pages → Build and
deployment → Source to **GitHub Actions** immediately before merging it. The
merge starts the first workflow deployment. Confirm that `Deploy Pages` succeeds.

For a stuck certificate, GitHub documents removing and re-adding the custom domain
in Pages settings to restart provisioning. Workflow publishing supports this
without committing to `main`. See [GitHub's certificate provisioning guide](https://docs.github.com/en/pages/getting-started-with-github-pages/securing-your-github-pages-site-with-https).

The website's eight apex `A`/`AAAA` records and `www` CNAME are currently proxied
through Cloudflare. Before switching them to **DNS only** for direct GitHub Pages
HTTPS, verify that GitHub has a valid certificate or allow a maintenance window
for issuance. An expired origin certificate produces browser errors when the
proxy is disabled.

## Email

The domain's mail records route email to Google. Manage the Google MX, SPF, DKIM,
and DMARC records separately from the website's `A`, `AAAA`, and `www` records.

## Files

- `index.html` — single-page academic project site
- `style.css` — minimal monochrome research-terminal theme
- `fonts/` — self-hosted IBM Plex Mono with license
- `favicon.svg` — `[t]` mark
- `logo.svg` / `logo.png` — square brand mark
- `og.svg` / `og.png` — source and rendered social preview card
- `sitemap.xml` — canonical public homepage for search indexing
- `.github/workflows/pages.yml` — PR artifact preparation and main-branch deployment
- `CNAME` — domain reference retained from branch-based publishing
