# Essence Learning — Website

Hugo source for [essencelearning.in](https://essencelearning.in) — an Aviation and Hospitality vocational training institute in Bangalore.

## Tech stack

- **[Hugo](https://gohugo.io/)** static site generator with a custom theme (`themes/el-theme/`)
- **[Tailwind CSS v3](https://tailwindcss.com/)** via Play CDN — no build step needed
- **[Alpine.js v3](https://alpinejs.dev/)** via CDN — mobile nav, accordions, gallery viewer
- **[Font Awesome 6](https://fontawesome.com/)** via CDN — icons
- Deployed to **GitHub Pages** via GitHub Actions

## Local development

Requires Hugo ≥ 0.128. Install from [gohugo.io/installation](https://gohugo.io/installation/).

```bash
cd el_site_new/
hugo server --disableFastRender
```

Open [http://localhost:1313](http://localhost:1313).

## Site structure

```
content/           # Pages and blog posts (Markdown + TOML front matter)
  blog/            # 18 blog posts
  courses.md       # Courses page (data-driven — see data/courses.yaml)
  faq.md           # FAQ page (data-driven — see data/faq.yaml)
  team.md          # Team page (data-driven — see data/team/)
  gallery.md       # Photo gallery
  contact.md       # Contact form
  introcourse.md   # Introductory Pilot Training Course

data/              # Structured content consumed by templates
  courses.yaml     # 8 courses (aviation, hospitality, skills)
  faq.yaml         # 14 FAQ items
  features/        # Homepage features section (6 cards)
  team/            # 12 team member profiles
  testimonials/    # 16 student testimonials

static/
  album/           # Gallery photos (prefix with 000_ to put new photos first)
  courses/         # Downloadable PDFs (ELCourses2018.pdf)
  files/           # Other downloadable files
  img/el/          # Blog banners and logos
  img/team/        # Team member photos
  img/testimonials/# Student testimonial avatars
  introcourse/     # Pilot course brochure pages (3 JPGs)

themes/el-theme/
  layouts/
    partials/      # nav, footer, head, hero, stats, features, testimonials, team, cta-band
    page/          # courses, faq, team, contact, gallery, introcourse
    blog/          # list and single blog templates
    _default/      # baseof, list, single fallbacks

hugo.toml          # All site config — colours, contact details, social links, CTAs
```

## Adding content

**New blog post:**
```bash
hugo new blog/my-post-title.md
```

**New gallery photo:** Copy the image into `static/album/`. Prefix with `000_` to make it appear first.

**Update course details:** Edit `data/courses.yaml` — the courses page regenerates automatically.

**Update FAQ:** Edit `data/faq.yaml`.

## Deployment

Pushing to `main` triggers the GitHub Actions workflow (`.github/workflows/deploy.yml`), which:
1. Installs Hugo
2. Runs `hugo --minify` → outputs to `docs/`
3. Uploads `docs/` as a GitHub Pages artifact
4. Deploys to `https://essencelearning.in`

The `docs/` build output is **not committed** — it is built fresh on every deploy.

## Configuration

All site-wide settings are in `hugo.toml` under `[params]`:

| Key | Purpose |
|-----|---------|
| `logo_nav` | Navbar logo image path |
| `email`, `phone1`, `phone2`, `whatsapp` | Contact details |
| `address_line1–3`, `address_city` | Office address |
| `facebook`, `linkedin` | Social links |
| `hero_headline`, `hero_subtext`, `hero_cta_*` | Homepage hero copy |
| `stat1–4_number/label` | Stats strip numbers |
| `cta_headline`, `cta_button`, `cta_url` | CTA band |
| `forms_endpoint` | Google Apps Script URL for contact form |

## Related

- **[services](../services/)** — Spring Boot contact form backend, Google Apps Script, archived assets (private repo)
