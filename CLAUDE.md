# Goodmark website

Static site for goodmarklabs.com: plain HTML and CSS, no build step. See README.md for the folder layout.
The live site deploys automatically from the `main` branch of github.com/Goodmarklabs/goodmark-website via GitHub Pages (workflow in `.github/workflows/pages.yml`, which publishes only the site files).

## Rules

- **Push after every commit.** Run `git push` straight after each `git commit` on `main`. GitHub Pages publishes from `main`, so an unpushed commit is an undeployed change.
- Never add analytics, cookies, trackers or third-party scripts. Fonts are self-hosted in `assets/fonts/`.
- The legal pages (`pocket-lyrics/privacy`, `terms`, `delete-account`) have Markdown twins in the Pocket Lyrics project at `docs/website/`. Change both, and update the effective date when the text changes.
- Show no street address or phone number anywhere. Contact is "Goodmark Labs (Goodmark Limited, New Zealand)" and support@goodmarklabs.com (admin@goodmarklabs.com for business).
- `_source/` holds the original product images (ignored by git). Regenerate `assets/img/` from them: 16:9 crop, WebP at 640/960/1280/1664 px, JPEG at 640/1280 px, same file names.
- Pull (`git pull --ff-only`) before editing: the Pocket Lyrics project also commits here (legal pages, reset-password page).
- Delete files only by exact name, after listing them; never wildcard-delete in this folder.
