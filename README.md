# TTConnect — Website Assets

Production-ready static files for **ttconnect.us**, hosted on GoDaddy.

## What's in this folder

```
site/
├── index.html        ← Home (landing page)
├── leagues.html      ← Leagues directory (Coming Soon)
├── clubs.html        ← Clubs directory (Coming Soon)
├── about.html        ← About / mission / contact
├── privacy.html      ← Privacy policy
├── 404.html          ← Custom not-found page
├── robots.txt        ← Search engine permissions
├── sitemap.xml       ← For Google Search Console
└── assets/
    ├── styles.css    ← All page styles
    ├── main.js       ← Nav toggle, filter chips, smooth scroll
    └── favicon.svg   ← Site icon
```

No build step. No dependencies. Pure HTML / CSS / JS — the simplest possible thing to drop into GoDaddy.

## How to upload to GoDaddy

### Option A — cPanel File Manager (most common)

1. Log in to GoDaddy → **My Products** → **Hosting** → **Manage** on your ttconnect.us plan.
2. Open **cPanel** (or "Web Hosting Dashboard" depending on plan).
3. Open **File Manager**.
4. Navigate into `public_html/` (this is your domain's web root).
5. If anything is already in there (e.g. a default `index.html` from GoDaddy), select it and **delete** it.
6. Click **Upload**.
7. Upload **the contents of this `site/` folder** — NOT the `site/` folder itself. That means:
   - `index.html`, `leagues.html`, `clubs.html`, `about.html`, `404.html`, `robots.txt`, `sitemap.xml` go in `public_html/`
   - The `assets/` folder goes in `public_html/assets/`
8. Once uploaded, visit https://ttconnect.us — `index.html` is loaded automatically.

### Option B — Drag-and-drop with FTP (FileZilla, Cyberduck, etc.)

1. In GoDaddy cPanel, create an FTP account if you don't already have one (cPanel → **FTP Accounts**).
2. Connect your FTP client using the credentials shown.
3. Navigate to `/public_html/` on the server.
4. Drag the **contents** of this `site/` folder into `public_html/` (same as above — don't drag the folder itself, drag what's inside).

### Option C — GoDaddy Website Builder (NOT recommended)

If your plan is "Website Builder" instead of cPanel hosting, you can't upload HTML directly. You would need to either:
- Upgrade to a cPanel / Linux hosting plan, or
- Recreate the design inside the Website Builder.

Hosting plans that support direct HTML upload are usually called **Web Hosting**, **Linux Hosting**, or **WordPress Hosting** (the underlying cPanel is the same).

## Setting up the 404 page

GoDaddy uses `.htaccess` to map custom error pages. Once your files are uploaded, also create a file called `.htaccess` in `public_html/` with this single line:

```
ErrorDocument 404 /404.html
```

(File manager → New File → `.htaccess`. If you don't see existing `.htaccess` files, enable "Show Hidden Files" in File Manager → Settings.)

## Forcing HTTPS (recommended)

GoDaddy plans usually include a free SSL certificate. After it's active (Hosting → Manage → SSL), add this to `.htaccess` to force every visitor onto HTTPS:

```
RewriteEngine On
RewriteCond %{HTTPS} !=on
RewriteRule ^ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]

ErrorDocument 404 /404.html
```

## After upload — sanity check

- [ ] https://ttconnect.us loads the home page
- [ ] https://ttconnect.us/leagues.html loads
- [ ] https://ttconnect.us/clubs.html loads
- [ ] https://ttconnect.us/about.html loads
- [ ] Visiting a bad URL (e.g. https://ttconnect.us/nope) shows the custom 404
- [ ] The favicon (orange ball on green) appears in the browser tab
- [ ] On mobile, the hamburger menu in the top right opens the nav

## What works right now

- **Visual design** — full responsive layout, hero, stats, featured leagues, US map, event feature, player spotlight, signup form.
- **Navigation** — header, footer, all pages link to each other.
- **Filter chips** — visually active state (UI demo; doesn't filter real data yet).
- **Newsletter form** — pretends to submit (shows "Sent ✓"). Wire to your email provider before launch.
- **Contact links** — all `mailto:` links route to `ttconnectadmin@gmail.com` with pre-filled subject lines for routing (e.g. "List my club", "Press inquiry").

## What's mocked & needs real data later

- **`clubs.html` is intentionally a "Coming Soon" page** with a waitlist signup. Replace it with a real directory once the verified club list is ready.
- League listings on `leagues.html` (currently 12 example leagues)
- Stats numbers on the home page (320 clubs, 68 leagues, etc.)
- The US map markers (illustrative cluster only)
- Player spotlight quote

These are wired up as plain HTML — when you have real data, edit the relevant `.html` file by hand, or migrate to a CMS / database later.

## Updating fonts, colors, copy

- **Colors** live as CSS variables at the top of `assets/styles.css` (`--forest`, `--orange`, `--cream`, etc.).
- **Fonts** are loaded from Google Fonts in each `.html` `<head>`. Swap by changing the `<link>` and the `--display` / `--body` / `--mono` variables.
- **Copy edits** — open the `.html` file in any text editor and edit directly. Save → re-upload that file to `public_html/`.

## Questions / handoff notes

- The site is fully static — no database, no PHP, no Node. It will be cheap to host and impossible to break.
- Page weight is ~25KB per page (plus ~30KB of CSS, cached). Google Fonts adds the only external dependency.
- Designed mobile-first; tested at 360px, 768px, 1024px, 1440px+.

— Built with care, May 2026
