# Execution Plan — Ivana Sánchez (EN/ES) Landing Page (Demo Business)

## What I verified in your workspace (read-only)
- Target deploy folder exists: `public_html/` (this will be the website root on hosting).
- Template source to use: `html/demo-business.html` (+ its related assets under `html/css/`, `html/js/`, `html/images/`, `html/demos/business/`).
- Content inputs available in `raw content/`:
  - Photos: `raw content/images/ivanita 1.jpeg`, `ivanita 2.jpeg`, `ivanita 3.jpeg`
  - Logo: `raw content/images/logo_vectorizado.svg`
  - Copy: `raw content/whatsapp conversation.txt` (English copy provided)
- FTP details (from `ftp info.txt`):
  - Host/IP: `ftp://217.21.76.193` / `ftp://wheat-worm-785534.hostingersite.com`
  - User: `u131837720`
  - Remote upload path: `public_html`

## Current decisions / constraints
- Primary CTA: a contact form that sends an email to Ivana (final recipient email TBD; use placeholders until you confirm).
- Language: site must be easily toggled between English and Spanish.
- Hosting: upload via FTP to remote `public_html/`.

## Goal
Use the **demo-business** template to create a single-person language-services website for Ivana Sánchez, deployed into `public_html/`, with a **clear language toggle (English/Spanish)**.

---

## Step-by-step execution plan

### 1) Create the site skeleton in `public_html/`
1. Copy the demo-business page(s) and required shared assets into `public_html/`:
   - `demo-business.html` → `public_html/index.html` (so the homepage loads at the root)
   - Bring over only the assets actually referenced by the page (CSS/JS/images/fonts/demos/business).
2. Ensure all asset paths work from the new location (no broken `css/`, `js/`, `images/`, `demos/` references).

**Checkpoint:** Opening `public_html/index.html` locally renders correctly (no missing CSS/JS).

### 2) Add brand assets (logo + photos)
1. Create `public_html/assets/` (or reuse existing template folders if cleaner) and place:
   - `logo_vectorizado.svg`
   - the three `ivanita *.jpeg` images
2. Replace the demo logo and hero/section images with Ivana’s logo and photos.

**Checkpoint:** Logo appears in header; at least 1–2 photos used in hero/about sections.

### 3) Adapt structure to “solo translator” services
1. Keep the demo-business layout but swap sections to match the WhatsApp structure:
   - Hero: name + title + credibility line + CTA
   - Services: Translation + Interpretation (two main blocks)
   - Certifications/Credentials: bullets
   - Why choose me: bullets
   - How it works: 3-step process
   - Certified & notarized translations: short explainer
   - Contact CTA: contact form (email-sending) + placeholders for phone/email until confirmed
2. Remove/disable irrelevant sections (e.g., “Agency”, generic “business marketing” wording).

**Checkpoint:** All visible text matches her services; no leftover “business agency” copy.

### 4) Implement bilingual toggle (English/Spanish) — simple, maintainable
**Approach (recommended for a static site):**
1. Store all translatable strings in one file, e.g. `public_html/i18n/translations.js` (or JSON).
2. Mark translatable elements in HTML with keys, e.g. `data-i18n="hero.title"`.
3. Add a small language switch UI in the header:
   - `EN | ES` (or a dropdown)
4. Implement JS to:
   - Switch language dynamically without page reload
   - Persist choice in `localStorage`
   - Default language from browser (`navigator.language`) if no saved preference
   - Update `<html lang="en">` / `<html lang="es">` accordingly

**Checkpoint:** Toggling language updates all main sections + nav labels; refresh keeps the chosen language.

### 5) Spanish copy creation + verification
1. Produce the Spanish equivalent of the WhatsApp English copy (accurate + professional tone).
2. Load both EN + ES into the translation map and verify:
   - Terminology consistency (legal/medical)
   - Title formatting and accents (Sánchez, intérprete, etc.)
   - Length fits the UI (no overflow on mobile)

**Checkpoint:** Full-page EN/ES coverage; no “missing translation” gaps.

### 6) SEO + metadata (light but important)
1. Update:
   - `<title>` and meta description (EN/ES)
   - OpenGraph tags (optional but useful)
   - Favicon/logo references if needed
2. Ensure one canonical index page; language toggling is client-side (acceptable for simple landing pages).

**Checkpoint:** Metadata reflects Ivana + translation services.

### 7) Contact form that emails Ivana
Because FTP/static hosting won’t send email from pure HTML/JS, implement the form using **one** of these approaches:

- **Option A (recommended on typical shared hosting): PHP mail handler**
   - Add `public_html/contact.php` (server-side) that validates fields, applies basic spam protection, and sends mail to a configured recipient.
   - Frontend posts the form to `/contact.php` and shows success/error messages.
   - Use placeholders for recipient email until you confirm it.

- **Option B: Third-party form backend (no server code)**
   - Use Formspree / similar provider; form posts to their endpoint.
   - Requires setting up the service and verifying the recipient email.

**Checkpoint:** Submitting the form shows success and you receive an email (once recipient is set).

### 8) Final local validation
1. Quick manual checks:
   - Mobile nav works
   - CTA opens or scrolls to the contact form
   - Images optimized enough (no huge load times)
2. Confirm no console errors.

**Checkpoint:** Clean load, good performance, no broken links.

### 9) Upload to hosting via FTP into remote `public_html`
1. Connect using provided FTP hostname/IP + username (password is now available in `ftp info.txt`; do not share it in chat/logs).
2. Upload the entire contents of local `public_html/` to remote `public_html/`.
3. Verify live site loads correctly.

**Checkpoint:** Website loads at the domain root, language toggle works live.

---

## Minimal info I still need (but I won’t act until you say “go”)
- Ivana’s destination email address for the contact form (placeholder until you confirm).
- Any required contact details to show (phone, location/service area) — placeholders until you confirm.

If you confirm “go”, I can start with Step 1 (building `public_html/` from `demo-business`) and keep changes minimal and reversible.