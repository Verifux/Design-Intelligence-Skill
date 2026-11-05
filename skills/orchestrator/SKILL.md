---
name: design-intelligence
description: "6-stage design intelligence orchestrator. Routes any UI, copy, or product design task through the right skill at the right stage: S0 Strategy, S1 Reference, S2 Generate, S3 Audit, S4 Verify, S5 Deliver. Load this first at the start of any design or product session."
argument-hint: "[task description or stage name]"
allowed-tools: Bash, Read, Write, Edit, AskUserQuestion, Skill
---

# Design Intelligence Stack: Orchestrator

6 stages. Every UI, copy, and product design task routes through this chain. Do not skip stages, each one is a quality gate.

Everything this orchestrator routes to is in this repo. Four original skills, MIT, no third-party installs required. The stages are the product, and the discipline is the order and the gates, not a particular tool.

---

## Stage Map

| Stage | Name | Skill or method | Job |
|---|---|---|---|
| S0 | Strategy | `/taste-arbitrage` | What should the words say? Run the weak-vs-strong test before any copy is written |
| S1 | Reference | Public galleries + your own extraction run | Pull palette, type, and layout signals off real sites before building anything |
| S2 | Generate | `/evidence-led-frontend` | Build with the constraints from S0 and S1 already in hand, ledger before code |
| S2M | Generate · Motion | The motion method below | When the deliverable moves. Name the job of each motion, write the hook, build so the render reproduces |
| S3 | Audit | `/evidence-led-frontend` (audit pass) | For an existing build, diagnose against the gates before you touch anything |
| S4 | Verify | The checkpoint gates + the render check | Post-flight. A build is not done because it renders |
| S5 | Deliver | The delivery method below | Ship the output in the right format and hand it over so the next edit starts warm |

---

## Routing Logic

When invoked, read the task context and route:

**Copy or positioning is being written or reviewed** → start at S0 (`/taste-arbitrage`)

**Starting a new landing page, portfolio, or redesign** → S1 (gallery reference) → S2 (`/evidence-led-frontend`)

**Existing site being improved** → S3 (`/evidence-led-frontend`, audit before it touches anything) → S4 to verify

**A component or product UI** → S2 (`/evidence-led-frontend` discipline, the any-UI note below)

**Direction genuinely undecided** → S1 → S2, build two or three distinct directions on the same content and compare them side by side before committing

**Any deliverable that moves** (reel, short, explainer, promo, title card, animated UI, scroll-scrubbed film) → S2 → **S2M Motion** before a frame is rendered

**End of any session** → run the `/mastery-loop` retrospective (2 min)

---

## S0 Strategy: `/taste-arbitrage`

Run before any copy is written. The weak-vs-strong test:
1. Does it lead with an aesthetic claim with no problem named behind it? Weak.
2. Does it name a specific user, workflow, or consequence before describing the interface? Strong.
3. Could a competitor with the same AI tools produce the exact same sentence? If yes, commodity layer.
4. Does it show the decision trail (research → reframe → build) or only the shipped artefact? Trail is strong.
5. Does it connect user need, business goal, and technical constraint in one paragraph? Connected is strong.

### Copy tells to cut
The test above judges whether a line says anything. These shapes give away that a machine wrote it, cut them on sight:
- "Not X but Y", and "not just X but Y". Say Y.
- One-word dramatic sentences ("Panic." "Simple." "Wild."). One per piece at most.
- A metaphor standing in for a fact ("a goldmine", "the secret sauce"). Say the plain fact.
- Category marketing words a rival could run unchanged ("Elevate", "Seamless", "Transform your workflow").

Score every headline, hook, and body line against the test and these tells, then rewrite until it passes. A first draft that reads clean has usually just hidden the tells better.

---

## S1 Reference: Public Galleries

Pull from these public sources before building. Mine for specific decisions, not whole systems.

