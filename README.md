# potlucktech-content

Content operations repo for [Potluck Technologies](https://www.potlucktech.com) — drafts, research reports, site assets, and Claude Code skills for the content pipeline.

## Structure

```
drafts/          Blog post drafts (markdown)
reports/         AEO/SEO research reports
site/            Static site assets (llms.txt, etc.)
docs/            Brand context + published assets (see below)
CLAUDE.md        Company/brand context for Claude Code
.claude/skills/  Claude Code skills for the content pipeline
```

### docs/

```
docs/background.md          Founder + company background
docs/tone-guide.md          Voice, tone, and 8 audience personas
docs/testimonials/          Case-study writeups + social thumbnails
docs/workshops/             Workshop landing assets (e.g. AI Agents 101)
docs/thumbnail-template/    Reusable 1800x1000 thumbnail template
```

## Thumbnails

Social/case-study thumbnails are authored as self-contained HTML and rendered
to PNG with headless Chrome (1800x1000). Shared type/layout lives in
`docs/thumbnail-template/_TEMPLATE.html`; copy it plus a `bg.png`, edit the
eyebrow/title/subtitle and the bottom block (meta line or stat cards), then:

```
"/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" \
  --headless --disable-gpu --hide-scrollbars \
  --force-device-scale-factor=1 --window-size=1800,1000 \
  --screenshot="out.png" "file://$PWD/<file>.html"
```

All PNGs are git-ignored (`*.png`) — including background sources like `bg.png`.
Commit the HTML; share/regenerate background images out of band, or un-ignore a
specific one with `git add -f path/to/bg.png` if a clone needs it to render.

## Content Pipeline Skills

| Skill | Purpose |
|---|---|
| `aeo-topic-research` | Discovers AEO opportunities — questions AI engines answer in our niche, competitor citations, content gaps |
| `aeo-content-writer` | Writes AEO-optimized blog post drafts from research briefs |
| `aeo-seo-site-audit` | Audits pages for content quality, schema markup, and AEO readiness |
| `seo-keyword-research` | Competitive keyword analysis and gap identification |
| `distribute-social` | Drafts Reddit and LinkedIn distribution for published posts |
| `distribute-outreach` | Backlink and citation outreach for published posts |
| `growth-pm` | Coordinates the full pipeline, maintains task board, routes work to the right skill |

## Setup

1. Clone the repo
2. Run aeo-topic-research skill to generate new blog post ideas
3. Run aeo-content-writer skill to generate a specific post (use blog post brief in reports/)
4. Editing of blog post is in this Google Doc: https://docs.google.com/document/d/1AHZs4K0fBiDmIpasrmVg4TepJHRxauXcdHldNEvX-Zw/edit?tab=t.0

## Collaborators

- [Sha-Mayn Teh](https://www.linkedin.com/in/shamayn/) — Co-Founder, Fractional CTO
- [Yu Chen](https://www.linkedin.com/in/yuchenmit/) — Co-Founder, Fractional CPO
