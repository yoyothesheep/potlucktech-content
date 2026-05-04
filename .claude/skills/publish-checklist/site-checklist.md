# Site Checklist — ai-proof-careers.com

## Page Type Detection

- Numeric input → blog post
- `YYMMDD-` prefix → now article
- Matches an industry slug → industry page
- Otherwise → career page

## Automated Script

```bash
python3 scripts/publish_check.py <slug|post-number|now-id> --sitemap <SITEMAP_PATH>
# --network / -n  also verify source URLs (slow)
# --build  / -b   also run npm run build
```

The script automatically checks: file existence, registry, required fields, field counts, slug format, sitemap (URL, lastmod, changefreq, priority), dates (ISO format), em-dashes, placeholders (TODO/TBD/Lorem/[insert]/PLACEHOLDER), external link attributes, FAQ question format, superlatives/fear phrases (now articles), and source URL resolution (with `--network`).

## JSON-LD Schema Map

- Blog posts: `Article` + `FAQPage`
- Career pages: `Guide` + `Occupation` + `FAQPage`
- Industry pages: `Guide` + `FAQPage`
- Now articles: no structured schema required

---

## Phase 2A: Blog Post

### Files
- Post component: `src/views/blog/PostN.tsx`
- Blog index entry: `src/views/Blog.tsx` POSTS array
- Route page: `app/blog/[slug]/page.tsx`

### Automated (verify script pass)
- [ ] Slug format: `/blog/[N]-[kebab-case]`
- [ ] POSTS array entry: `faqQuestion` ends with `?`, `faqAnswer` ≤2 sentences
- [ ] Route exports `metadata` with title, description, `alternates.canonical`
- [ ] Dates: `publishedDateISO` is valid ISO format; `editedDateISO` present and valid if this is an update

### Manual
- [ ] `editedDate` / `editedDateISO` updated to today if this is an edit
- [ ] Sources: 3+ high-authority (BLS, O*NET, gov agencies, peer-reviewed); each has a working external link + `id="source-N"` anchor; specific stats in prose traceable to a cited source
- [ ] Cross-post: any referenced posts exist and are published; `faqAnswer` accurately reflects actual post content
- [ ] AEO/SEO audit: run steps 7–9 of `/aeo-seo-site-audit` (Schema Validation, Content Quality, Authority & Citability) directly on the post component; fix all 🔴 Critical issues (do not save audit report to file)

### Summary

| Check | Status | Notes |
|-------|--------|-------|
| Blog index entry | | |
| SEO & metadata | | |
| JSON-LD (Article + FAQPage) | | |
| Sitemap | | |
| Dates | | |
| Formatting | | |
| Sources & citations | | |
| Cross-post consistency | | |
| Accessibility & mobile | | |
| Build | | |
| AEO audit | | |

---

## Phase 2B: Career Page

### Files
- Data file: `src/data/careers/[slug].tsx`
- Route: `app/career/[slug]/page.tsx`
- Layout (read-only): `src/components/CareerDetailPage.tsx`

### Automated (verify script pass)
- [ ] Data file exists and exports `CareerData` with all required fields: `title`, `score`, `salary`, `openings`, `growth`, `description`, `jobTitles`, `keyDrivers`, `risks`, `opportunities`, `howToAdapt`, `taskData`, `careerCluster`
- [ ] Route exists, imports `getCareerMetadata`, exports `metadata`
- [ ] Slug in `CAREER_PAGE_SLUGS` (`src/data/careerPageRegistry.ts`)
- [ ] `taskData` 5+ entries, `careerCluster` spans 3+ levels
- [ ] Sources linked: `statSourceName` count == `statSourceUrl` count; `attribution` count == `sourceUrl` count minus `isEmerging:true` count; `sourceName` count == `isEmerging:true` count

### Manual — CareerData fields
- [ ] `description`: one concise sentence (shown in page header, not a paragraph)
- [ ] `jobTitles[]`: includes all O*NET sample job titles for this occupation
- [ ] `keyDrivers`: 2–4 sentences, no em-dashes
- [ ] `careerCluster` nodes: `steps[]` are concrete and actionable (specific course/tool/cert — not "learn Python"); `isEmerging: true` nodes have `description`, `core_tools`, `stat`, `fit`, `steps` all filled

### Manual — Sources & SEO
- [ ] Sources live in three places (no top-level `sources[]` array; `sources?: Source[]` is optional/unused):
  - `statSourceName`/`statSourceUrl` on risks and opportunities stat blocks
  - `attribution`/`sourceUrl`/`sourceDate` on each `howToAdapt.quotes[]` entry
  - `sourceName`/`sourceTitle`/`sourceDate`/`sourceUrl` in each `careerCluster` emerging node's `stat` object
- [ ] Title follows template: `[Job Title] Career Guide: AI Risk, Salary & Next Steps`
- [ ] Description follows template: `[Job Title] scores [score]/100 on AI resilience — [tier] territory. See which tasks AI already automates, how salaries are holding, and which adjacent roles offer better protection.`
- [ ] Canonical resolves to `https://www.ai-proof-careers.com/career/[slug]`