| Source | What to extract |
|---|---|
| **Awwwards** (`awwwards.com`) | Winning type pairings, layout composition, motion patterns. Filter by year, check site of the day for current signals |
| **Dribbble** (`dribbble.com`) | Color palette ideas, micro-interaction patterns, card and component details. Never a full page layout |
| **CSS Design Awards** (`cssdesignawards.com`) | Production-quality interaction references, with published per-entry criteria so you can read why it scored |
| **Mobbin** (`mobbin.com`) | Mobile-first patterns, onboarding flows, real product UI states |

**Extraction method.** Pick 3 sites. For each, note: font family, type scale, primary color and neutral, layout family (grid type, hero layout), and motion signature (scroll behavior, hover states). Do not copy markup, extract the visual system. Measure the values with a script rather than recalling them, so S2 has real numbers to build from.

**Keep two kinds of reference apart.** A *product reference* says what the thing should feel like, the voice, the palette, the density. An *interaction reference* says how one pattern should behave, a filter, a stepper, an onboarding flow. Mixing them is how a page ends up looking like one site and working like another. Pull each from the right source and label which is which.

**Measure the real viewport, not the image.** A 2x screenshot has twice the pixels of the viewport it came from, so halve it. If you cannot tell the capture width, say what you assumed. A number measured at the wrong width is worse than no number, because it looks exact.

**Convergence rule.** Where two or more independent references use the same type choice, palette signal, or layout pattern, that is the real trend. Weight it. Where only one does, investigate before you copy it.

---

## S2 Generate

### Landing pages and portfolios
Use `/evidence-led-frontend`. It allows exactly two sources for any decision: a measured reference value, or a named checkpoint ID. Anything else must be declared as an assumption out loud.

It emits a decision ledger BEFORE the code. If a run produces markup without a ledger, that run skipped the part that makes the output defensible, and you should push back rather than accept it.

Declare the read first: *"Reading this as a [page kind] for [audience], where the visitor's single next action is [action], and the thing that must land in the first viewport is [claim]."* If you cannot name the action, stop and ask.

### Structure before surface
Before type and colour, settle the structure in grayscale. Lay out the first viewport with no colour and no final type: the hierarchy, the one thing the eye should land on, the primary action, and the empty, loading, and error states. If it does not read in grayscale, it will not read in colour. Colour and type sharpen a structure that already works, they cannot rescue one that does not. Fix the layout here, where changes are cheap, before you spend a decision on a typeface.

The reflex to watch is the left-right split, text one side and an image the other. The model reaches for it before a word of copy is written, which is exactly why it reads as templated. Choose the first-viewport skeleton on purpose, where the eye enters, what carries the weight, where the one action sits, before you write the copy that fills it.

The first viewport is a hook. It has to say what this is and who it is for inside a second or two, and the things that kill a video hook kill a hero too (see the hook killers in S2M): a slow lead-in, wording the reader has to decode, or a claim aimed at no one in particular.

### When the direction is undecided
When the visual direction is genuinely open, do not marry the first idea. Build two or three distinct directions on the same real content and the same first viewport, then put them side by side and choose with a reason. Distinct means they disagree about something that matters, the type voice, the density, how loud the accent runs, not three tints of one idea. Keep the content identical across them so you are comparing directions and not copy. Record why the winner won in the ledger. One direction deepened still beats three half-built ones, so diverge only when the choice is real, then converge fast.

### Interface motion
Three motions earn their place in almost any interface, and a screen that skips them feels broken rather than calm:
1. **Feedback on the primary action.** The press gets an immediate response, completion hands back a result.
2. **The origin of a state change.** When something opens, selects, or enters a list, show where it came from so the user is not guessing what just happened.
3. **The entrance.** Content arrives in a short staggered reveal, not all at once, which reads as a page load.

Everything past these three is a signature move, and one per screen is the limit. Animate transform and opacity, keep entrances at 0.15 to 0.25s, honour `prefers-reduced-motion`, and never leave a box idly pulsing to fill space.

