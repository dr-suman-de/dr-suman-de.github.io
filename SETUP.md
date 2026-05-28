# Build Your Own Profile Site

A guide to replicating this executive profile site for your own personal or professional brand. No build tools or frameworks required — it is a single HTML file with plain CSS and a handful of vendor libraries.

---

## What This Is

A single-page personal profile built with:

- **Bootstrap 4** — layout and responsive grid
- **Isotope** — filterable speaking/portfolio grid
- **jQuery** — smooth scroll and Isotope initialisation
- **Themify Icons** — icon set (`ti-*` classes)
- **Google Fonts** — Playfair Display (headings) + Inter (body)

All custom CSS lives in a `<style>` block inside `index.html`. There is no build step, no npm, no bundler.

---

## Quick Start

### 1. Fork or copy the repository

```bash
git clone https://github.com/your-speaker/your-speaker.github.io.git
cd your-speaker.github.io
```

Rename the remote to point to your own GitHub repository, then push.

### 2. Rename the repository for GitHub Pages

GitHub Pages serves a repo named `<your-username>.github.io` at `https://<your-username>.github.io/`. Rename the repo accordingly in **Settings → General**.

### 3. Open `index.html`

Everything is in this one file. No compilation needed — open it directly in a browser to preview locally.

---

## Personalising the Content

### Accent colour

Find the `:root` block near the top of the `<style>` section and change `--accent`:

```css
:root {
    --accent: #3B82F6;   /* ← change this to any colour you like */
    --navy:   #0f1923;
    ...
}
```

This single variable controls every highlight, border, button, and icon accent across the entire page.

### Profile photo

Replace `assets/imgs/avatar.jpg` with your own headshot (recommended: square crop, white or neutral background, at least 600 × 600 px).

If you use a different filename, run a find-and-replace for `avatar.jpg` across `index.html`.

### SEO and structured data (`<head>`)

Update the following in order:

| Tag | What to change |
|---|---|
| `<title>` | Your name, title, and organisation |
| `meta name="description"` | One-sentence professional summary |
| `meta name="keywords"` | Your name variants and key topics |
| `meta name="google-site-verification"` | Your own Google Search Console token |
| `link rel="canonical"` | Your site URL |
| `og:*` and `twitter:*` tags | Your name, description, and photo URL |
| JSON-LD `Person` schema | See section below |

### JSON-LD Person schema

The `<script type="application/ld+json">` block tells Google's Knowledge Graph who you are. Replace every field:

```json
{
  "@type": "Person",
  "name": "Your Full Name",
  "givenName": "First",
  "familyName": "Last",
  "honorificPrefix": "Dr.",          ← remove if not applicable
  "alternateName": ["Name Variant 1", "Name Variant 2"],
  "jobTitle": "Your Title",
  "email": "you@example.com",
  "url": "https://yourusername.github.io/",
  "image": "https://yourusername.github.io/assets/imgs/avatar.jpg",
  "worksFor": { "name": "Your Organisation" },
  "alumniOf": [ ... ],
  "sameAs": [ "LinkedIn URL", "Google Scholar URL", ... ]
}
```

### Topnav

```html
<a class="navbar-brand" href="...">Your Name or Blog Title</a>
```

Update the nav links if you rename or remove sections.

### Masthead (hero section)

Search for `sd-masthead` in `index.html`. Replace:

- Eyebrow label
- Name (`sd-mast-name`)
- Title and organisation lines
- Credential chips (`sd-chip`) — delete or update each one
- CTA button URLs (LinkedIn, Google Scholar, etc.)
- Social icon links (`sd-social-link`)

### About section

Replace the two `<p>` bio paragraphs with your own text. Update the four stat chips (years, publications, citations, keynotes) to reflect your numbers.

Update or remove the three offer cards (Research / Product Leadership / Thought Leadership) to match your own value proposition.

### Impact bar

Four numbers displayed on a dark background. Update the `impact-num` values and their `impact-lbl` labels.

### Career timeline

Each role is a `.tl-item` block:

```html
<div class="tl-item">
    <div class="tl-dot"></div>          ← add class="current" for present role
    <div class="tl-period">2022 – Present</div>
    <div class="tl-role">Your Role</div>
    <div class="tl-org">Organisation · Location</div>
    <div class="tl-desc">One or two lines of context.</div>
</div>
```

