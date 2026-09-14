---
name: evidence-led-frontend
description: "Build landing pages, portfolios, and marketing sites where every visual decision traces to a measured reference or a named audit checkpoint, and the agent has to show that trail before it ships. Use for a new marketing page, a portfolio, a hero or section rebuild, a visual overhaul, or any brief that says make this look better, more premium, less generic, or less AI-generated. Also use when reviewing a page someone else built and you need to say precisely why it reads as templated. Not for dashboards, data tables, admin panels, or multi-step product UI."
argument-hint: "[page kind, audience, and any brand constraints]"
allowed-tools: Bash, Read, Write, Edit, Glob, Grep, AskUserQuestion
---

# Evidence-Led Frontend

Most design skills hand the model a list of preferences and hope taste emerges. This one does the opposite: it refuses to let a decision into the build unless that decision has a source.

There are exactly two legal sources.

1. **A measured reference value.** A number or colour extracted from a real site with a script, not recalled from training data.
2. **A named audit checkpoint.** A specific ID from the framework in the Checkpoint Gates section below.

Anything with neither is a preference. Preferences are how a page ends up looking like every other page, because a model's preferences are the statistical centre of everything it has seen. The centre is the slop.

---

## The one rule

> If you cannot name the source for a decision, you have not made a decision. You have defaulted.

This has a practical consequence you must honour: **you produce a decision ledger before you produce the page.** Not after, and not on request. See the Decision Ledger section.

---

## Build order

Do these in sequence. Each step closes off a class of default before the next one opens.

**1. State the read.**
One sentence, out loud, before anything else:

> "Reading this as a [page kind] for [audience], where the visitor's single next action is [action], and the thing that must land in the first viewport is [claim]."

If you cannot fill in the action, stop and ask. A page with no next action is a brochure, and brochures fail `cvr_01` and `cvr_03` no matter how they look.

**2. Fix the type system.** Before any layout. See Measured Baseline.

**3. Fix the ground and the accent.** Before any component. See Measured Baseline.

**4. Compose the first viewport only.** Get one screen genuinely right. A strong hero and four weak sections beats five mediocre ones, and it is much easier to extend a good decision than to rescue a bad one at section five.

**5. Extend downward.** Sections inherit the system. New type sizes, new colours, and new radii at this stage are drift, not variety.

**6. Run the Checkpoint Gates.** Fix what fails. Report what you could not fix and why.

**7. Emit the ledger.**

---

## Measured baseline

Every value in this section came off a live site with a script on **2026-07-26**. These are not aesthetic opinions and they are not mine, they are observations. Treat them as a floor to clear, not a style to copy.

### The four standing references

| Site | Type | Display max | Ground | Accent |
|---|---|---|---|---|
| Benjamin Creative | PP Neue Montreal Medium | **146px** | `#111111` | `#FB4617` |
| PZ Studio | custom (regular / light) | **101px** | `#000000` | none |
| Media.Monks | Helvetica Now, Helvetica Now Extended, Morian | **172px** | `#191715` on `#EAE8E4` | none |
| Red Collar | RedCollar custom, TTCommons | **130px** | `#0D0C0C` on `#FAFAFA` | `#F51B1B` |

### What the set agrees on, and what that costs you to ignore

**None of the four use Inter.**
Inter is the default reach, which is exactly why it reads as templated. It is not a bad typeface, it is an *unmarked* one. For reference, the Verifux landing page itself measured Inter at 83% of rendered text and tripped the overused-font rule in its own audit, so this is not a rule I am exempt from.
→ Pick one display face with a real voice. Geist, Cabinet Grotesk, Satoshi, PP Neue Montreal, Neue Haas Grotesk, or a licensed custom face. One. Then use a different *cut* of the same family for emphasis rather than importing a second family.

**All four run display type between 101px and 172px.**
Not 48px. Not 64px. The smallest of the four is 101px.
→ If your largest text is under 72px on desktop, you are not being restrained, you are being timid, and it reads as a template. Restraint is Media.Monks at 172px with no accent colour at all.

**Not one uses pure black or pure white.**
Measured grounds: `#0D0C0C`, `#111111`, `#191715`, `#2D2D2D`. Measured lights: `#FAFAFA`, `#EAE8E4`.
→ `#000` and `#fff` flatten depth because nothing in the physical world reflects like that. Tint your neutrals, and tint them all in the same direction. Warm greys and cool greys in one palette is the single most common tell that a page was assembled rather than designed.

**Two of four use exactly one hot accent. The other two use none.**
`#FB4617` and `#F51B1B`.
→ The discipline worth stealing is frequency, not hue. The accent should appear rarely enough that it still registers as an event. If your accent is on the nav, three buttons, six icons and a border, it has stopped being an accent and become a background.

### How to re-measure

These values decay. Re-run the extraction rather than trusting a date, especially before citing a number to a client.

```bash
# The library the values above come from
cat ~/.claude/skills/design-reference-library/references/library.json
```

If a site has been redesigned since the measured date, say so in the ledger rather than quoting a stale number as current.

---

## Decision ledger

Emit this **before** the code, as a markdown table. It is the deliverable that separates this from a vibe.

| Decision | Value | Source | Type |
|---|---|---|---|
| Display face | Cabinet Grotesk | No standing ref uses Inter; one face, own voice | measured |
| Display size | 108px / 6.75rem | Standing refs measure 101 to 172px | measured |
| Ground | `#0F0E0D` | Refs never use pure black; warm-tinted | measured |
| Accent | `#EA3718`, used 3 times | One hot accent, frequency not hue | measured |
| CTA position | Above fold, single primary | `cvr_01` CTA hierarchy | checkpoint |
| Focus ring | 2px, 3:1 against both grounds | `acc_02` focus indicators | checkpoint |