### Any UI (components, product interfaces)
The same discipline carries, the scope changes. `/evidence-led-frontend` is tuned for marketing pages, so for a component or a product screen, keep the ledger and the gates but drop the large-display-type baseline, which is wrong for dense UI. Build against whatever component tooling the project already has, the ledger still governs every decision. If the project has a design system, read it first and inherit it rather than inventing a parallel one.

### Direction already decided
When the visual language is already chosen, you can skip the reference hunt and go straight to building. The ledger does not get skipped with it. Every decision still names its source, even when the source is "the brand system says so."

---

## S2M Generate: Motion

The static stages assume the output holds still. When the deliverable moves, Generate routes through here first. That covers a social reel or short, an explainer, a product promo, an animated title card, a motion detail inside a UI, and a scroll-scrubbed film. Motion is a quality gate like every other stage, not a flourish added at the end.

One rule governs all of it: every motion does a job or it is cut. A move either directs attention, shows a change or a relationship, or carries a beat of the story. Motion that only breathes, idle drift and decorative loops, is cost with no return. Decide the job before you animate the thing.

**1. Doctrine gate.** Before a single frame, write down what each motion is for. If you cannot name the job, the move does not belong. This gate is what stops a piece from becoming a showreel of easing curves with nothing to say.

**2. Script, for anything narrated.** A video with a voice or captions lives or dies on its first three seconds. The hook names a clear subject and opens a gap the viewer needs closed. Then stakes (why it matters to them), a promise (what they get by the end), beats that each land one concrete thing, a new reason to stay every few seconds, real proof near the end, and a payoff that closes the opening gap followed by one ask. Score the draft against clarity, curiosity and truth, strip the tells that make writing sound machine-made, and rewrite until it holds. Real numbers only, each with a source. If the user handed you a hook, it wins and you build under it. The hook has four common ways to fail, each losing the viewer in the first second: a slow lead-in before the topic ("this is one of the craziest things"), wording they have to decode, a topic aimed at no one in particular, and a tease the payoff never earns. Name the viewer and the gap in plain words, fast.

**3. Build and edit.** Compose so the render reproduces: one timeline, seek-safe, the same input giving the same frames every run. Theme the accent to the brand instead of shipping a default. Footage and B-roll have to match the line being spoken, because a cutaway that contradicts the voiceover reads worse than no cutaway at all. For a talking-head cut into a short: cut to the narration, caption with word-level timing, and keep every card clear of the frame edges. The craft rules that separate a cheap cut from an expensive one: one accent colour for the whole piece, graphics that draw or grow themselves rather than just appearing, entrances at 0.15 to 0.25s, something changing every two to three seconds and landing on the words, and nothing pulsing to fill dead air. If a stretch has nothing to change, the edit is too long, tighten it.

**4. Audio.** A narration voice, a music bed, and cuts that land on the beat. The music has to be licensed for the use. A placeholder track is for checking timing and never ships.

The frames animate the same evidence a static page does, so the motion inherits the palette, type, and accent discipline from S1 and S2 rather than starting a new look.

### Scroll landings
For a landing, brand, or launch page built to persuade, the scroll is the motion. Two things have to be present: sections that enter on the content below the fold, and at least one scroll-driven beat where the main subject visibly changes as you move. Pick the technique from the page's own material, a wordmark collapsing into the nav, a background that shifts by chapter, a line of copy lighting up word by word, rather than defaulting to a pinned hero that zooms. Documents, tools, and dashboards do not get this.

---

## S3 Audit: `/evidence-led-frontend` (audit pass)

For any existing site. Run before generating. The same skill handles this: point it at existing markup and it diagnoses against the checkpoint gates before it proposes a change. Generating first is how a redesign quietly becomes a rewrite.