### Manual — Source Audit
- [ ] Open rendered page in browser; click every inline `[Name, Date]` citation — confirm correct destination (not homepage or redirect)
- [ ] Click every quote attribution link — confirm it reaches the **specific article**, not a 404, redirect, or generic homepage (e.g. `hbr.org/` alone is not acceptable — must link to the exact article)
- [ ] Unlinked quote attributions (plain text, no link) = blank `sourceUrl` → fix in card JSON
- [ ] For WEF, McKinsey, Deloitte, ACM, HBR citations: manually search the article title to confirm it exists (these domains block bots — `generate_career_pages.py` prints `⚠ MANUAL CHECK` for these)
- [ ] Run `python3 scripts/generate_career_pages.py --code <CODE> --force` and confirm no `⚠` warnings printed; if warnings appear, fix in card JSON and re-run
- [ ] **Any patched sourceUrl must be opened in a browser and confirmed before the card is regenerated.** Do not assume a URL is correct because it follows a known site pattern — patch → verify → regenerate, in that order.

### Manual — Mobile layout
- [ ] Career map: detail panel opens directly below the clicked card, not below the entire level row
- [ ] Stats strip: single row with inner dividers on both mobile and desktop
- [ ] Job title chips wrap cleanly — no overflow
- [ ] Risks/Opportunities stat + label on one line without awkward wrapping
- [ ] How to Adapt stacks to single column on mobile

### Manual — AEO & Data Integrity
- [ ] AEO/SEO audit: run steps 7–9 of `/aeo-seo-site-audit` (Schema Validation, Content Quality, Authority & Citability) directly on the career data file and route; fix all 🔴 Critical issues (do not save audit report to file)
- [ ] Network check: `python3 scripts/publish_check.py <slug> --network`; all source URLs return HTTP 200

### Summary

| Check | Status | Notes |
|-------|--------|-------|
| CareerData fields | | |
| Sources & citations | | |
| SEO & schema | | |
| JSON-LD (Guide + Occupation + FAQPage) | | |
| Sitemap | | |
| Formatting | | |
| Mobile layout | | |
| AEO/SEO audit | | |
| Build | | |
| Data integrity (network) | | |

---

## Phase 2C: Industry Page

### Files
- Route: `app/industry/[slug]/page.tsx`
- Data file: `src/data/industries/[slug].ts`
- Layout (read-only): `src/components/IndustryPageLayout.tsx`

### Automated (verify script pass)
- [ ] Route exists and exports `metadata: Metadata` with `title`, `description`, `alternates.canonical`
- [ ] `meta` prop on `<IndustryPageLayout>` matches `metadata` export exactly (title, description, canonical in sync)
- [ ] Data file exports cluster with `name`, `description`, `careers[]`
- [ ] Each career in `careers[]` has `title`, `slug`, `score`, `growth`, `openings`, `level` (1–5)
- [ ] Every `slug` in `careers[]` exists in `CAREER_PAGE_SLUGS`
- [ ] Sitemap entry present, lastmod=today, changefreq=monthly, priority=0.8

### Manual
- [ ] All `careers[]` slugs have live career pages (data file + route both exist)
- [ ] Scores, growth, and openings in `careers[]` match values in the corresponding career data files
- [ ] No em-dashes in data file
- [ ] JSON-LD `Guide` schema present in route file
- [ ] Build passes

### Summary

| Check | Status | Notes |
|-------|--------|-------|
| Route & metadata | | |
| Career slug validation | | |
| Data consistency | | |
| JSON-LD (Guide + FAQPage) | | |
| Sitemap | | |
| Formatting | | |
| Build | | |

---

## Phase 2D: Now Article

### Files
- Data file: `src/data/now/[id].tsx`
- Index: `src/data/updates.tsx`
- Route: `app/now/[slug]/page.tsx`

### Automated (verify script pass)
- [ ] ID format: `YYMMDD-kebab-case-title`
- [ ] Imported in `src/data/updates.tsx`, appears in `UPDATES` array
- [ ] `category` is a valid `UpdateEntry` type value; appears in `CATEGORIES` in `src/views/Now.tsx`
- [ ] Required fields: `id`, `date` (human-readable string), `title`, `content` (ReactNode), `links` (1+ entry with `label` + `href`)
- [ ] No superlatives: unprecedented, revolutionary, game-changer, the best, comprehensive
- [ ] No fear phrases: "don't get left behind", "before it's too late", "act now", "window is closing"
- [ ] No false binary: "it's not about X, it's about Y" pattern
- [ ] Sitemap: URL present, lastmod=today, changefreq=monthly, priority=0.6

### Manual
- [ ] `generateStaticParams` in `app/now/[slug]/page.tsx` will pick up the new article (reads from `UPDATES`)
- [ ] Build output includes `/now/[id]`
- [ ] Category filter on `/now` correctly shows/hides this article

### Summary

| Check | Status | Notes |
|-------|--------|-------|
| Category validation | | |
| Required fields | | |
| Index registration | | |
| Sitemap | | |
| Formatting & voice | | |
| Build | | |
