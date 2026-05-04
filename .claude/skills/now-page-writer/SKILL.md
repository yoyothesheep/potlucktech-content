# `/now` Page Writer

> **When to use this skill:** Any time you are writing or editing content that lives under `app/now/` — launch announcements, platform updates, and release notes. Read it before you write a single word.

> **Visual design is handled by the `editorial-design` skill.** This skill covers voice, tone, and structure only. Before building or refactoring any visual layout for a `/now` post (callouts, stat blocks, quote cards, dividers, mastheads, charts), **invoke the `editorial-design` skill** and follow its primitives and rules. Do not hand-roll `rounded-xl bg-card` callouts — they violate the editorial system.

---

## The Persona Behind This Voice

Think of the writer as someone who has been watching the labor market change in real-time from the inside — a technologist who genuinely cares about the people on the other side of this shift. They are not a pundit. They are not a cheerleader. They are a thoughtful peer who happens to have data.

The reader is someone sitting at their desk, mid-career or early-career, quietly wondering if their job is still going to exist. They've Googled it. They've seen the hot takes. They don't need more noise. They need a straight answer and a clear path.

Write for that person.

---

## Core Tone Principles

### 1. Hopeful, not hype-driven
There is a meaningful difference between optimism and spin. Hype says "this changes everything." Hope says "things are shifting, and here's where to find solid ground." We do the latter.
- **Don't write:** "This is a game-changer that will transform how you navigate your career."
- **Do write:** "We built this because people deserve better data than the anxiety cycle offers."

### 2. The "Dinner Table" Test (Relatable and Down-to-earth)
Write as if you’re explaining a complex shift to a smart friend at a dinner table. Use plain words. Use contractions. Let sentences breathe. 
- **The Rule**: If you wouldn't say the sentence in a real-world conversation, don't write it.
- **Example**: Instead of "Many workers are facing uncertainty," use "You've likely heard a version of this in a group chat or in the silence after a team meeting."

### 3. Emotionally grounded, not emotionally manipulative
You are allowed to name the feeling in the room. "This is a hard time to be starting a career." That's honest.
- **Validation through Data**: Don't tell the reader they are worried; show them that 500,000 other people are searching for the same footing they are. Let the numbers validate the emotion.
- **Example**: "500K+ impressions—not because people are curious, but because they are looking for solid ground." (Actually, avoid "not because... but because..." patterns — use: "500K+ impressions. People are looking for solid ground, not just curiosity.")

### 4. Hard Technical Anchoring (Specific, always)
Vague language is hollow. It sounds safe but says nothing. Earn trust by using specific professional "anchors" (high-fidelity tasks only an insider would know).
- **Don't write:** "Marketing is seeing significant AI impact."
- **Do write:** "Marketing is shifting toward attribution modeling and hard brand differentiation."

### 5. Kill the "AI-isms" (No telltale AI marks)
We must strip out the rhetorical patterns that have become markers of generated content:
- **Zero Superlatives**: Absolutely no "unleash," "harness," "empower," "unlock," "pave the way," or "seamless."
- **No False Binaries**: Avoid the "It’s not X, it’s Y" structure. State the reality directly.
- **No Rhetorical Juxtapositions**: Never use the "not because... but because..." or "not just X... but Y..." construction. These feel over-structured and "hollow."
- **Staccato Texture**: Vary sentence lengths. AI writes in medium-length, balanced blocks. Use short, punchy fragments for emphasis. (e.g., "Same job title. Two different realities.")

---

## Structure of a `/now` Announcement

### The Title
Should describe the moment, not sell it. It can be a statement or a quiet question. It should feel like the beginning of a real conversation.

- **Good:** "From Leaderboard to Deep Dives: What We Launched Today"
- **Good:** "A New Chapter: Industry Guides for the Careers Being Hit First"
- **Avoid:** "Introducing Our Revolutionary New Feature"

### The Opening (2–4 sentences)
Ground the reader in the context first. What's the situation that made this necessary? What have we been seeing? Don't open with what you built. Open with why it matters.

