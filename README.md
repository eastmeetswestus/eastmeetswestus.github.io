# East Meets West: website template

A static site (HTML, CSS and a little JavaScript) for **East Meets West**, which sells hot buns and boba. It is built for GitHub Pages and needs no build step and no framework.

This business is separate from Confetti and Pixels Art and from TradeLedger / ContractorSheetsCo. Do not reuse their logos, accounts, copy or links here.

**Status (2026-10-16):** finished design with free stock photos as filler. Domain set to `eastmeetswest.us` (`CNAME`, canonical, Open Graph, `robots.txt`, `sitemap.xml`). Menu names and descriptions are generic samples, each marked `<!-- (sample) -->` in `index.html`; every price shows `$—`. Address, hours, phone, email, order links, social links and the story are still `[PLACEHOLDER]`s. Nothing factual has been invented (no prices, address, hours, reviews or awards). Photo credits: `assets/images/CREDITS.md`. `_preview/` holds local screenshots and is excluded by `.gitignore` (do not upload it).

```
website/
├── index.html        main page (all sections)
├── styles.css        all styling; colors are tokens at the top
├── script.js         mobile menu toggle + footer year (about 30 lines)
├── 404.html          "page not found" page
├── robots.txt        template
├── sitemap.xml       https://eastmeetswest.us/
├── CNAME             eastmeetswest.us (GitHub Pages custom domain)
├── assets/
│   ├── favicon.svg   PLACEHOLDER logo mark
│   └── images/       WebP photos (stock filler) + og-image.jpg + CREDITS.md
└── README.md
```

To preview, double-click `index.html`. Fonts load from Google Fonts, so you need internet access for the final look.

---

## A. How to fill each placeholder

Search the files for `[` to find every placeholder. In VS Code, use Ctrl+Shift+F and search for `\[[A-Z]` with regex turned on.

### 1. Meta / SEO (top of `index.html`, inside `<head>`)
| Placeholder | What to put |
|---|---|
| `[SHORT TAGLINE]`, `[CITY]` in `<title>` | Keep it under about 60 characters, e.g. `East Meets West \| Buns & Boba \| Springfield` |
| `[META DESCRIPTION]` | 140 to 160 characters of true facts: what you serve, where, and why to visit |
| `[DOMAIN]` | Your final domain without `https://`, e.g. `eastmeetswestboba.com`. It appears in `index.html`, `robots.txt` and `sitemap.xml` |
| `[OG DESCRIPTION]`, `[OG IMAGE ALT TEXT]` | The text and photo description shown when the link is shared on Facebook, iMessage and similar apps |
| `og-image.jpg` | Save a **1200x630** JPG as `assets/images/og-image.jpg` |
| `apple-touch-icon.png` | A **180x180** PNG logo at `assets/apple-touch-icon.png` |
| `assets/favicon.svg` | Replace it with the real logo mark (square SVG), or use a PNG and change the `<link rel="icon">` line |

### 2. Structured data (the `<script type="application/ld+json">` block)
This block tells Google you are a restaurant. Fill in the name, phone, email, address, `geo` (right-click your pin in Google Maps to copy the latitude and longitude), `priceRange` (`$` or `$$`), `acceptsReservations`, and the social URLs in `sameAs`.
- **Hours:** add one object per group of days that share hours, e.g.
  `{ "@type": "OpeningHoursSpecification", "dayOfWeek": ["Monday","Tuesday"], "opens": "11:00", "closes": "20:00" }`. Use 24-hour time.
- **Delete any line you cannot fill truthfully**, and keep the JSON valid (no trailing comma before `}` or `]`).
- Test it at https://search.google.com/test/rich-results after you publish.

### 3. Header and hero
- `[CTA LABEL]` and `[PRIMARY CTA LINK]`: choose **one** action and use the same label in the nav and the hero:
  - "Order now" links to your online ordering URL
  - "Find us" links to `#visit`
  - "Book catering" links to `#contact` or a booking form URL
- `[TAGLINE]`: one short line.
- **Logo:** to use an image logo, replace the `EW` text mark in the header with the `<img>` line shown in the comment.

### 4. Photos
The site now uses stock photos from Pexels/Unsplash (see `assets/images/CREDITS.md`). To swap in a real photo, save it in `assets/images/` with the same file name (same shape: buns/boba cards 4:3 at 900x675, gallery 4:5 at 640x800, about 4:5 at 900x1125, hero about 1920 wide), or change the `src`, `width`, `height` and `alt` on the `<img>`. Then delete its row in CREDITS.md.

Older notes for the original placeholder slots:
Each photo slot is a `<div class="img-slot">`. To add a photo, replace the whole `<div ...>...</div>` with an `<img>`:
```html
<img src="assets/images/bun-1.jpg" alt="Describe what is in the photo" width="800" height="600" loading="lazy">
```
| Slot | Shape | Suggested size |
|---|---|---|
| `hero` | square | 1200x1200 (use `fetchpriority="high"` instead of `loading="lazy"`) |
| `bun-*`, `boba-*` | 4:3 landscape | 800x600 |
| `about` | 4:5 portrait | 960x1200 |

