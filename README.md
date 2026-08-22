# HumansOfCoding — Website

Static marketing site for **HumansOfCoding** — apps, websites, MVPs and custom software.
Plain HTML, CSS and vanilla JavaScript. No build step, no framework, no server, no paid services.

```
humansofcoding/
├── index.html        all page content
├── style.css         all styling (mobile-first)
├── script.js         all behaviour + YOUR BUSINESS INFO at the top
├── assets/
│   ├── favicon.svg   browser tab icon
│   ├── og-image.svg  social share preview
│   └── README.md     how to add project images
├── .nojekyll         tells GitHub Pages to serve files as-is
├── robots.txt
└── sitemap.xml
```

---

## 1. Run it locally

**Easiest way:** double-click `index.html`. It opens in your browser and everything works —
animations, menu, dark mode, all links.

**Optional (closer to the real thing):** run a tiny local server so the URL is `http://localhost`
instead of `file://`.

```bash
# Python (already installed on most machines)
python -m http.server 8000
# then open http://localhost:8000

# or Node
npx serve .
```

Any change to the files shows up on a browser refresh — there is nothing to build or compile.

---

## 2. Before you publish — 3 things to edit

### a) Your contact details → `script.js`

Open `script.js`. The first block is the only place contact info lives:

```js
const CONFIG = {
  instagram: "humansofcoding",
  whatsapp:  "910000000000",             // ← your number: country code + number, digits only
  whatsappMessage: "Hi Adil! I have an idea I'd like to build. Can we talk?",
  email:     "your-email@example.com",    // ← your real email
  emailSubject: "Project enquiry from humansofcoding.com",
  bookingUrl: ""                          // ← optional Calendly / Topmate link
};
```

Every **Book a Free Call**, **WhatsApp**, **DM** and **Email** button on the page reads from this.

How "Book a Free Call" resolves: `bookingUrl` if set → otherwise WhatsApp → otherwise Instagram DM.
While `whatsapp` is still the `910000000000` placeholder, WhatsApp buttons quietly fall back to
Instagram so no button is ever broken.

### b) Portfolio projects → `index.html`

Search the file for `PORTFOLIO DATA`. Six placeholder projects sit between that marker and
`END PORTFOLIO DATA`. Each one is a self-contained block — edit the category, name and description,
duplicate or delete blocks freely:

```html
<span class="proj__cat">Mobile App</span>
<h3>Restaurant Ordering App</h3>
<p>Menu, cart, live order tracking and a simple kitchen dashboard.</p>
```

To use a real screenshot instead of the drawn thumbnail, see `assets/README.md`.

### c) Testimonials → `index.html`

Search for `TESTIMONIAL PLACEHOLDERS`. The three quotes are clearly-marked placeholders with
generic names — **not** invented customers. When you have real reviews (with the client's
permission), replace the quote, `.t__name` and `.t__role`, then delete:

- the `<span class="t__flag">Placeholder</span>` chip in each card, and
- the "Sample layout — real client reviews will be added here." line in the section heading.

---

## 3. Deploy to GitHub Pages

### Option A — Publish from a branch (simplest)

1. Create a repository on GitHub, e.g. `humansofcoding.github.io` (a repo named exactly
   `<username>.github.io` is served at the root domain) or any name like `website`.

2. Push these files from this folder:

```bash
git init
git add .
git commit -m "HumansOfCoding website"
git branch -M main
git remote add origin https://github.com/<your-username>/<your-repo>.git
git push -u origin main
```

3. On GitHub: **Settings → Pages → Build and deployment**
   - Source: **Deploy from a branch**
   - Branch: **main**, folder: **/ (root)** → **Save**

4. Wait ~1 minute. Your site is live at:
   - `https://<your-username>.github.io/` if the repo is named `<username>.github.io`
   - `https://<your-username>.github.io/<your-repo>/` for any other repo name

`index.html` must stay in the repository root — Pages serves it as the home page.
`.nojekyll` is already included so GitHub serves every file untouched.

### Option B — Drag and drop (no command line)

Create the repo on github.com → **Add file → Upload files** → drag `index.html`, `style.css`,
`script.js`, `robots.txt`, `sitemap.xml`, `.nojekyll` and the `assets` folder in → **Commit** →
then follow step 3 above.

### After the first deploy: fix the URLs

Four places still say `https://humansofcoding.github.io/`. Replace them with your real URL:

| File | What to change |
|------|----------------|
| `index.html` | `og:url`, `og:image`, `twitter:image`, `<link rel="canonical">`, and the `url` in the JSON-LD block |
| `robots.txt` | the `Sitemap:` line |
| `sitemap.xml` | the `<loc>` line |

Social previews (WhatsApp, Instagram, X) need absolute URLs — relative paths will not show an image.

### Custom domain (optional)

Point your domain's DNS at GitHub Pages, then **Settings → Pages → Custom domain**. GitHub commits a
`CNAME` file for you. Update the URLs above to the new domain and tick **Enforce HTTPS**.

---

## 4. What's already handled

- **Mobile-first** and checked with no horizontal scroll at 375 / 390 / 430 px, tablet and desktop
- **Sticky bottom CTA bar** on phones (Instagram traffic lands on a visible "Book a Free Call")
- **Light + dark theme** with a toggle, remembered per visitor, no flash on load
- **Animations** — scroll reveals, floating doodles, drawn hand-made line art, animated timeline,
  price count-up; every one of them is switched off under `prefers-reduced-motion: reduce`
- **Works without JavaScript** — all content renders, all links still work
- **SEO** — title, meta description, Open Graph, Twitter card, canonical, JSON-LD business schema,
  semantic HTML, one `<h1>`, ordered heading levels
- **Performance** — no libraries, no framework, one small CSS file, one small JS file, all
  illustrations are inline SVG (no image downloads). Only external request: Google Fonts.

### Want an even faster site?

Fonts are the only third-party request. To drop it, delete the three `fonts.g...` lines in
`index.html`; the CSS already falls back to system fonts.

---

## 5. Common edits

| I want to… | Where |
|-----------|-------|
| Change the accent colour | `style.css` → `:root { --accent: #ff5a2c; }` (and `--accent-hover`, `--accent-soft`) |
| Change the MVP price | `index.html` → search `50,000` (appears in the hero badge, MVP section, mobile menu, footer, meta description) |
| Add / remove a service or industry card | `index.html` → `#services` / `#industries` — copy an `<article class="card ...">` block |
| Edit the About text | `index.html` → `#about` |
| Change section order | `index.html` → move whole `<section>` blocks; nav links use the section `id`s |
| Rename a nav item | `index.html` → `.nav__links` **and** `.menu__inner` (desktop and mobile menus) |

---

© 2026 HumansOfCoding.