```
Example opening:

Something has been shifting in the job market — and if you've been paying attention, you've felt it before you saw it. 
We've watched over half a million people find their way to this site in the past few months. 
They don't just browse. They explore, they compare, they come back.
That told us something important about what people need right now.
```

### The Body: What We're Announcing
State the news directly. No buildup. Be concrete: what exists now that didn't exist before? Use numbers and specifics.

Move quickly to **why it matters for the reader** — not what it is technically, but what it changes for someone trying to figure out their career.

### Industry or Feature Cards
When linking to content (industry pages, career guides, etc.), write 1–2 sentences of honest framing, not promotional copy.

- **Good:** "Finance & Accounting. The impact is uneven — entry-level roles are being hit much harder than senior ones, and the data shows exactly where the line falls."
- **Avoid:** "Explore our comprehensive Finance & Accounting guide with in-depth analysis!"

### The Honest Middle
Every good announcement makes room for the hard truth. We are not pretending things are fine. The AI shift is real, the entry-level pipeline is compressing, and people are right to be uncertain.

Name this without dwelling on it. Then pivot to what the data shows as useful — specific paths, concrete signals, real options.

### The Feedback / Community Moment
Every `/now` piece should remind readers they are part of a conversation, not a broadcast. Reference the "Give Feedback" button on career pages. Invite them in.

```
Example:

We've added a feedback button to every career page — not as a formality, but because 
what you're experiencing in your specific role is something the data can't fully capture. 
If something doesn't look right, or if your situation has changed, tell us.
```

### The Close
End with a clear next step — a link, an invitation, or a quiet reflection. Don't end with a call-to-action that sounds like a CTA. End with a sentence that makes the reader feel good about having read this.

- [Good]: "If any of this resonates, the industry pages are live. Start wherever it makes sense for you."
- [Avoid]: "Click here to explore our full suite of career resources today!"

---

## Graphics & Visual Rhythm

While the `editorial-design` skill provides the global primitives, `/now` posts follow a specific "Technical Editorial" standard for high-fidelity data and career content.

### 1. The Vertical Spine (Desktop Only)
All major visual groups (tables, bar charts, card grids) must use `mx-auto w-5/6` as their container. This creates a consistent vertical spine that separates high-density data from the standard-width prose columns.
- **IMPORTANT**: On mobile viewports, hide the vertical spine decorations (lines and dots) to maximize horizontal space for the content.

### 2. The High-Tension Hug (Tension and Alignment)
We prioritize tight vertical tension over airy white space. The first content block of any article should "hug" the header's baseline divider.
- **Implementation**: Set `mb-0` on the header's terminal divider and `mt-0` on the first content block (e.g., the opening quote grid).
- **Internal Padding**: Use condensed internal padding for grouped layout elements (`py-4` instead of `py-8` or `py-12`).

### 3. Condensed Mobile Flow (Responsive Cleanliness)
Maintain a streamlined article flow on small screens by hiding redundant UI elements:
- **Breadcrumbs**: Hide the final breadcrumb title on mobile (`hidden md:flex`). The line should strictly read `Home › Now`.
- **Clamping**: Always use `line-clamp-3` on the `/now` index page previews to keep the timeline scannable.
- **Sidebars**: Hide the date/category sidebar on mobile. Place a small, subtle date string below the description instead.
- **Margins**: Use `px-8` on mobile to provide enough horizontal breathing room for the high-density text.

### 4. High-Fidelity Cards (Emerging Roles)
When showcasing emerging careers or transition maps, use the high-fidelity landscape card:
- **Geometry**: Mandatory `rounded-none` (no corner radius).
- **Background**: Use a neutral grey finish (`#efefef` or `bg-foreground/[0.04]`). Avoid the "creamy" yellow-tinted backgrounds which read as too soft.
- **Borders**: High-contrast boundaries (`border-foreground/30`).
- **Aspect Ratio**: Landscape orientation is preferred. Inside the card, split content side-by-side (e.g., Title/Sector on left, Description/Stat on right) on desktop to prevent cards from becoming too tall/square.
- **Clickable Signal**: Every data claim or source must be an external hyperlink, not just static text.

