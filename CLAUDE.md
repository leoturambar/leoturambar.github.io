# CLAUDE.md — Portfolio leoturambar.github.io

Technical reference for anyone working on this repository.

## The site

- Live at: leoturambar.github.io
- Built in: pure HTML/CSS/JS — no Jekyll, no framework, no build step
- Local repo path: Progetti/portfolio/
- One standalone HTML file per page
- Push with: git add . && git commit -m "message" && git push origin main
- Commit messages in English

## Pages

- index.html — homepage
- about.html — extended personal narrative
- experience.html — research background with timeline
- projects.html — four AI projects
- skills.html — technical skills, domain knowledge, certifications
- sitemap.xml — SEO
- robots.txt — SEO
- assets/ — images and media

## Design system

### Palette
- Background: #0d0d0d
- Text: #f0ede8
- Accent: #c8a96e
- Muted: rgba(240, 237, 232, 0.45)
- Border: rgba(240, 237, 232, 0.12)

### Typography
- Display/headings: DM Serif Display (Google Fonts)
- Body: Inter (Google Fonts)
- Size scale defined in :root CSS variables:
  --size-xs through --size-4xl

### Recurring visual patterns
- Section header: accent border-top 1px + label
  (uppercase, tracked) + title
- Page motif: DM Serif Display italic,
  var(--size-2xl), below the header
- Bullet two-column: action verb right-aligned
  in white 200px column, detail in muted 1fr
- Screenshot placeholders: dashed border,
  16/9 aspect ratio, centered filename label

## Navigation

- Fixed nav, hidden on homepage until hero
  scrolls out (is-visible + has-bg classes)
- On all other pages: nav visible immediately
  via DOMContentLoaded script
- Active page: aria-current="page" on the
  relevant nav link, permanent underline via
  CSS [aria-current="page"]::after
- Contact link: href="#contact" on homepage,
  href="index.html#contact" on all others
- Nav links order: About · Experience ·
  Projects · Skills · Contact

## Scroll-based index/timeline

Use getBoundingClientRect approach,
NOT IntersectionObserver:

function getActiveSection(sections) {
  let active = sections[0];
  sections.forEach(function(section) {
    const top = section.getBoundingClientRect()
      .top - 120;
    if (top <= 0) active = section;
  });
  return active;
}

window.addEventListener('scroll',
  updateActive, { passive: true });
updateActive();

Active class: is-active on the corresponding
sidebar/timeline item.

## Layout patterns

### Homepage (index.html)
- .home-wrapper: CSS grid 3fr 2fr
- Left column: hero + positioning sections
- Right column: sticky portrait image
- Right column hidden below 900px

### Projects (projects.html)
- Page grid: sidebar 220px + 1fr content
- Each project: grid-template-columns:
  minmax(auto, 520px) 1fr
- Text left, image right
- Image migrates below text below 900px

### Skills / Experience
(skills.html, experience.html)
- Page grid: 1fr content + 220px sticky index
- Index hidden below 900px

## Rules for AI tools

- No dead code — remove CSS rules for
  elements that no longer exist
- Mobile responsive by default — test at
  900px and 560px breakpoints
- Never overwrite files without showing the
  diff first, unless explicitly told to save
  directly
- Use placeholders for missing assets — note
  the expected filename and location
- All text content in English
- Clean, well-commented HTML/CSS
- One page or section at a time unless
  explicitly told otherwise
- If something sounds wrong or inconsistent
  with the established style, flag it