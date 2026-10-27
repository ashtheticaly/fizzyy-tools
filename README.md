# Fizzyy Tools

Static AI tools directory. Plain HTML, CSS, JavaScript and one JSON file. No build step, no paid services, no API keys.

## 1. Preview
Browsers block loading the JSON file when you double-click index.html, so run a tiny local server (Python is free and often pre-installed):

    cd fizzyy-tools
    python3 -m http.server 8000

Open http://localhost:8000. On Android you can use Termux, or just deploy (step 3) and preview online.

## 2. Edit tool listings
Open `data/tools.json`. Each tool is one object. Add a new one by copying an existing object and changing every field:
- `id`: short lowercase id with no spaces (used in the URL).
- `cat`: writing, image, video, audio, coding, productivity, education, business, design or research.
- `pricing`: exactly Free, Freemium or Paid.
- `pop`: your own 1-100 editorial score (used for "Popular" and sorting).
- `verified`: set to a date like "2026-10-27" only after you check the official pricing page yourself. Leave null if unchecked.
- `sponsored`: true shows a Sponsored label. `affiliate`: your real affiliate URL (leave null otherwise).
New tools added to the end of the file appear under "Recently added". Then run `python3 make_sitemap.py` to refresh sitemap.xml.

Every listing was written from general knowledge, so pricing details are intentionally broad and `verified` is null. Check each official site before relying on a claim.

## 3. Deploy free
GitHub Pages: create a free GitHub account and a public repository, upload all files from this folder (keep the same structure), then Settings > Pages > Deploy from branch > main > / (root). Your site appears at https://USERNAME.github.io/REPO/.
Cloudflare Pages: create a free account, Workers & Pages > Create > Pages > connect your GitHub repo (or upload the folder), leave build command empty and output directory `/`.
Both free plans need no credit card for static sites. Check each host's current free-plan terms.

## 4. Custom domain (optional, a domain costs money yearly)
Buy a domain from any registrar, add it in GitHub Pages settings (or Cloudflare Pages > Custom domains), add the DNS records they show, and enable HTTPS. Then set `SITE` in make_sitemap.py to your real address and rerun it.

## 5. Prepare for advertising
- Replace the placeholder text in contact, about, privacy and terms with real details. Have the legal pages reviewed.
- AdSense approval is decided by Google and is not guaranteed. It generally expects original, useful content, a real domain, and complete policy pages. Apply only when the site has enough original content.
- After approval, paste Google's script in the marked comment in each page head and unhide the `ad-slot` elements (remove the `hidden` attribute). Add a cookie consent notice where required and update the Privacy Policy.
- Affiliate links: join real programs, put the URL in `affiliate`, and keep the disclosure page accurate.

## Known limitations
- Header and footer are repeated in each HTML file; edit them in all pages.
- Tool pages use `tool.html?id=...`, filled in by JavaScript. Search engines can read this, but static per-tool pages would be stronger for SEO; a small generator script can add them later.
- No og:image is included; add a 1200x630 image and an og:image tag if you want link previews.
- The contact page uses an email link because there is no backend.