### 5. Precise Data Visuals (Bar Charts)
- **Dimensions**: Use "Technical Bars" with a condensed height (`h-2` to `h-4`). 
- **Geometry**: `rounded-none` for all bar ends and tracks.
- **Rhythm**: Increase the vertical gap between items (`gap-y-5` to `gap-y-7`). This airiness allows individual data points to feel precise and isolated rather than clumped.
- **Aesthetics**: Use high-contrast or accent colors for fills against very light neutral tracks.

---

## The `preview` Field

Every `UpdateEntry` has a required `preview` string that appears on the `/now` index page. The full `content` (with visuals, quote cards, stat grids) is only shown on the individual post page.

**Rules for `preview`:**
- Plain text only. No JSX, no visuals, no quote cards, no stat grids.
- The reader should immediately understand **what the article is actually about** — what shipped, what changed, what's new. Not the mood-setting intro, not the context, not the emotional framing. That belongs in the full post.
- Start with a clear action phrase that signals the update type (e.g. "Today, we're publishing...", "We just shipped...", "New this week:...").
- 1-3 sentences max. Name the specific features, pages, or content shipped.
- It's OK to be direct and informational here. The preview earns the click; the full post earns the trust.

**Good:** "Today, we're publishing industry guides for the four sectors where AI's impact is most visible: Software & Tech, Finance & Accounting, Sales & BizDev, and Marketing & Growth. Full breakdowns of which roles are holding and how to position yourself."

**Bad:** "Something has shifted in the labor market this year..." (that's the post opening, not the preview — tells the reader nothing about what the article covers)

---

## The Embedded Tone Guide 

> **Copy-paste this block as a comment near the top of any new `updates.tsx` entry or content file when authoring `/now` content. It's a fast reminder before you write.**

```tsx
/**
 * TONE GUIDE — /now Content
 *
 * Voice: Honest peer, not a pundit. Hopeful, not hype-driven.
 *
 * ✅ DO:
 *   - Open with the situation/context, not the feature
 *   - Name the real feeling in the room (uncertainty, transition, change)
 *   - Use specific numbers, names, and concrete examples
 *   - Write in plain language — contractions OK, jargon not OK
 *   - Give readers a clear, honest next step
 *   - Acknowledge what is hard before pivoting to what is useful
 *
 * ❌ DON'T:
 *   - Use superlatives: "best," "revolutionary," "unprecedented," "game-changer"
 *   - Open with what we built (open with why it matters)
 *   - Write promotional link copy — frame content honestly instead
 *   - Use vague language — if you can't point to a number or a name, rewrite it
 *   - Lean into drama or use uncertainty to manufacture urgency
 *   - Use fear-based framing: "Don't get left behind," "before it's too late"
 *   - Use competitive/hustle framing: "Crush it," "Win at your career"
 *   - Use clickbait labels: "Ultimate guide," "Everything you need to know"
 *   - Use the AI false-binary: "It's not about X, it's about Y" — this is a rhetorical
 *     tic that feels borrowed from tech hype decks. State your point directly instead.
 *
 * STRUCTURE:
 *   1. Opening (2–4 sentences): the context, the moment
 *   2. The news: what exists now, specifically
 *   3. Why it matters for the reader, not for us
 *   4. The honest middle: name the hard thing, then the useful thing
 *   5. Community moment: feedback, invitation
 *   6. Close: next step that feels like a natural conversation, not a CTA
 */
```

---

## Word & Phrase Reference

### Superlatives & Hype
| Instead of... | Try... |
|---|---|
| "Unprecedented" | "Real," "significant," "something we haven't seen before at this scale" |
| "Game-changer" | Name the specific change |
| "Revolutionary" | Drop it — let the data speak |
| "Comprehensive" | Name what's actually covered |
| "Ultimate guide" | "A guide to [specific thing]" — name the scope honestly |
| "Everything you need to know" | State what the piece actually covers |
| "We're excited to announce" | Just make the announcement |

### Fear-Based & Urgency Framing
Fear-based copy manufactures urgency by making the reader feel like they're already behind. It's the default mode of most career and productivity content — and exactly what we're not. The underlying message should always be *"here's what's true and what to do"*, not *"you're running out of time.*"

| Instead of... | Try... |
|---|---|
| "Don't get left behind" | "Here's where the growth is concentrated" |
| "Before it's too late" | Name the actual timeline or signal instead |
| "Act now" / "Your window is closing" | State what is changing and when, specifically |
| "The clock is ticking" | Drop it entirely — it says nothing concrete |
| "You can't afford to ignore this" | "This is worth paying attention to, because [specific reason]" |

### Competitive / Hustle Framing
This framing pits the reader against the market, other workers, or AI. It's motivating for some but alienating for many — and it implies that career navigation is a competition to be won, not a set of real decisions to be made carefully.

| Instead of... | Try... |
|---|---|
| "Crush it" / "Kill it" | Say what success actually looks like |
| "Win at your career" | "Make a good next move" or "find roles with real staying power" |
| "Stay ahead of AI" | "Understand where AI is actually having an impact" |
| "Beat the algorithm" | Just describe what the data shows |
| "Dominate your industry" | Drop it entirely |

### The AI False Binary
There's a very common rhetorical pattern in tech writing that frames everything as a corrective: *"It's not about [thing everyone fears]. It's about [thing we're selling you]."* It's a structure borrowed from TED talks and hype decks. It sounds wise but is usually just reframing anxiety, not resolving it.

