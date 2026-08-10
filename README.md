# tertius.cc

Static site for tertius.cc. Plain HTML/CSS, no build step.

## Local preview

```sh
python3 -m http.server 8000 --directory .
# open http://localhost:8000
```

## Deployment (GitHub Pages)

1. Create a GitHub repo at `tertius-ai/website` and push this directory.
2. In the repo settings under **Pages**, set source to **Deploy from a branch** → `main` / `/ (root)`.
3. The `CNAME` file sets the custom domain to `tertius.cc`.
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

## Email (Cloudflare Email Routing)

1. In Cloudflare dashboard → Email → Email Routing → enable.
2. Cloudflare adds the required MX + TXT records automatically.
3. Add a custom address: `contact@tertius.cc` → forward to your personal inbox.
4. Verify the destination address via the confirmation email.

## Files

- `index.html` — single-page company site
- `style.css` — minimal monochrome research-terminal theme
- `fonts/` — self-hosted IBM Plex Mono with license
- `favicon.svg` — `[t]` mark
- `logo.svg` / `logo.png` — square brand mark
- `og.png` — social preview card
- `CNAME` — GitHub Pages custom domain config
