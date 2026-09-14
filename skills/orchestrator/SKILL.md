---
name: design-intelligence
description: "6-stage design intelligence orchestrator. Routes any UI, copy, or product design task through the right skill at the right stage: S0 Strategy, S1 Reference, S2 Generate, S3 Audit, S4 Verify, S5 Deliver. Load this first at the start of any design or product session."
argument-hint: "[task description or stage name]"
allowed-tools: Bash, Read, Write, Edit, AskUserQuestion, Skill
---

# Design Intelligence Stack: Orchestrator

6 stages. Every UI, copy, and product design task routes through this chain. Do not skip stages, each one is a quality gate.

---

## Stage Map

| Stage | Name | Skill(s) | Job |
|---|---|---|---|
| S0 | Strategy | `/taste-arbitrage` | What should the words say? Run weak-vs-strong test before any copy is written |
| S1 | Reference | Public galleries (Awwwards, Dribbble, CSSDA, Mobbin) + optional `refero` MCP / `refero-design` skill | Extract palette, type, and layout signals before building anything |
| S2 | Generate | `/evidence-led-frontend` (landing/portfolio) + peer deps for any UI | Build with constraints from S0 and S1 already in hand |
| S3 | Audit | `/evidence-led-frontend` audit pass + peer dep `21st-ui-review` | For existing builds, audit before generating |
| S4 | Verify | Peer dep `/impeccable` | Post-flight. `npm run design:check`. Exit 2 = fix before shipping |
| S5 | Deliver | Peer dep `/scroll-world` (cinematic landing) + `/frontend-design-toolkit` (tool selection) | Deliver the output in the right format |

---

## Routing Logic

When invoked, read the task context and route:

**Copy or positioning is being written or reviewed** → start at S0 (`/taste-arbitrage`)

**Starting a new landing page, portfolio, or redesign** → S1 (gallery reference) → S2 (`/evidence-led-frontend`)

**Existing site being improved** → S3 (`/evidence-led-frontend`, audit before it touches anything) → S4 to verify

**Component or UI in any framework** → S2 (peer dep: `21st-ai` / `21st-ui-build` / `ui-styling`)

**Cinematic scroll landing page** → S5 (peer dep: `/scroll-world`)

**Choosing which tool or skill to use** → S5 (peer dep: `/frontend-design-toolkit`)

**End of any session** → Run the `/mastery-loop` retrospective (2 min)

---

## S0 Strategy: `/taste-arbitrage`

Run before any copy is written. The weak-vs-strong test:
1. Does it lead with an aesthetic claim with no problem named behind it? Weak.
2. Does it name a specific user, workflow, or consequence before describing the interface? Strong.
3. Could a competitor with the same AI tools produce the exact same sentence? If yes, commodity layer.
4. Does it show the decision trail (research → reframe → build) or only the shipped artefact? Trail is strong.
5. Does it connect user need, business goal, and technical constraint in one paragraph? Connected is strong.

---

## S1 Reference: Public Galleries

Pull from these sources before building. Mine for specific decisions, not whole systems.

| Source | What to extract |
|---|---|
| **Awwwards** (`awwwards.com`) | Winning type pairings, layout composition, motion patterns. Filter by year, check site of the day and site of the month for current signals |
| **Dribbble** (`dribbble.com`) | Color palette ideas, micro-interaction patterns, card and UI component details |
| **CSS Design Awards** (`cssdesignawards.com`) | Production-quality interaction and animation references. Look at Special Kudos winners |
| **Mobbin** (`mobbin.com`) | Mobile-first patterns, onboarding flows, navigation patterns. Best for product UI reference |

### Refero (optional, needs the MCP configured)

Refero indexes real shipped product UI, so it answers "how do real products actually solve this" rather than "what looks good in a gallery shot". It is a searchable source, not a replacement for the convergence rule below.

| Tool | Use it for |
|---|---|
| `refero_search_styles` | Visual direction. Start here when the look is undecided |
| `refero_search_screens` | A concrete screen pattern (pricing, settings, empty state, onboarding) |
| `refero_search_flows` | A whole journey across several screens, such as signup or checkout |
| `refero_get_screen_image` | Pull the actual screenshot once a result looks right |
| `refero_get_similar_screens` | Widen the set around one good result before committing |

If the MCP is not connected, the `refero-design` skill still carries the research-first method and craft knowledge offline. Install: `npx skills add https://github.com/referodesign/refero_skill --skill refero-design`

**Extraction method:** Pick 3 sites from any source. For each, note: font family, type scale, primary color + neutral, layout family (grid type, hero layout), motion signature (scroll behavior, hover states). Do not copy markup, extract the visual system.

**Convergence rule:** Where two or more independent references independently use the same type choice, palette signal, or layout pattern, that is the real trend. Weight it.

---

## S2 Generate

### Landing pages and portfolios
Use `/evidence-led-frontend`. It allows exactly two sources for any decision: a measured reference value, or a named checkpoint ID. Anything else must be declared as an assumption out loud.

It emits a decision ledger BEFORE the code. If a run produces markup without a ledger, that run skipped the part that makes the output defensible, and you should push back rather than accept it.

Declare the read first: *"Reading this as a [page kind] for [audience], where the visitor's single next action is [action], and the thing that must land in the first viewport is [claim]."* If you cannot name the action, stop and ask.

### Style presets (the taste-skill family)

