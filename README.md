# TradeWind — Curated Global Tech Gadgets Showcase

A single-file, static affiliate storefront (`index.html`) with no backend, no
checkout, and no card collection. Every product routes to an official store
via `target="_blank" rel="noopener noreferrer sponsored"`. Built with vanilla
HTML/CSS/JS for maximum speed on Vercel's static hosting.

## Files

| File | Purpose |
|---|---|
| `index.html` | The entire app — markup, "Cargo Manifest" design system CSS, product data, and filtering/search JS |
| `vercel.json` | Static hosting config + security headers + cache headers |
| `robots.txt` | Search engine crawl rules |
| `sitemap.xml` | Basic sitemap for the homepage |

## 1. Before you deploy — replace the placeholders

Open `index.html` and update:

1. **Affiliate links** — every product in the `PRODUCTS` array (near the
   bottom of the file, inside the `<script>` tag) has a `link` field like:
   ```
   link: "https://www.amazon.com/s?k=Sony+WH-1000XM5&tag=youraffiliateid-20"
   ```
   Replace `youraffiliateid-20` with your real Amazon Associates tag, or swap
   the whole URL for a ShareASale / CJ / Impact / direct-brand affiliate link.
   Every product should point to a real product page, not a search results
   page, once you have real tracking links.

2. **Domain references** — search the file for `your-domain.vercel.app` and
   replace with your real deployed domain (used in the canonical tag, Open
   Graph tags, JSON-LD, `robots.txt`, and `sitemap.xml`).

3. **AdSense** — once your AdSense account is approved, uncomment the script
   tag near the top of `<head>` and add your publisher ID. Then replace the
   contents of the `.ad-slot` `<div>` elements with your actual `<ins
   class="adsbygoogle">` ad units (there are 3 pre-built placeholder slots:
   one leaderboard in the hero, one inline in the FAQ, and one auto-inserted
   every 6 products in the grid).

4. **Product photos (optional)** — the current build uses lightweight inline
   SVG line icons per category instead of photos, so the page has zero
   external image requests and loads instantly. If you'd rather use real
   product photography, replace the `card__icon` div in the `cardHTML()`
   function with an `<img>` tag pointing at your own optimized images (WebP,
   ideally under 40KB each, with `loading="lazy"`).

## 2. Push to GitHub

```bash
cd tradewind
git init
git add .
git commit -m "Initial commit: TradeWind affiliate storefront"
git branch -M main
git remote add origin https://github.com/<your-username>/tradewind.git
git push -u origin main
```

(Create the empty `tradewind` repo on GitHub first at
https://github.com/new — don't initialize it with a README, since you
already have one.)

## 3. Deploy to Vercel

**Option A — Vercel dashboard (easiest):**
1. Go to https://vercel.com/new
2. Import the `tradewind` GitHub repo you just pushed.
3. Framework preset: choose **Other** (this is a static site — no build step,
   no install command needed).
4. Leave the build/output settings blank and click **Deploy**.
5. Vercel will give you a live URL like `tradewind.vercel.app` within
   seconds.

**Option B — Vercel CLI:**
```bash
npm i -g vercel
cd tradewind
vercel        # deploy a preview
vercel --prod # promote to production
```

## 4. After deploying

- Update `your-domain.vercel.app` references (step 1.2 above) to your real
  Vercel URL or custom domain, then redeploy.
- Submit `https://your-domain.vercel.app/sitemap.xml` to Google Search
  Console and Bing Webmaster Tools to speed up indexing.
- Add a custom domain under **Project → Settings → Domains** in Vercel if
  you have one.
- Re-check your affiliate disclosure wording against the FTC's current
  guidance (and any local advertising-standards body relevant to your
  audience) before going live — the built-in disclosure banner and footer
  text are a starting point, not legal advice.

## Customizing the catalog

All product data lives in the `PRODUCTS` array inside `index.html`. To add,
remove, or edit a product, edit that array — the grid, search index, category
filters, and result counts all regenerate automatically from it. To add a
new category, add it to the `CATEGORY_ORDER` array and give it an entry in
the `ICONS` object (an inline SVG string).
