# potlucktech-content

Content operations repo for [Potluck Technologies](https://www.potlucktech.com) — drafts, research reports, site assets, and Claude Code skills for the content pipeline.

## Structure

```
drafts/          Blog post drafts (markdown)
reports/         AEO/SEO research reports
site/            Static site assets (llms.txt, etc.)
.claude/skills/  Claude Code skills for the content pipeline
```

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
2. Copy each skill's `CONFIG.example.md` to `CONFIG.md` and fill in values
3. For Google Docs sync: run `/mcp` in Claude Code and authenticate Google Drive

## Collaborators

- [Sha-Mayn Teh](https://www.linkedin.com/in/shamayn/) — Co-Founder, Fractional CTO
- [Yu Chen](https://www.linkedin.com/in/yuchenmit/) — Co-Founder, Fractional CPO
