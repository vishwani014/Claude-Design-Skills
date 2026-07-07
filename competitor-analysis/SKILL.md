---
name: competitor-analysis
description: Runs a structured competitor analysis for a software product or project idea, producing a markdown report covering feature comparison, pricing, positioning, UX patterns, and strategic gaps. Use this skill whenever the user explicitly asks for a "competitor analysis," "competitive analysis," "market scan," or asks to "analyze competitors" / "research the competition" for a product, app, platform, or project — whether or not they've named specific competitors yet. Make sure to trigger this even when the user only gives a project idea and asks something like "who else is doing this" or "what's already out there."
---

# Competitor Analysis

A workflow for researching a software product's competitive landscape and turning that research into a decision-ready report. This is a multi-stage process — resist the urge to do it all in one pass. Each stage produces something worth checking before you spend more effort on the next one, which keeps you from writing a beautifully detailed report about the wrong five competitors.

## Why the staging matters

Competitor research is easy to get wrong in a way that isn't obvious until the report is already long: the wrong competitors get selected, or the analysis drifts toward whichever competitor has the most polished marketing site rather than whichever one the user actually competes with. A checkpoint after competitor selection is cheap (one question) and saves redoing the expensive part (deep research across five or six products).

## Stage 1: Establish scope and seed list

Before searching, understand what's being built. Ask if it isn't already clear from context:
- What does the product/project do, in one or two sentences?
- Who is it for (target user, market, geography)?
- Any competitors already in mind? The user may name specific companies, or just describe the space.

If the user gave a seed list, treat those as confirmed inclusions. If they gave none, or only 1-2, move to Stage 2 to fill the list out via search.

## Stage 2: Identify competitors (search to fill gaps)

Use `web_search` to find additional competitors — direct competitors (same problem, same audience) and adjacent ones (same problem, different audience, or vice versa) are both worth surfacing. Aim for a working list of 4-7 competitors; more than that dilutes the report and less than 3 rarely gives useful contrast.

For each candidate, do a quick sanity check (name, one-line description, URL) before adding it to the list — don't let obviously irrelevant results (defunct products, unrelated tools that just share a keyword) onto the list.

**Checkpoint:** Before doing deep research, show the user the proposed competitor list and ask them to confirm, trim, or add to it. This is the single most important checkpoint in the whole workflow — everything downstream depends on researching the right set of products.

## Stage 3: Research each competitor

For each confirmed competitor, gather what's findable via `web_search` and `web_fetch` (their site, pricing page, app store listings, review sites like G2/Capterra, recent press or blog posts). Not everything will be findable for every competitor — note gaps rather than guessing or inventing numbers.

Gather, per competitor:
- **Feature set** — core capabilities, standout features, notable omissions
- **Pricing & business model** — tiers, free/freemium presence, billing model (subscription, usage-based, one-time)
- **Positioning & target audience** — who they market to, how they describe themselves, tone
- **UX & design patterns** — navigation structure, onboarding approach, visual style; describe in words rather than assuming you can screenshot (note if the user wants actual screenshots captured separately)
- **Tech stack signals** — anything discoverable from job postings, engineering blogs, BuiltWith-style clues, or site behavior; mark as "not discoverable" rather than guessing when nothing surfaces
- **Strengths & weaknesses** — inferred from reviews, feature gaps, or user complaints found in research

Keep per-competitor research in working notes; don't write the final report prose until all competitors are covered, so the comparison sections are consistent.

## Stage 4: Synthesize the report

Write a single markdown file with this structure:

```markdown
# Competitor Analysis: [Project Name]

## Overview
[1-2 paragraphs: the space, who's in it, headline takeaway]

## Feature Comparison Matrix
[Table: competitors as columns, key features as rows, checkmarks/notes as cells]

## Pricing & Business Models
[Per-competitor summary, then a short comparative note]

## Market Positioning & Target Audience
[Per-competitor summary: who they target and how they position themselves]

## UX & Design Patterns
[Per-competitor summary of navigation, onboarding, visual style]

## Tech Stack Signals
[Whatever was discoverable; explicitly note "not publicly discoverable" where relevant]

## Strengths, Weaknesses & Gaps
[Per-competitor strengths/weaknesses, then a synthesized "gaps to exploit" section — where is the field weak, underserved, or inconsistent]

## Recommendations
[2-4 concrete implications for the user's project: differentiation angles, pricing positioning, features to prioritize or deprioritize]
```

Follow the docx/pptx skill conventions only if the user asks for those formats instead — by default this skill's output is a `.md` file, since that's fastest to read, paste into Notion/docs, and iterate on.

Save the file to the outputs directory and present it. Don't pad the report with filler — every section should say something specific to these competitors, not generic industry commentary that would apply to any comparison.

## Notes on rigor

- Never fabricate pricing, feature lists, or user numbers. If it can't be found, say so plainly ("pricing not publicly listed") rather than estimating.
- Cite where specific claims come from when it matters (e.g., "per their pricing page" or "per G2 reviews") so the user can verify anything that surprises them.
- If a competitor pivoted, shut down, or was acquired since you'd expect, flag that explicitly rather than reporting stale info as current.