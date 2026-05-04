---
name: editorial-design
description: Visual system for long-form content on ai-proof-careers.com. Use when designing or refactoring layouts for /now posts, blog posts, or any long-form page that should read as editorial (magazine/journal) rather than SaaS dashboard. Invoked by now-page-writer and should be invoked directly when building visual components for long-form content.
---

# Editorial Design

Visual system for long-form content. The goal: pages that read like a considered print journal (The Economist, a Linear release note, a CG Journal spread) — not a SaaS marketing page.

Reference points: Linear's /now posts (fine lines, sharp corners, precise visuals conveying meaning with minimal text), the site's own career pages (hairline dividers, tiny uppercase labels, a single bold stat), and editorial layouts that use a serif masthead + hairlines + one accent.

---

## First principles

1. **Lines, not fills.** Separate content with 1px hairlines (`border-t border-border`), not with colored card backgrounds. Default to no `bg-card`. Reach for a fill only when a block must truly pop off the page — and then only once per post.
2. **Sharp corners.** Default to `rounded-none`. Allow `rounded-sm` (2px) for pills and buttons. Never `rounded-xl` or `rounded-lg` on content blocks. No circular icon badges.
3. **One accent, used once.** Pick a single accent per post (default: coral `hsl(16,85%,58%)`). Apply it to exactly one element — the hero stat, or one callout. Everything else is ink-on-paper (`foreground`, `muted-foreground`, `border`).
4. **Type contrast carries the design.** Serif display for H1/H2 (`font-serif`). Sans for body. Tiny uppercase tracked labels (`text-[10px] font-bold uppercase tracking-widest text-muted-foreground`) for section markers. The contrast between these three registers is what makes it feel editorial.
5. **Data visible, not dressed up.** Oversized pull-stats (`text-5xl`/`text-6xl`) carry weight by size alone — no background, no icon, no colored circle. One per section max.
6. **Trust whitespace and rules.** If you want something to feel important, give it a top hairline, vertical space above/below, and a tiny uppercase kicker. That's it.
7. **No decorative icons.** Lucide icons only as inline marks (`w-3 h-3`) next to text, same color as the text. Never inside a colored circle. Never as the main visual of a card.

---

## Primitives

Use these patterns. Do not invent card variants outside this set.

### Masthead (top of post)
```tsx
<header className="not-prose border-b border-border pb-6 mb-10">
  <div className="flex items-center justify-between text-[10px] font-bold uppercase tracking-widest text-muted-foreground">
    <span>{category}</span>
    <span>{date} · Issue {n}</span>
  </div>
  <h1 className="font-serif text-4xl md:text-5xl font-normal leading-[1.1] mt-6 text-foreground">
    {title}.
  </h1>
</header>
```

### Hairline divider (optionally labeled)
```tsx
<div className="flex items-center gap-3 py-1 not-prose">
  <div className="flex-1 border-t border-border" />
  <span className="text-[10px] font-bold uppercase tracking-widest text-muted-foreground">{label}</span>
  <div className="flex-1 border-t border-border" />
</div>
```
Unlabeled: just `<hr className="border-t border-border my-10" />`.

### Pull-stat (one per section, max)
```tsx
<div className="not-prose grid grid-cols-[auto_1fr] gap-6 items-start my-10 py-6 border-t border-b border-border">
  <div className="font-serif text-6xl leading-none text-[hsl(16,85%,58%)]">62%</div>
  <p className="text-[11px] uppercase tracking-widest font-bold text-muted-foreground leading-relaxed max-w-[24ch]">
    of visitors explore more than one career before leaving
  </p>
</div>
```
Only this element gets the accent color. Never colorize the label.

### Data list (label/value rows)
```tsx
<dl className="not-prose my-8">
  {rows.map((r) => (
    <div key={r.label} className="grid grid-cols-[1fr_auto] items-baseline py-3 border-b border-border last:border-b-0">
      <dt className="text-[11px] uppercase tracking-widest font-bold text-muted-foreground">{r.label}</dt>
      <dd className="font-serif text-2xl leading-none text-foreground">{r.value}</dd>
    </div>
  ))}
</dl>
```

### Pull-quote (no card)
```tsx
<figure className="not-prose my-10 border-l border-foreground/30 pl-6">
  <blockquote className="font-serif text-2xl italic leading-snug text-foreground">
    "{quote}"
  </blockquote>
  <figcaption className="text-[10px] uppercase tracking-widest font-bold text-muted-foreground mt-3">
    — {attribution}
  </figcaption>
</figure>
```