Add as many `.tl-item` blocks as needed, most-recent first. The current role dot pulses — add `class="tl-dot current"` to it.

### Publications

Each publication is a `.pub-card` block. Four type modifier classes control the top border and badge colour:

| Class | Colour | Use for |
|---|---|---|
| `pt-journal` | Blue | Journal articles (IEEE Transactions, etc.) |
| `pt-conf` | Teal | Conference papers |
| `pt-other` | Purple | Other academic venues |
| `pt-industry` | Orange | Industry or practitioner publications |
| `pt-bib` | Dark navy | Full bibliography / "see all" card |

Example:

```html
<div class="pub-card pt-journal">
    <div class="pub-venue">IEEE Transactions on AI · Oct 2024</div>
    <div class="pub-title">Your Paper Title</div>
    <div class="pub-meta">
        <span class="pub-badge">Journal</span> Co-authors · DOI
    </div>
    <a href="https://doi.org/..." target="_blank" class="text-accent">View paper →</a>
</div>
```

### Speaking / Portfolio (Isotope grid)

Each item needs a `filter-*` class for Isotope filtering and a matching filter button:

```html
<!-- Filter button -->
<a href="#" data-filter=".filter-keynote">Keynote</a>

<!-- Portfolio item -->
<div class="col-md-4 portfolio-item filter-keynote">
    ...
</div>
```

Add or remove filter categories to match your speaking history.

### Education

Each degree is an `.edu-card` block:

```html
<div class="edu-card">
    <div class="edu-degree">Degree Name</div>
    <div class="edu-school">Institution · Location</div>
    <div class="edu-meta">Year range · GPA or grade</div>
</div>
```

### Skills and certifications

Skills use `.skill-tag` pills — add `class="ft"` to highlight featured ones. Certifications use `.cert-item` cards; link each `cert-name` to the badge URL on Credly or the issuer.

### Achievements

Each achievement is an `<li>` inside `.ach-list`. Update the four `.stat-chip` numbers at the top of the section.

### Contact section

Update the email address (appears twice — once as a `mailto:` href and once as display text), location, and social links.

---

## Sitemap and robots.txt

Update `sitemap.xml` with your URL and today's date:

```xml
<loc>https://yourusername.github.io/</loc>
<lastmod>YYYY-MM-DD</lastmod>
```

Update `robots.txt` with your sitemap URL:

```
Sitemap: https://yourusername.github.io/sitemap.xml
```

---

## Deploying to GitHub Pages

1. Push `index.html` and all assets to the `main` (or `master`) branch of `<yourusername>.github.io`.
2. In the repository **Settings → Pages**, set the source to the root of the `main` branch.
3. GitHub will publish the site at `https://<yourusername>.github.io/` within a minute or two.

---

## Verifying with Google Search Console

1. Go to [Google Search Console](https://search.google.com/search-console) and add your site URL as a property.
2. Choose **HTML tag** verification. Copy the `content` value from the meta tag provided.
3. Replace the `google-site-verification` content value in `index.html` with your own token.
4. Push the change, then click **Verify** in Search Console.
5. Submit your sitemap URL under **Sitemaps**.

---

## File Structure

```
your-site/
├── index.html          ← everything lives here
├── sitemap.xml
├── robots.txt
├── assets/
│   ├── imgs/
│   │   └── avatar.jpg  ← replace with your photo
│   ├── css/
│   │   └── johndoe.css ← base template CSS (do not modify)
│   └── vendors/
│       ├── jquery/
│       ├── bootstrap/
│       ├── isotope/
│       └── themify-icons/
```

---

## Tips

- **All customisation goes in `index.html`** — do not modify `johndoe.css` or vendor files.
- **One accent colour controls everything** — changing `--accent` in `:root` is the fastest way to rebrand.
- **Keep `class="navbar"` on the `<nav>` tag** — jQuery's smooth scroll selector depends on it.
- **Keep `.portfolio-container` and `.filters`** — Isotope's initialisation in `johndoe.js` depends on these class names.
- After pushing to GitHub Pages, run your URL through [Google's Rich Results Test](https://search.google.com/test/rich-results) to verify the JSON-LD Person schema is being parsed correctly.
