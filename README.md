# Emmanuel Martínez — Academic Website

Personal academic website built with [al-folio](https://github.com/alshedivat/al-folio) and hosted on GitHub Pages.

## Local development

```bash
bundle install
npm ci
bundle exec jekyll serve
```

The site is available at `http://localhost:4000` while the development server is running.

## Content

- `_pages/` contains the main pages.
- `_projects/` contains research project profiles.
- `_bibliography/papers.bib` generates the publications list.
- `_news/` contains homepage announcements.
- `_data/socials.yml` and `_data/repositories.yml` configure external profiles and code repositories.