**Don't write:**
> "It's not about whether AI will take your job. It's about whether you'll take AI's job."

**Don't write:**
> "This isn't about automation. It's about augmentation."

These sound smart but land as dismissive — they minimize real concerns while sneaking in a sales angle. Instead, sit with the real tension and let the data do the reframing:

**Do write:**
> "The task data shows something more nuanced than a simple replacement story. Programmers are seeing automation hit the execution layer hardest. Developers who own architecture and system design are holding up. The difference isn't the job title — it's what the person is actually responsible for."

### Jargon & Filler
| Instead of... | Try... |
|---|---|
| "Leverage" | "Use," "apply" |
| "Robust" | Drop it — say what it does |
| "Deep dive" (as a noun) | "A guide," "a breakdown," "a closer look at..." |
| "Explore our..." | "The [page] is live. Start with [X]." |
| "Unpack" | Just explain the thing |

---

## Tone Inspirations

Two reference points for what this voice can reach toward when the moment calls for it.

---

### Mamdani's St. Patrick's Day Speech (2026)
**What it is:** A routine civic breakfast address that went viral because it made Irish people, Palestinians, and immigrants feel genuinely seen — while teaching others something real about history.

**The key moves to borrow:**

**1. Open with an unexpected historical anchor.**
Don't open with the announcement. Open with a moment from history that reframes the entire piece. Mamdani doesn't open with "Happy St. Patrick's Day." He opens in 5th-century Ireland, which earns everything that follows.

For `/now` content: start not with "we launched X" but with the underlying human moment that made the launch feel necessary.

**2. Use a repeating anchor phrase.**
"Weep with those who weep" is introduced in the first paragraph and returned to in the final sentence — with a pause. The phrase does the structural and emotional work. Everything between is earned context.

For `/now` content: if there's a phrase that captures the tension the site exists to address ("people deserve better than the anxiety cycle offers"), return to it. Let it close the loop.

**3. Name who is usually left out.**
Mamdani names Palestinians by name in a St. Patrick's Day speech. It's unexpected, but it doesn't feel jarring — because the whole speech built toward it. The move: identify the people who are usually passed over in silence, and name them directly. It makes those people feel seen, and it makes everyone else pay attention.

For `/now` content: name the specific worker who is worried right now. Not "people navigating career uncertainty." The 28-year-old programmer who's been refreshing job boards for three months.