### Contrast block (e.g. fear vs signal)
Two columns separated by a single vertical rule. No colored borders, no backgrounds. The label does the framing.
```tsx
<div className="not-prose grid grid-cols-1 sm:grid-cols-2 my-10">
  <div className="sm:pr-8 pb-8 sm:pb-0 border-b sm:border-b-0 sm:border-r border-border">
    <div className="text-[10px] uppercase tracking-widest font-bold text-muted-foreground mb-3">The fear</div>
    <blockquote className="font-serif text-lg italic leading-snug">"…"</blockquote>
    <div className="text-[10px] uppercase tracking-widest text-muted-foreground mt-3">— attribution</div>
  </div>
  <div className="sm:pl-8 pt-8 sm:pt-0">
    <div className="text-[10px] uppercase tracking-widest font-bold text-muted-foreground mb-3">The signal</div>
    <blockquote className="font-serif text-lg italic leading-snug">"…"</blockquote>
    <div className="text-[10px] uppercase tracking-widest text-muted-foreground mt-3">— attribution</div>
  </div>
</div>
```

### Section kicker (before an H2)
```tsx
<div className="text-[10px] font-bold uppercase tracking-widest text-muted-foreground mt-14 mb-2">
  {sectionNumber} — {sectionLabel}
</div>
<h2 className="font-serif text-3xl font-normal leading-tight text-foreground mb-6">{heading}</h2>
```

### Linked item row (industry/feature cards, replacement for promotional cards)
```tsx
<ul className="not-prose my-8 border-t border-border">
  {items.map((it) => (
    <li key={it.slug} className="border-b border-border">
      <Link href={it.href} className="grid grid-cols-[auto_1fr_auto] gap-6 items-baseline py-5 group">
        <span className="font-serif text-3xl text-muted-foreground tabular-nums">{it.num}</span>
        <div>
          <div className="font-serif text-xl leading-tight text-foreground group-hover:underline">{it.title}</div>
          <p className="text-sm text-foreground/70 mt-1 leading-relaxed">{it.blurb}</p>
        </div>
        <ArrowRight className="w-4 h-4 text-muted-foreground" />
      </Link>
    </li>
  ))}
</ul>
```

---

## Type scale

| Role | Class |
|---|---|
| H1 (masthead title) | `font-serif text-4xl md:text-5xl font-normal leading-[1.1]` |
| H2 (section) | `font-serif text-3xl font-normal leading-tight` |
| H3 | `font-serif text-xl font-medium` |
| Body | `text-base text-foreground/80 leading-relaxed` (inherits from prose) |
| Pull-quote | `font-serif text-2xl italic leading-snug` |
| Pull-stat number | `font-serif text-6xl leading-none` |
| Kicker / label | `text-[10px] font-bold uppercase tracking-widest text-muted-foreground` |
| Small caption | `text-[11px] text-muted-foreground` |

Body uses the default sans. Only headings, stats, and quotes use serif. If `font-serif` is not configured in Tailwind, fall back to `font-family: ui-serif, Georgia, serif` via inline style on the component — do not ship sans-only headings.

---

## Color discipline

- **Ink:** `text-foreground`, `text-foreground/80`, `text-foreground/70`, `text-muted-foreground`. Build 90% of the page from these.
- **Rules:** `border-border` only. No colored borders.
- **Accent (once per post):** coral `hsl(16,85%,58%)`. Used on the single most important stat or one callout. Never on generic card borders, icons, or hover states.
- **Forbidden on /now and long-form editorial pages:**
  - `bg-card` on content blocks (it flattens the page into boxes)
  - Red/green semantic colors for tone (fear/signal, etc.) — use labels instead
  - Gradients, shadows (`shadow-*`), `ring-*`
  - Circular icon badges (`rounded-full` containers around icons)

---

## Charts and visuals

When a post needs a chart or diagram:

- Stroke width 1px. No fills, no gradients. Black or `foreground`, with at most one accent stroke.
- Labels in the same `text-[10px] uppercase tracking-widest` as kickers.
- Prefer annotated line charts, stacked hairline bars, or a small table over a donut or pie.
- If an illustration is needed, think Linear's release graphics: sharp-cornered rectangles, hairline strokes, one accent. No rounded blobs, no soft drop shadows.

Do not use `recharts` defaults — they ship rounded bars and gradient fills. Override.

---

## Authoring checklist

Before shipping any long-form page, verify:

- [ ] Zero `rounded-xl` / `rounded-lg` on content blocks
- [ ] Zero `bg-card` fills on content blocks (hairlines only)
- [ ] Exactly one accent color, used on exactly one element
- [ ] All H1/H2/pull-quotes/pull-stats use serif
- [ ] No icons inside colored circles
- [ ] Section transitions use hairlines + uppercase kickers, not boxes
- [ ] Pull-stats are oversized (5xl+) and stand alone — not gridded into dashboard tiles
- [ ] Quote blocks use left-border, not card
- [ ] No gradients, no shadows, no colored semantic borders

If any box is checked wrong, refactor before shipping. The point of this system is restraint — breaking one rule anywhere makes the whole page read SaaS again.

---

## Anti-patterns (things that make the page look generic)

- Four-across grid of `rounded-xl bg-card` stat tiles
- Icons in filled circles next to labels
- Left-border-colored cards used for tone (red = bad, green = good)
- Every section wrapped in its own card
- Body-weight headings (makes headings look like bolded paragraphs — serif + `font-normal` at large size reads as a heading without needing weight)
- "Explore our comprehensive guide" promotional card with image + CTA button. Use the numbered linked-item list instead.
