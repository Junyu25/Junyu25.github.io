# Better Options for Hosting Your Personal Website on GitHub

*Research report — June 12, 2026*

## TL;DR

Yes, there are clearly better options. Your current setup (Hexo 5.0.2 + Butterfly, last content update Nov 2020, deployed by pushing pre-built HTML) is both stale and fragile — and critically, **the Hexo source files are not in this repo**, so any path forward involves rebuilding the site from recovered content.

**Recommendation: al-folio (Jekyll academic theme) deployed via GitHub Actions**, with **Hugo Blox Academic CV** as the runner-up if you want a true parallel English/Chinese site, and **Quarto** if computational-notebook publishing becomes your priority. Details and trade-offs below.

---

## 1. Current state of your site

| Aspect | Finding |
|---|---|
| Generator | Hexo 5.0.2 (current Hexo is 7.x; Butterfly theme now requires newer setups) |
| Theme | Butterfly (still actively maintained — 8.3k★, v5.5.5 released June 2026) |
| Source files | **Not in this repo** — only generated HTML. No `source` branch exists. |
| Content | 13 posts (2018–2020, mixed English/Chinese), CV, Research, BioSoft, About pages |
| Deployment | Manual: build locally, push HTML. No GitHub Actions. |
| Last activity | Content: Nov 2020. Last commit: Nov 2021 (deleted CNAME). |

### Content recovery is feasible ✅

I verified locally that post content extracts cleanly from the generated HTML — each post's body sits in a well-defined `#article-container` div (Butterfly's standard layout), and **all images (12 MB) are already in this repo's `/img/` directory**. Converting the 13 posts + 4 pages back to Markdown is a scriptable, low-risk task (an afternoon of work, mostly review). Code blocks, headings, and links survive the round-trip; only Hexo-specific shortcodes (if any were used) would need manual touch-up.

---

## 2. The hosting model itself should change

Regardless of which generator you pick, the modern best practice on GitHub is:

> **Source repo (Markdown) → GitHub Actions builds on every push → deploys to GitHub Pages**

You write Markdown, commit, push — and never run a build tool locally again. This directly fixes the failure mode that killed your current site: the build environment lived only on one machine, and when the source was lost, the site froze in 2020.

GitHub Pages limits are a non-issue for you: 1 GB site size (yours is 26 MB), soft 100 GB/month bandwidth, and custom Actions workflows aren't subject to the 10-builds/hour soft limit. Cloudflare Pages or Netlify could serve the same repo with slightly better global CDN performance, but for a personal academic site GitHub Pages is the simplest option with the fewest accounts to maintain — no reason to leave.

---

## 3. Candidate evaluation

All figures verified against the primary GitHub repos / docs during this session (June 2026).

| | **al-folio** | **academicpages** | **Hugo Blox Academic CV** | **Quarto website** | **AstroPaper (Astro)** | **Hexo 7 + Butterfly (rebuild)** |
|---|---|---|---|---|---|---|
| Framework | Jekyll | Jekyll | Hugo | Quarto (Pandoc) | Astro | Hexo |
| Stars / activity | 15.7k★, v1.0 June 2026, 4 maintainers | 17.1k★, v0.8.4 June 2025 | 9.5k★ (builder), v0.12.0 Apr 2026 | 5.7k★ (CLI), v1.9 May 2026, backed by Posit | 4.7k★, v6.1 June 2026 | Theme 8.3k★, active |
| Publications from BibTeX | ✅ automatic | ⚠️ via TSV/notebook scripts | ✅ BibTeX/DOI auto-import | ⚠️ manual listings/citations | ❌ blog-only | ❌ |
| CV page | ✅ RenderCV/JSONResume → auto PDF | ✅ | ✅ | ⚠️ build your own page | ❌ | ❌ |
| Math (MathJax/LaTeX) | ✅ | ✅ | ✅ native | ✅ native | ⚠️ via plugins | ⚠️ via plugins |
| Jupyter/R notebooks | ⚠️ Jupyter display support | ⚠️ generator scripts only | ✅ publish `.ipynb` as posts | ✅✅ first-class (its core purpose) | ❌ | ❌ |
| Mixed EN/ZH posts in one feed | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| True parallel EN/ZH site (i18n) | ❌ not supported | ❌ not supported | ✅ Hugo native multilingual, zh included | ⚠️ third-party (babelquarto) | ✅ i18n-ready | ⚠️ plugin-based |
| GitHub Actions deploy | ✅ included | ✅ included | ✅ included | ✅ official action (`quarto-actions/publish@v2`) | ✅ standard Astro action | ⚠️ DIY workflow |
| Maintenance burden | Low (template + Actions; Ruby deps handled in CI) | Low–medium (older codebase) | Low–medium (single Hugo binary; **history of breaking renames**: Academic→Wowchemy→Hugo Blox; growing commercial layer) | Low (one tool, no theme fork) | Medium (npm ecosystem churn) | Medium + you'd rebuild everything anyway |

