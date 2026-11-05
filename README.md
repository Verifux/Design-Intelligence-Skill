<p align="center">
  <img src="assets/banner.svg" alt="Design Intelligence Skill, a six stage design stack for Claude Code" width="100%" />
</p>

<h1 align="center">Design Intelligence Skill</h1>

<p align="center">
  <em>Six stages between a brief and work that does not look generated, static or in motion.</em>
</p>

<p align="center">
  <a href="LICENSE"><img src="https://img.shields.io/badge/license-MIT-cc2a3f?style=for-the-badge&labelColor=0a0a0a" alt="MIT License" /></a>
  &nbsp;
  <a href="#install"><img src="https://img.shields.io/badge/claude%20%C2%B7%20codex%20%C2%B7%20cursor-ready-cc2a3f?style=for-the-badge&labelColor=0a0a0a" alt="Claude, Codex, Cursor" /></a>
  &nbsp;
  <a href="CHANGELOG.md"><img src="https://img.shields.io/badge/changelog-read-cc2a3f?style=for-the-badge&labelColor=0a0a0a" alt="Changelog" /></a>
</p>

Most AI design tooling is a pile of skills with no opinion about when to use which one. This is the opposite: an **orchestrator** that reads your task and routes it through six stages in order, so reference work happens before generation and verification happens before you call it done.

The stages are the product. Four original skills carry them, and there is nothing else to install.

<p align="center"><sub><a href="#install">Install</a> · <a href="#the-six-stages">Stages</a> · <a href="#whats-in-this-repo">Skills</a> · <a href="#which-one-should-i-use">Which one</a> · <a href="#the-decision-ledger">Ledger</a> · <a href="#common-questions">FAQ</a> · <a href="#license">License</a></sub></p>

---

## Install

```bash
git clone https://github.com/Verifux/Design-Intelligence-Skill.git ~/.claude/plugins/design-intelligence
```

Or drop a single `SKILL.md` into `~/.claude/skills/` and use it on its own. Every skill here is a standalone portable file with no build step and no runtime.

Then start any design session with the orchestrator:

```
/design-intelligence build a landing page for a B2B SaaS tool
```

It reads the task, picks the stage, and pulls in the right skill. You do not have to remember the map.

---

## The six stages

| Stage | Name | Job | Skill or method |
|---|---|---|---|
| **S0** | Strategy | What should the words say? Weak-vs-strong test before a line of copy is written | `/taste-arbitrage` |
| **S1** | Reference | Extract type, palette, and layout signals from real work before building | Public galleries + your own extraction |
| **S2** | Generate | Build with the constraints from S0 and S1 already in hand | `/evidence-led-frontend` |
| **S2M** | Generate · Motion | When the deliverable moves: name the job of each motion, write the hook, build so the render reproduces | The motion method |
| **S3** | Audit | For existing builds, diagnose before you touch anything | `/evidence-led-frontend` audit pass |
| **S4** | Verify | Post-flight. A build is not done because it renders | The checkpoint gates + render check |
| **S5** | Deliver | Ship it in the right format, hand it over warm | The delivery method |

**Anti-skipping rule.** Do not invoke S2 without running S0 and S1. Do not call a build done without S4. Every skipped stage is quality debt that surfaces in production, usually in front of a client.

**Convergence rule.** Where two or more independent checks flag the same issue, that is the real signal. Act on it. Where only one does, investigate before you rewrite anything.

---

## What's in this repo

Everything here is original to this project. Nothing is vendored in, and nothing third-party has to be installed for the stack to work end to end.

| Skill | Install name | What it does |
|---|---|---|
| **orchestrator** | `design-intelligence` | The entry point. Reads a task, routes it to the right stage, enforces the anti-skipping rule. Start here. |
| **evidence-led-frontend** | `evidence-led-frontend` | S2 and S3. Builds and audits landing pages and portfolios where every decision traces to a measured reference value or a named audit checkpoint, and emits the trail as a decision ledger before the code. |
| **taste-arbitrage** | `taste-arbitrage` | S0. Copy and positioning. Runs any line through a five-question weak-vs-strong test. Built on the thesis that AI commoditised execution, so judgment is the scarce skill and the copy should show the decision trail, not the artefact. |
| **mastery-loop** | `mastery-loop` | Session operating system. Observe, extract, encode, apply, measure, repeat. Names the failure patterns directly: planning-as-avoidance, waiting for perfect conditions, silent stall. |

The motion method (S2M), the verify gates (S4), and the delivery rules (S5) live in the orchestrator itself, so the four skills plus the orchestrator are the whole kit.

### Why evidence-led-frontend is different

Most anti-slop skills are a list of preferences. A model's preferences are the statistical centre of everything it has seen, and the centre is the slop, so a preference list fights the problem with the thing causing it.

