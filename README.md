# Ivana Sánchez — Language Services Website (EN/ES)

Static website project built from the **Crafto** template (`demo-business`) and prepared for deployment to shared hosting under `public_html/`.

## Project layout

- `public_html/` — **Deploy this folder** to your hosting (server web root).
- `html/` — Original Crafto template source (reference only).
- `raw content/` — Provided assets and copy from Ivana (inputs).
- `plan.md` — Step-by-step execution plan for building/customizing the site.

## Current status

- `public_html/` contains the staged **demo-business** template.
- Ivana’s images/logo have been copied into `public_html/images/`.

## Local preview (simple)

You can preview with any static server. From repo root:

```bash
cd public_html
python3 -m http.server 8080
```

Then open `http://localhost:8080`.

## Local development (template tooling)

The Crafto template includes a Gulp pipeline under `html/`.

```bash
cd html
npm install
npm run start
```

Note: this is optional for the deployed site. The deployed site lives in `public_html/`.

## Deployment

Upload the **contents** of `public_html/` to the remote `public_html/` directory on your hosting.

### Automated FTP deploy (recommended)

This repo includes a small script that deploys `./public_html` to your FTP hosting using `lftp`:

```bash
./upload_deploy --help
```

Install dependency (Ubuntu/Debian):

```bash
sudo apt-get update
sudo apt-get install -y lftp
```

Required environment variables:

- `FTP_HOST` (example: `wheat-worm-785534.hostingersite.com`)
- `FTP_USER`
- `FTP_PASS`

Optional environment variables:

- `FTP_REMOTE_PATH` (default: `public_html`)

Examples:

- Dry run (shows what would change):

```bash
FTP_HOST=... FTP_USER=... FTP_PASS=... ./upload_deploy --dry-run
```

- Normal deploy (uploads changed/newer files only):

```bash
FTP_HOST=... FTP_USER=... FTP_PASS=... ./upload_deploy
```

- Full sync (also deletes remote files not present locally):

```bash
FTP_HOST=... FTP_USER=... FTP_PASS=... ./upload_deploy --delete
```

Important:
- Do **not** commit or publish FTP credentials.
- Keep `ftp info.txt` out of version control (recommended: add it to `.gitignore`).

## Bilingual requirement (English / Spanish)

End goal: site content must be easily toggleable between English and Spanish.

Implementation approach (planned):
- Mark translatable text in HTML with keys (e.g., `data-i18n="hero.title"`).
- Store translations in a single `public_html/i18n/translations.js`.
- Add a header toggle (`EN | ES`) that:
  - switches language without reload
  - persists in `localStorage`
  - defaults from `navigator.language`.

## Contact form requirement

Primary CTA is a **contact form that sends an email** to Ivana.

Because static HTML/JS cannot send email directly, the plan is one of:
- **PHP handler** on hosting (recommended if PHP is available), e.g. `public_html/contact.php`.
- **Third-party form backend** (Formspree or similar).

Recipient email address is currently a placeholder until confirmed.

## Security / privacy notes

- Don’t commit passwords or private contact details.
- If you add a server-side mail handler, validate inputs and add basic spam protection (honeypot / rate-limit).