### Notes on each

- **al-folio** — The de-facto standard academic theme. Hit v1.0 this month, has a dedicated maintainer team, and is purpose-built for exactly your profile: auto-generated publications page from a `.bib` file, CV page from JSON/YAML with PDF export, projects, teaching, news, dark mode, MathJax. You create it via GitHub's "use this template," fill in YAML + Markdown, and the bundled Actions workflow does everything. Its one real gap is no official multilingual mode — but your current site doesn't have one either; it mixes EN and ZH posts in a single feed, which al-folio handles fine.
- **academicpages** — More stars but an older, plainer codebase (last release June 2025, actively seeking maintainers). al-folio is the stronger pick in the same Jekyll niche.
- **Hugo Blox Academic CV** — Feature-rich and the only candidate with first-class parallel EN/ZH support (Hugo's native multilingual mode; Chinese translations and a Chinese README ship with the project). Also publishes Jupyter notebooks as posts. The caution: the project has been renamed twice (Academic → Wowchemy → Hugo Blox) with breaking migrations each time, and is increasingly oriented around a commercial CMS (Ownable) — a long-term churn risk that cuts against your "minimal maintenance" goal.
- **Quarto** — Open-source scientific publishing system from Posit (the RStudio company). As a bioinformatician, this is the most interesting wildcard: `.ipynb` and `.qmd` files render natively, with citations, cross-references, and an official GitHub Action (with `freeze` so CI never re-executes your analyses). But academic-profile features (publications page, CV) are build-it-yourself, and multilingual needs the third-party `babelquarto` package.
- **AstroPaper / Astro** — Modern and fast, but blog-only; no academic features. Wrong shape for your needs.
- **Rebuilding on Hexo 7** — Butterfly is still actively maintained, so this is viable, but since your source is lost you'd be rebuilding from scratch anyway — and Hexo has no academic features (publications, CV). No advantage over switching.

---

## 4. Recommendation

**Primary: al-folio.** It matches all four of your constraints best:

1. **Academic profile + blog** — publications from BibTeX, CV with PDF export, projects, and a blog, all out of the box.
2. **Minimal maintenance** — "use this template" repo + included GitHub Actions; you only ever touch Markdown, YAML, and your `.bib` file. Largest community (15.7k★) means problems are already answered in its issues/FAQ.
3. **Bilingual content** — handles your existing mixed EN/ZH post stream exactly as your current site does.
4. **Bioinformatics extras** — MathJax, code highlighting, Jupyter notebook display, Mermaid diagrams.

**Choose Hugo Blox Academic CV instead** if you decide you want a genuinely parallel Chinese/English site (separate `/zh/` tree with a language switcher) — that's its decisive advantage, weighed against its rename/commercialization churn.

**Keep Quarto in mind** if your site's center of gravity shifts toward publishing computational analyses (R/Python notebooks as posts). It's also reasonable to start with al-folio now and later embed Quarto-rendered notebooks as individual pages.

---

## 5. Suggested migration outline (follow-up task, ~1 day total)

1. **Recover content** (~2–3 h): script the extraction of the 13 posts + About/Research/BioSoft pages from `#article-container` HTML into Markdown with front-matter (title, date, tags, lang); copy `/img/` assets. Manual review of each post.
2. **Create the new site**: generate a private working repo from the al-folio template; fill in `_config.yml`, bio, CV data, and a `papers.bib` with your publications.
3. **Port content**: drop recovered Markdown into `_posts/`; rebuild CV/Research as al-folio pages.
4. **Deploy**: point the repo at `Junyu25/Junyu25.github.io` (replacing this one — the old HTML is preserved in git history), enable GitHub Pages with the Actions workflow.
5. **Preserve URLs** (optional, ~30 min): your post URLs are `/posts/<id>/`; add `redirect_from` entries (jekyll-redirect-from, bundled with al-folio) so old links keep working.

---

## Sources

- [al-folio repo](https://github.com/alshedivat/al-folio) and [README](https://github.com/alshedivat/al-folio/blob/main/README.md)
- [academicpages repo](https://github.com/academicpages/academicpages.github.io)
- [Hugo Blox builder repo](https://github.com/HugoBlox/hugo-blox-builder) and [Academic CV template](https://github.com/HugoBlox/theme-academic-cv)
- [Quarto CLI repo](https://github.com/quarto-dev/quarto-cli) and [GitHub Pages publishing docs](https://quarto.org/docs/publishing/github-pages.html)
- [babelquarto (multilingual Quarto)](https://github.com/ropensci-review-tools/babelquarto)
- [AstroPaper repo](https://github.com/satnaing/astro-paper)
- [hexo-theme-butterfly repo](https://github.com/jerryc127/hexo-theme-butterfly)
- [GitHub Pages limits](https://docs.github.com/en/pages/getting-started-with-github-pages/github-pages-limits)