Rules for the ledger:

- Every row is `measured` or `checkpoint`. There is no third category.
- If you want a decision that fits neither, you must write the row as `assumption` **and say so in your reply to the user**. Two or three assumptions on a page is normal. Twelve means you are designing from defaults and calling it a ledger.
- Keep it to the decisions that shape the page. Ten to twenty rows. A ledger listing every border radius is theatre.

---

## Checkpoint gates

These are real IDs from the MX/BX/AIX framework, the same ones a Verifux audit scores against. A static marketing page cannot satisfy all 54, so this is the subset that applies at build time. Run them before you call the build done.

### Must pass, no exceptions

| ID | Check | Failure looks like |
|---|---|---|
| `acc_01` | Colour contrast | Body text under 4.5:1, or large text under 3:1. Measure it, do not eyeball it. |
| `acc_02` | Focus indicators | Tab through the page. If you lose the cursor, it fails. |
| `acc_03` | Image and icon accessibility | `alt=""` on a meaningful image, or `alt="image"` |
| `acc_06` | Text sizing | Body under 16px, or a line longer than roughly 75 characters |
| `cvr_01` | CTA hierarchy | Two competing primaries, or a primary that is only a colour away from a secondary |
| `cvr_03` | Value proposition clarity | First viewport does not say what this is or who it is for |
| `con_01` | Visual consistency | A second type scale or a second grey family appears mid-page |

### Should pass, justify in the ledger if not

| ID | Check |
|---|---|
| `vis_03` | Interactive affordance. Hover, active and disabled states actually exist |
| `vis_05` | Empty state design, where any list or feed can be empty |
| `cog_01` | Information hierarchy and scannability |
| `cog_05` | Page density and visual noise |
| `con_05` | Icon consistency. One family, one stroke weight |
| `err_05` | 404 page, when routing exists |
| `cvr_02` | Trust signals, where a claim needs backing |
| `aix_01` | Machine-readable structure. Real semantic elements, heading order intact |
| `aix_04` | Factual groundedness. No invented statistic or fake testimonial |

`aix_04` is not a style rule and it is the one I would most expect an agent to quietly break. Do not invent a customer name, a percentage, a funding figure, or a logo wall. Use an obvious placeholder and tell the user it needs real content.

---

## Counter-evidence, not opinion

Each of these is a pattern that reads as generated. The point is that each has a stated reason, so you can argue with it rather than obey it.

| Pattern | Why it reads as generated |
|---|---|
| Three equal feature cards in a row | The highest-frequency layout in the training distribution. Reaching for it is literally reaching for the average. |
| Purple to blue gradient on a dark ground | The most common accent treatment in AI-generated UI since 2023. Instantly recognisable as a tell. |
| Inter, or system-ui left unstyled | Unmarked by definition. See the measured baseline. |
| Everything centred | Symmetry is the lowest-energy composition. It is what you get when no decision was made. |
| Pure `#000` background | No standing reference uses it. Flattens depth. |
| Lucide or Feather icons, untouched | The default icon set for this class of tool. Fine as geometry, a tell as a choice. |
| `height: 100vh` | Breaks on iOS Safari. Use `100dvh`. This one is a bug, not a taste call. |
| Em dashes in body copy | The strongest single textual tell of unedited model output. Use a comma, a colon, or a full stop. |
| "Elevate", "Seamless", "Unleash", "Transform your workflow" | Category-level marketing language that survives find-and-replace across any competitor. If a rival could run the same sentence unchanged, it says nothing. |
| Round testimonial avatars, three across, with dots | Pattern-matched furniture. Nobody reads the third one. |

On that last row of copy tells: the deeper test lives in `/taste-arbitrage`. If the page's words are load-bearing, run that first and come back. Building a beautiful page around weak positioning is the most expensive mistake available here, because it looks finished.

---

## Motion

Motion is the fastest way to make a page feel either expensive or cheap, and the difference is mostly restraint.

- Animate `transform` and `opacity`. Animating `top`, `left`, `width` or `height` causes layout thrash and reads as jank on a mid-range laptop.
- Entry animations stagger. Everything arriving at once is a page load, not a reveal. 60 to 90ms between siblings.
- Duration 200 to 400ms for interface feedback. Past 500ms the interface feels like it is thinking.
- Honour `prefers-reduced-motion`. This is `acc_05` adjacent and it is not optional.
- One signature move per page. A scroll-pinned section *or* a cursor-reactive hero *or* a scrub-driven reveal. Three signature moves is a showreel, not a product.

---

## Scope limit

This skill covers **landing pages, portfolios, marketing sites, and visual overhauls of those**.

It does not cover dashboards, data tables, admin panels, settings screens, or multi-step product UI. Those have mature systems already (Fluent, Carbon, Atlassian) that encode years of decisions this skill would actively fight. Large display type and sparse composition are wrong for a data table, and being confidently wrong there is worse than being plain.

If the brief is a product UI, say so and route to the component-level skills instead of stretching this one over it.

---

## Output contract

Every run produces, in this order:

1. **The read.** One sentence.
2. **The decision ledger.** Table, sourced, assumptions flagged.
3. **The build.** Working code, no placeholder comments, no truncation.
4. **The gate report.** Which checkpoints pass, which fail, what you could not fix and why.

A build that ships without the ledger has skipped the only part that makes it defensible to a client. If you are about to skip it because the task felt small, that is precisely when the defaults win.