Photos are cropped to these shapes automatically. Keep each file under about 300 KB: export as WebP or JPG at about 80% quality (https://squoosh.app is free). Always write real `alt` text.

### 5. Menu cards (Hot Buns and Boba)
The menu is plain HTML in `index.html`, so it works without JavaScript and search engines can read it.
- **Add an item:** copy a whole `<article class="menu-card"> ... </article>` block and paste it next to the others.
- **Remove an item:** delete the whole `<article>` block.
- Fill in `[MENU ITEM]`, `[PRICE]` (e.g. `$6.50`) and `[DESCRIPTION]`.
- `<span class="tag">[TAG]</span>` is optional (e.g. Vegetarian, Spicy, Seasonal). Delete it if you don't need it, and only use a dietary tag if it is accurate.
- The grid rearranges itself automatically for 1 to 4+ columns.

### 6. Build your boba
Fill in `[BASE OPTIONS]`, `[FLAVOR OPTIONS]` and `[TOPPING OPTIONS]`. To add a 4th step (sweetness or ice), copy a `<li class="step">` block.

### 7. Our story
Fill in `[ABOUT HEADLINE]`, the two paragraphs, `[OWNER NAME], [TITLE]` and `[PHOTO: about]`.

### 8. Hours and location
- Fill in the address, `[PARKING / ACCESS NOTE]` and the 7 `[HOURS]` cells (e.g. `11am – 8pm` or `Closed`).
- `[GOOGLE MAPS DIRECTIONS LINK]`: in Google Maps, click **Share → Copy link**.
- **Map embed:** in Google Maps, click **Share → Embed a map → Copy HTML**. Copy only the `src="..."` URL into the commented `<iframe>`, uncomment it (remove `<!--` and `-->`), and delete the `[MAP]` placeholder div.
- Keep these hours the same as the JSON-LD hours and your Google Business Profile.

### 9. Order and contact
- `[ORDER LINK]`: your ordering page (Square, Toast, DoorDash and so on). Delete the item if you don't offer online ordering.
- Phone: the `href` needs digits only, e.g. `tel:+15555555555`. The visible text can be formatted, e.g. `(555) 555-5555`.
- Email: `mailto:you@domain.com`.
- Catering: a link or a `mailto:`. Delete the item if you don't offer catering.

### 10. Social and footer
Replace `[INSTAGRAM URL]`, `[TIKTOK URL]` and `[FACEBOOK URL]`, and delete any platform you don't use (also remove it from `sameAs` in the JSON-LD). Fill in `[FOOTER LINE]`. The year updates automatically.

### 11. Colors and fonts
Edit the tokens at the top of `styles.css` (`--red`, `--jade`, `--cream`, `--gold` and so on). Dark mode is a second block of tokens just below them. It follows the visitor's device setting, and light mode is the default.

### 12. robots.txt and sitemap.xml
Replace `[DOMAIN]` in both files, and set `[YYYY-MM-DD]` in the sitemap to the date you publish.

---

## B. Publish on GitHub Pages (free)

1. Create a free account at https://github.com if you don't already have one.
2. Create a **new public repository**. Choose one:
   - **User site:** name the repo exactly `<username>.github.io`. The site appears at `https://<username>.github.io/`.
   - **Project site:** use any name, e.g. `east-meets-west`. The site appears at `https://<username>.github.io/east-meets-west/`.
3. Upload the **contents** of this `website/` folder (not the folder itself) to the root of the repo. Use **Add file → Upload files** and drag everything in, including the `assets` folder. Then commit.
4. In the repo, go to **Settings → Pages**. Under **Build and deployment**, set **Source: Deploy from a branch**, **Branch: `main`**, folder **`/ (root)`**, then click **Save**.
5. After a minute or two, the URL appears at the top of the Pages settings. Open it and check every section on your phone.

> **Project site without a custom domain:** `404.html` uses root paths (`/styles.css`). Change them to `/east-meets-west/styles.css` (your repo name), or connect a custom domain (section C), which makes root paths work as they are.

To update the site later, edit or upload files in the repo. Pages redeploys automatically.

---

## C. Connect a custom domain

**Candidate domains:** `eastmeetswestboba.com` (**recommended**: it says what you sell and is easier to spell out loud) or `eastmeetswest.us`. Check that the domain is available, then buy it from a registrar. Buying a domain is the owner's decision and cost; this template does not buy anything.

### Steps
1. **Verify the domain in GitHub first.** Go to your GitHub profile: **Settings → Pages → Add a domain**. This stops other people from claiming it.
2. **Add a `CNAME` file** to the repo root. It is a plain text file named exactly `CNAME`, with no file extension, containing one line:
   ```
   eastmeetswestboba.com
   ```
   (Typing the domain in **repo Settings → Pages → Custom domain** also creates this file.)
3. **At your domain registrar's DNS settings**, add these records:

   | Type | Host / Name | Value |
   |---|---|---|
   | A | `@` | `185.199.108.153` |
   | A | `@` | `185.199.109.153` |
   | A | `@` | `185.199.110.153` |
   | A | `@` | `185.199.111.153` |
   | CNAME | `www` | `<username>.github.io` (no repo name) |

   Optional IPv6 (AAAA records for `@`): `2606:50c0:8000::153`, `2606:50c0:8001::153`, `2606:50c0:8002::153`, `2606:50c0:8003::153`.

   *Checked against GitHub's docs on 2026-10-16 ("Managing a custom domain for your GitHub Pages site"). Recheck before you set up DNS: https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site*

   Delete any old parking-page A or CNAME records that the registrar added for `@` or `www`.
4. In **repo Settings → Pages**, enter the domain under **Custom domain** and click Save. Once the DNS check passes (minutes to 24 hours), tick **Enforce HTTPS**.
5. Replace `[DOMAIN]` everywhere with the final domain (`index.html`, `robots.txt`, `sitemap.xml`).
6. Optional: if you also buy the second domain, forward it to the main one at the registrar. Don't publish the same site on both domains.

### After launch
- Submit `https://<domain>/sitemap.xml` in Google Search Console.
- Set up or claim your **Google Business Profile** with the same name, address, phone and hours as the site.
