# goodmarklabs.com

Static website for Goodmark Labs, the trading name of Goodmark Limited. Plain HTML and CSS, no build step, no analytics. The only JavaScript is a few lines for the light/dark toggle, which remembers the choice in the browser's localStorage and sends nothing anywhere. The password reset page is the one exception: its script sends the new password to Firebase Authentication, and nothing else.

## Layout

| Path | Page |
| --- | --- |
| `index.html` | Home: who we are, products, contact |
| `pocket-lyrics/index.html` | Pocket Lyrics product page |
| `pocket-lyrics/support/index.html` | Support and FAQ |
| `pocket-lyrics/privacy/index.html` | Privacy Policy |
| `pocket-lyrics/terms/index.html` | Terms of Use |
| `pocket-lyrics/delete-account/index.html` | Account deletion instructions (Google Play "account deletion URL") |
| `pocket-lyrics/reset-password/index.html` | Password reset page, Firebase's custom action URL (not linked or indexed; see below) |
| `404.html` | Not-found page, served by GitHub Pages for any missing address |
| `.github/workflows/pages.yml` | Publishes the site files to GitHub Pages on every push to `main` |
| `assets/site.css` | All styles, light and dark via `prefers-color-scheme` plus the toggle |
| `assets/fonts/` | Self-hosted Bricolage Grotesque (headings) and Instrument Sans (text), latin subsets, from Google Fonts (OFL licence) |
| `assets/logo.svg`, `assets/favicon.svg` | Goodmark logo and mark |
| `assets/pocket-lyrics-icon-*.png` | Pocket Lyrics app icon, copied from the app project |
| `assets/img/` | Product images as WebP (640, 960, 1280 and 1664 px wide) with JPEG fallbacks (640 and 1280 px), all cropped to 16:9 |
| `_source/` | The original PNGs the product images were made from. Not linked from any page; safe to leave out of a deploy |
| `assets/`, `favicon.ico` | Other icons |
| `robots.txt`, `sitemap.xml` | Search engine hints |

Clean URLs work because every page is a folder containing `index.html`. Links use absolute paths (`/pocket-lyrics/privacy/`), so the site must be served from the root of the domain, not a subfolder.

## Before publishing

No placeholders remain. The effective date on the privacy, terms and delete-account pages is 5 November 2026; change a page's date whenever its text changes.

The source drafts for the legal pages live in the Pocket Lyrics project at `docs/website/*.md`. Keep both in sync.

## Replacing a product image

Put the new image in `_source/`, then regenerate the sizes in `assets/img/` (16:9 crop, WebP at 640/960/1280/1664 wide, JPEG at 640/1280) and keep the same file names so the pages pick them up without edits.

## Password reset page

Firebase sends every account email's link here, with `mode`, `oobCode` and `apiKey` in the address, so no key is stored in this repository. The page calls Firebase's `accounts:resetPassword` API directly and loads no third-party scripts. Its 8-character minimum matches the app. It isn't in `sitemap.xml` and is marked `noindex`. The custom action URL is set in the Firebase console under Authentication > Templates, and applies to every email template.

## Previewing locally

Absolute links need a web server rather than opening the files directly. From this folder:

    python3 -m http.server 8000

then open http://localhost:8000 in a browser.

## Publishing

The site is in the public GitHub repository `Goodmarklabs/goodmark-website` and is served by GitHub Pages. On every push to `main`, the workflow in `.github/workflows/pages.yml` copies only the site files (pages, `assets/`, `favicon.ico`, `robots.txt`, `sitemap.xml`) into the deployment, so this README, CLAUDE.md, the workflow itself and `_source/` are never served. Deploying is: commit, then push. The custom domain goodmarklabs.com is set in the repository's Pages settings; `www.goodmarklabs.com` redirects to it.

`_source/` and `.DS_Store` are ignored by git.