Covers:
- Typography (font swap priority, tracking, scale)
- Color and surfaces (palette cleanup, accent discipline)
- Layout (symmetry, grid, spacing, max-width)
- Interactivity and states (hover, active, loading, empty, error)
- Content (copy quality, fake data, AI tells)
- Component patterns (generic card, three-equal-cards, accordion FAQ)
- Code quality (semantic HTML, inline styles, z-index scale)

---

## S4 Verify

A build is not done because it renders. Run the checkpoint gates from `/evidence-led-frontend` against it, in this order:

- **Contrast** (`acc_01`). Body text at 4.5:1, large text at 3:1. Measure it, do not eyeball it.
- **Focus** (`acc_02`). Tab through the page. If you lose the cursor, it fails.
- **Image and icon accessibility** (`acc_03`), **text sizing** (`acc_06`).
- **CTA hierarchy** (`cvr_01`) and **value-proposition clarity** (`cvr_03`). The first viewport says what this is and who it is for, with one primary action.
- **Visual consistency** (`con_01`). No second type scale or second grey family appears mid-page.
- **Factual groundedness** (`aix_04`). No invented statistic, customer name, or fake testimonial. Placeholders are labelled as placeholders.

Fix what fails. Report what you could not fix and why. A gate you skipped is a gate that fails in front of a client.

### Look at the real frames
The gates above are necessary and not sufficient. Render the page at the real viewports (a narrow phone, a tablet, a laptop, a wide screen) and look at the actual screenshots, not the code and not the editor preview. Tab through it on the keyboard and watch the focus move. Reading the markup tells you what you intended; the frame tells you what shipped, and the gap between the two is where the templated tells hide. Where you can, hand the frames to a second reviewer working without your context, a fresh agent or a person, because the author is the worst judge of whether their own page reads. A reviewer who finds nothing says so, and does not invent changes to look useful. They grade against a fixed anchor, take the lower grade when unsure, separate a real defect from a matter of taste, and state plainly what they could not check. A static screenshot is not proof that the motion or the flow works, only that the frame does. A green build is not evidence. The frames are.

### Walk the task
Looking good and working are different sign-offs. For anything with a real flow, a form, a multi-step process, anything that saves something, walk the task on the running page before you call it done: enter at the real starting point and go through to the result. Mark every spot where you get stuck, take a wrong turn, or have to stop and guess. At each step, can you tell whether you are waiting, done, or have failed, and does the feedback show up next to what you did? Report the few issues that block the main task, not a list of everything. Do not read a real person's speed off how long the walk took.

### Motion: verify by render

A motion piece is not done because the build passed or the timeline looks right in the editor. Render it, then open the actual output and pull frames across the whole run. Check that the captions stay readable over the busiest footage, that no card flashes at a frame edge, that the footage matches what is being said at that second, and that the key moves land on the beat. A green build is not evidence. The rendered frames are.

---

## S5 Deliver

Ship the output in the format the destination expects, and hand it over so the next person does not start cold.

**Static pages.** Semantic HTML, a real heading order, no placeholder comments left in, and the decision ledger alongside the code so a reviewer can see why each choice was made.

**Motion.** The aspect the platform expects: 9:16 for a reel, short, or TikTok, 16:9 for YouTube and most embeds. Write faststart so it plays before it finishes downloading. Hand over the caption file, two alternate hooks, and the facts sheet with its sources.

**Everything.** Say plainly what is verified and what is still an assumption. A deliverable that hides its open questions is the expensive kind, because it looks finished.

---

## Convergence Rule

Where two or more independent checks flag the same issue, same type problem, same copy weakness, same layout pattern, that is the real signal. Act on it. Where only one does, investigate before you rewrite anything.

---

## Anti-Skipping Rule

Do not invoke S2 (Generate) without running S0 (copy check) and S1 (reference pull). Do not call a build done without S4 (verify). Do not render a motion piece before the doctrine gate, and for anything narrated, before the script passes its checks; do not call a render done off a green build, pull frames from the output first. Every skipped stage is a quality debt that shows up in production.