`/evidence-led-frontend` is the default and is the only one of these that enforces an evidence trail. Reach for a taste-skill preset instead when the visual direction is already decided and you want that specific language. Load only one preset at a time, they conflict with each other by design. A preset and `/evidence-led-frontend` compose fine: the preset supplies the look, the ledger still has to justify it.

| Skill | Use when |
|---|---|
| `/high-end-visual-design` | It must feel expensive. Softer contrast, generous whitespace, spring motion |
| `/minimalist-ui` | Editorial product UI, Notion or Linear temperament, warm monochrome, flat bento |
| `/industrial-brutalist-ui` | Swiss type, extreme scale contrast, rigid grids, deliberately raw |
| `/gpt-taste` | Driving GPT or Codex rather than Claude. Harder enforcement, higher variance |
| `/stitch-design-taste` | The deliverable is a Google Stitch `DESIGN.md` rather than code |
| `/design-taste-frontend-v1` | v2 broke something specific and you need the old behaviour back |

Image-only skills belong in S1, not here. They emit reference frames, never code: `/imagegen-frontend-web`, `/imagegen-frontend-mobile`, `/brandkit`. `/image-to-code` is the bridge: it generates references, reads them, then implements to match. State the pipeline explicitly in the prompt, for example "generate images, then analyse, then code".

### Any UI (components, product interfaces)

Use the 21st family. It has four distinct jobs and picking the wrong one wastes a round trip.

| Skill | Job |
|---|---|
| `/21st-ui-explore` | Direction undecided. Produces several meaningfully different options |
| `/21st-ai` | Sketch from a prompt, iterate a variant in place, pull the code out |
| `/21st-ui-build` | Direction already chosen. Build production UI against the project's design context |
| `/21st-cli-use` | Search and install existing catalogue components, themes, templates |

Auto-trigger worth knowing: when a project has a `components.json`, search 21st before hand-writing UI.

Refresh all 21st skills with `npx @21st-dev/cli install-skill`.

### Component library / design system
**Peer dependencies:**
```bash
npx ui-skills add baseline-ui
npx ui-skills add fixing-accessibility
npx ui-skills add fixing-motion-performance
```

---

## S3 Audit: `/evidence-led-frontend` (audit pass)

For any existing site. Run before generating. The same skill handles this: point it at existing markup and it diagnoses against the checkpoint gates before it proposes a change. Covers:
- Typography (font swap priority, tracking, scale)
- Color and surfaces (palette cleanup, accent discipline)
- Layout (symmetry, grid, spacing, max-width)
- Interactivity and states (hover, active, loading, empty, error)
- Content (copy quality, fake data, AI tells)
- Component patterns (generic card, three-equal-cards, accordion FAQ)
- Code quality (semantic HTML, inline styles, z-index scale)

**Supplementary audit peer dep:**
```bash
# 21st.dev UI review (lint-style design check)
claude plugin add 21st-dev/21st-ui-review
```

---

## S4 Verify

**Peer dependency:**
```bash
# impeccable (design quality checker)
npx add-skill impeccable/impeccable
```

After wiring, verify runs as:
```bash
npm run design:check
```

Exit code 2 = fix before shipping. Non-negotiable.

---

## S5 Deliver

### Cinematic scroll landing page
**Peer dependency:**
```bash
claude plugin add oso95/scroll-world
```
Generates a scroll-scrubbed landing page using Higgsfield (stills) and Monid (video). Full 8-step pipeline: interview → stills → float → camera architecture → connectors → encode → assemble → QA.

### Tool and skill selection
**Peer dependency:**
```bash
claude plugin add wilwaldon/Claude-Code-Frontend-Design-Toolkit
```
Reference for 70+ frontend tools organized by task, picks the right animation lib, MCP, or install stack for the job.

---

## Peer Dependencies: Install Everything

Bundled in this repo: `/taste-arbitrage`, `/mastery-loop`, and the orchestrator you are reading.

Everything below is third-party and installs separately.

```bash
# Taste-skill family (Leonxlnx). One command installs all of them:
# design-taste-frontend, gpt-taste, high-end-visual-design, minimalist-ui,
# industrial-brutalist-ui, stitch-design-taste, redesign-existing-projects,
# full-output-enforcement, image-to-code, imagegen-frontend-web,
# imagegen-frontend-mobile, brandkit
npx skills add Leonxlnx/taste-skill

# Pin a single one instead, by its install name (not its folder name)
npx skills add Leonxlnx/taste-skill --skill "design-taste-frontend"

# 21st.dev skill family, and how to refresh it later
npx @21st-dev/cli install-skill

# Refero: research-first design method, plus live search of real shipped UI
npx skills add https://github.com/referodesign/refero_skill --skill refero-design
claude mcp add --transport http refero https://api.refero.design/mcp \
  --header "Authorization: Bearer <your-refero-key>"

# Others
claude plugin add oso95/scroll-world
claude plugin add wilwaldon/Claude-Code-Frontend-Design-Toolkit
```

**Install location matters.** `npx skills add` writes to `.agents/skills/` in the current directory and symlinks into Claude Code, so running it from different folders gives you different skill sets. `claude mcp add` without `-s user` is likewise scoped to the current project.

---

## Convergence Rule

Where two or more tools independently flag the same issue, same type problem, same copy weakness, same layout pattern, that is the real signal. Act on it.

---

## Anti-Skipping Rule

Do not invoke S2 (Generate) without running S0 (copy check) and S1 (reference pull). Do not call a build done without S4 (verify). Every skipped stage is a quality debt that shows up in production.