**4. The pivot through the hard thing — not around it.**
"When I think of the Irish, I do not think first of oppression. I think of resistance." He doesn't deny the hard thing. He passes through it on the way to something truer. This is different from toxic positivity or false hope.

For `/now` content: acknowledge the compression, the layoffs, the real fear — then move *through* it to what the data shows.

**5. Earn the culture, not just the politics.**
"96-minute Troy Parrott goals" and "Fairytale of New York" land because they're specific. They signal genuine knowledge, not performance. They make the serious parts feel less distant.

For `/now` content: one specific, grounded detail (a real job title, a real city, a real number) earns more credibility than a paragraph of earnest framing.

**6. The weighted close.**
"To all those who still — weep." The pause is the point. Don't race to the CTA. The close should land with some weight.

---

### An Inconvenient Truth (2006)
**What it is:** A documentary built around a slideshow presentation that launched a global climate movement — by treating the audience as smart enough to handle data.

**The key moves to borrow:**

**1. Let the data be the protagonist.**
Gore doesn't argue that climate change is real. He shows you the data and lets you arrive at the conclusion. The evidence builds, layer by layer, until the conclusion feels inevitable rather than asserted.

For `/now` content: don't tell the reader what to think about the AI shift. Show them the task displacement rates, the entry-level pipeline compression, the specific roles that are holding versus falling. The conclusion is theirs to reach.

**2. Data + moral weight = urgency without manipulation.**
The film doesn't use fear-based framing to manufacture urgency. The urgency comes from understanding the data clearly. The data *is* the argument.

For `/now` content: the site has real BLS numbers, real O*NET task data, real displacement percentages. Lead with those. The stakes speak for themselves.

**3. Treat the audience as intelligent.**
The film doesn't simplify to the point of distortion. It explains the science. It respects the audience's capacity to hold complexity.

For `/now` content: don't round off the nuance. "Entry-level roles are compressing faster than senior ones" is more useful than "some jobs are changing." Trust the reader to handle the real picture.

**4. The reveal structure.**
Here's what we know → here's what it means → here's what to do. Not: here's what to do, and here's why. The sequence matters. Earn the recommendation with evidence first.

---

## Relationship to the `/blog` Voice

The blog (career guides, research posts) is **analytical**. It builds arguments from data. It cites sources. It earns trust through evidence.

The `/now` voice is **personal and reflective**. It speaks from the perspective of a team watching something unfold and wanting to be honest about what they're seeing. It still uses data, but the frame is: *"here's what we built and why, written by people who care about where this goes."*

The two sections complement each other. The blog earns authority. The `/now` earns trust.

---

## Before You Publish Checklist

- [ ] Does the opening describe the situation before describing the feature?
- [ ] Is every general claim backed by a specific number or example?
- [ ] Have you named what is genuinely hard, not just what is hopeful?
- [ ] Are the industry/feature links framed honestly (not promotionally)?
- [ ] Is there a feedback / community invitation somewhere?
- [ ] Does the closing feel like a natural end of a conversation?
- [ ] **Visual Spine**: Are all charts and grids aligned to `mx-auto w-5/6`?
- [ ] **Sharp Corners**: Are all visual blocks (cards, bars) using `rounded-none`?
- [ ] **Landscape Flow**: Are card grids balanced (e.g., 2x2) and internally landscape?
- [ ] **Data Proof**: Are all statistics cited with clickable external links?
- [ ] Is there any fear-based urgency language? ("don't get left behind," "before it's too late")
- [ ] Is there any competitive framing? ("crush it," "win," "stay ahead")
- [ ] Is there an "it's not X, it's Y" construction? Rewrite it as a direct statement.
- [ ] Read it aloud. Does it sound like a real person?
- [ ] Does the opening anchor the moment in context before naming the feature? (Mamdani move)
- [ ] Does the data do the persuading, or are you telling the reader what to feel? (Inconvenient Truth move)
- [ ] Have you named a specific person, number, or detail that earns the reader's trust rather than performing concern?
- [ ] Does the close land with weight, or does it race to the CTA?