This one allows exactly two sources for any decision: a measured value pulled off a live site with a script, or a named checkpoint from the MX/BX/AIX framework (`acc_01`, `cvr_03`, `aix_04` and the rest), the same ones a [Verifux](https://verifux.app) audit scores against. Anything with neither source is a default wearing a decision's clothes. The skill makes the agent write the ledger **before** the code, which is also what makes the output defensible in front of a client rather than just pretty.

---

## Which one should I use?

- Starting any design session at all, reach for **`/design-intelligence`** and let it route.
- Writing or reviewing **words** (positioning, a case study, a proposal), use **`/taste-arbitrage`** before you design anything around them.
- Building a **new landing page or portfolio**, use **`/evidence-led-frontend`**.
- Working on **something that already exists**, still use **`/evidence-led-frontend`**, but let it audit before it touches anything. Generating first is how a redesign quietly becomes a rewrite.
- Something that **moves** (a reel, explainer, promo, animated title), route through the **Motion** stage: name the job of each move, write the hook, build so the render reproduces, and verify by pulling frames.
- Reviewing **how you work** rather than what you built, use **`/mastery-loop`** at the start or end of a session.

Scope limit worth stating plainly: `evidence-led-frontend` is tuned for landing pages, portfolios, marketing sites, and overhauls of those. For dashboards, data tables, and multi-step product UI, keep its ledger and gates but drop the large-display-type baseline, which is wrong for dense UI.

---

## The decision ledger

`evidence-led-frontend` emits this table **before** it writes any code. Every row is `measured` or `checkpoint`. There is no third category, and anything that fits neither has to be declared as an assumption out loud.

| Decision | Value | Source | Type |
|---|---|---|---|
| Display face | Cabinet Grotesk | No standing ref uses Inter; one face, own voice | measured |
| Display size | 108px | Standing refs measure 101 to 172px | measured |
| Ground | `#0F0E0D` | Refs never use pure black; warm-tinted | measured |
| Accent | `#EA3718`, used 3 times | One hot accent, frequency not hue | measured |
| CTA position | Above fold, single primary | `cvr_01` CTA hierarchy | checkpoint |
| Focus ring | 2px, 3:1 on both grounds | `acc_02` focus indicators | checkpoint |

Two or three assumptions on a page is normal. Twelve means the agent is designing from defaults and calling it a ledger.

It also opens with the read, one sentence, before anything else: *"Reading this as a [page kind] for [audience], where the visitor's single next action is [action], and the thing that must land in the first viewport is [claim]."* Getting that sentence wrong is cheap. Getting it wrong silently, after 400 lines of CSS, is not.

---

## Reference sources

`references/public-gallery-sources.md` carries extraction guides for four public galleries:

| Source | What to pull from it |
|---|---|
| **Awwwards** | Layout composition, type pairings, motion patterns. Filter by industry, not Site of the Day. A B2B winner beats an agency showpiece |
| **Dribbble** | Palette ideas and single component details. Never a full page layout. Shots are pictures of interfaces, not interfaces |
| **CSS Design Awards** | Production-quality interaction, with published per-entry criteria so you can read why something scored |
| **Mobbin** | Mobile-first patterns, onboarding flows, real product UI states |

Extraction method: pick three sites, and for each note the font family, type scale, primary plus neutral colour, layout family, and motion signature. Extract the system. Never copy the markup.

---

## What this is not

- Not a component library. There is no code to import.
- Not a dashboard or data-UI system. It adapts to dense UI, but mature systems (Fluent, Carbon, Atlassian) already encode years of decisions for those.
- Not a Figma plugin.
- Not a replacement for judgment. It routes the work and enforces the order. It cannot tell you whether the idea was worth building.

---

## Common questions

**How is this different from the other AI design skills?**
Most of them are a single skill with strong opinions about aesthetics. This is an orchestrator with strong opinions about *sequence*. Reference before generation, a sourced decision before code, verification before you call it done.

**Do I need anything else installed?**
No. The four skills here run standalone and cover all six stages end to end. There is no peer-dependency list to chase.

**Does it work outside Claude Code?**
Yes. Every skill is a portable `SKILL.md`. Codex, Cursor, and anything else that reads agent skills can use them, and you can paste one into a chat directly.

**Why is the em dash banned?**
It is one of the most reliable tells of unedited model output. The rule is enforced in the skills and held to in this README.

---

## Credits

The orchestrator, `evidence-led-frontend`, `taste-arbitrage`, and `mastery-loop` are original work by [Kishan Rama](https://designerama.co.za) / Designerama.

The measured reference values come from original extraction runs against four live sites, and the checkpoint IDs come from the [Verifux](https://verifux.app) MX/BX/AIX framework.

---

## License

[MIT](LICENSE) © 2026 Kishan Rama / Designerama.

Everything in this repository is original to this project.
