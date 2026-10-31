---
name: creator-intelligence
description: Pull mode for Creator Intelligence. Searches every saved card and concept page in creator-intelligence/ (by shape, pool, company, concept or theme), returns matches generously with the count, and bridges a card to the audience on request. Researches nothing new. Use when Huzaifa runs /creator-intelligence or asks what the library has on something.
---

# Creator Intelligence: pull mode

Search the library when Huzaifa sits down to make something:
`/creator-intelligence discipline`, `/creator-intelligence shocking-number finds
about pricing`, `/creator-intelligence anything on pivots`, or
`/creator-intelligence bridge 2026-10-31-14`.

**Read-only, apart from the search log.** Never edit cards, concept pages or
anything else, and never research anything new: no web search, no fetching.
The only file this skill writes is `creator-intelligence/searches.md`.

## The library

- Cards: `creator-intelligence/cards/YYYY/MM/<card-id>.md`. Frontmatter: id,
  number, date, title, shape, pool, concept, kind, source_link, source_name,
  strategy, featured, wildcard, status. Body: The find, The surprise, The idea,
  and for featured or deepened cards, `## In depth` and `## Deeper` sections.
- Concept pages: `creator-intelligence/concepts/<slug>.md`. Each lists every
  card that anchors that concept.

Shapes: `1-hidden-reason`, `2-shocking-number`, `3-wrong-decision-worked`,
`4-tiny-change`, `5-unknown-origin`, `6-day-walk`, `7-far-field`,
`8-unexpected-claim`, `9-unfamiliar-concept`, `unshaped`, plus any trial shapes.
Pools: `marketing`, `psychology`, `founders`.

## Searching

Work out which kind of search it is. Many are both.

- **Exact** (a shape, pool, company, person, concept, date, status such as
  "used" or "deepened", or "featured"): Grep the frontmatter and body and return
  every precise match. For a concept, start from its concept page.
- **Theme** ("discipline", "pricing", "anything on pivots"): cards aren't filed by
  theme, so judge relevance yourself. Grep for the obvious words and synonyms,
  read the concept page names, then read candidate cards and decide. Be
  generous: include anything a creator might reasonably use for the theme, and
  rank the strongest first.

Combine filters when a query has both ("shocking-number finds about pricing" is
shape 2 plus the theme pricing).

## Returning results

Lead with the count, always in the form **"showing 15 of 40"**, so Huzaifa can
see past your ranking. Show up to 20 at a time. If there are more, say how to
see the rest ("say 'more' for the next 20").

For each match:

```text
14 · Haier's CEO smashed 76 fridges   (2026-10-31 · 3 Wrong decision that worked · Founders · used)
The find: ...
The idea: ... (quality signalling)
Source: <source_link> · creator-intelligence/cards/2026/10/2026-10-31-14-haier-smashed-fridges.md
```

After the list, name the concepts the matches cluster around, with their
concept-page paths. Those are the big topics. If nothing matches, say so and
suggest the nearest concepts or shapes that do have cards.

## Bridging on request

When asked to bridge a card ("bridge the Haier one", "bridge 2026-10-31-14", or
the number from the results just shown), bridge it the same way ci-reply does.
Write options of deliberately different kinds:

- **Flipped belief:** what the viewer has wrong
- **New frame:** a different way to see something
- **Lever:** a specific thing to do (the actionable tip lives here)

Each names the audience problem it aims at, then the landing line:

```text
→ Can't stay consistent · Flipped belief
  You don't lack willpower, your environment has too much friction.
→ Wants to move faster · New frame
  Every step between you and the work is a decision you have to win again.
→ Can't stay consistent · Lever
  Remove the first step: sleep in your running clothes.
```

- If `../creator-intelligence/brain/audience-problems.md` exists and lists
  problems, aim at those. Otherwise choose the problem yourself.
- One off-list option may aim at a problem not on the list.
- A find can have no bridge. Say so in one line if nothing honest connects.
- Never write the bridge onto the card. Cards stay raw.

## Logging

Append one line per search or bridge to `creator-intelligence/searches.md`
under `## Log` (create the file with the header below if it's missing). ci-weekly
reads this file as a signal.

```text
- 2026-10-31 14:22 · search · "shocking-number finds about pricing" · exact+theme · 40 matches · showing 15 · top: 2026-10-31-14-haier-smashed-fridges, 2026-10-28-03-...
- 2026-10-31 14:30 · bridge · 2026-10-31-14-haier-smashed-fridges
```

Get the time with `date '+%F %H:%M'` if Bash is available; otherwise use the date
alone. Remind Huzaifa, in one short line at the end, that the log only reaches
the weekly run once second-brain is committed and pushed.
