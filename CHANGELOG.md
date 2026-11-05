# Changelog

## 1.5.0 · 5 November 2026

A batch of capabilities the stack was missing, added as original method. The ideas were sharpened by studying two strong peer skills, a design skill and a video-writing skill, nothing was copied from either.

### Added
- **Structure before surface** in S2. Settle the first viewport in grayscale (hierarchy, the one focal point, the primary action, and the empty, loading, and error states) before type or colour, and name the left-right split reflex as the tell it is. Choose the skeleton before the copy that fills it.
- **Comparing directions** in S1 and S2. When the direction is genuinely open, build two or three distinct directions on the same content, put them side by side, and choose with a reason recorded in the ledger.
- **Interface motion** in S2. The three motions almost any interface needs: feedback on the primary action, the origin of a state change, and a staggered entrance. One signature move past that, no idle pulsing.
- **Reference discipline** in S1. Keep product references (what it should feel like) apart from interaction references (how a pattern behaves), and measure the real viewport rather than the image's pixels.
- **Copy tells** in S0. The machine-written shapes to cut on sight: "not X but Y", one-word dramatic sentences, a metaphor standing in for a fact, and category marketing words a rival could run unchanged.
- **Hook craft** in S2M, generalised to any opening. The four ways a hook fails (slow lead-in, wording to decode, aimed at no one, a tease with no payoff), which kill a page hero as surely as a video hook.
- **Motion craft rules** in S2M: one accent per piece, graphics that draw themselves, 0.15 to 0.25s entrances, change every two to three seconds on the words, nothing pulsing to fill dead air.
- **Scroll landings** in S2M: two musts (content-driven section entrances and one scroll-driven beat), with the technique picked from the page's own material rather than a default pinned zoom.
- **Look at the real frames** and **Walk the task** in S4. Render and review the actual screenshots with an independent reviewer who grades against an anchor and states what they could not check, and for anything with a flow, walk the task on the running page and mark where a user gets stuck, takes a wrong turn, or hesitates. Looking good and working are separate sign-offs.

## 1.4.0 · 5 November 2026

Self-contained. The stack used to route several stages to third-party skills and tools as peer dependencies. It now stands entirely on its own four skills, so there is nothing external to install and the whole six-stage chain works after a single clone.

### Removed
- The "wider ecosystem" and "peer dependencies" install lists, and every third-party pointer in the orchestrator: taste-skill and its style presets, the 21st.dev family, Refero, scroll-world, the frontend design toolkit, the `impeccable` verify step, HyperFrames, and the `ui-skills` component packs.

### Changed
- **S2 Generate** now covers component and product UI with the same ledger-and-gates discipline, tool-agnostic, instead of routing to a third-party component skill.
- **S2M Motion** describes the build as a deterministic, seek-safe render in whatever renderer you use, with no named install.
- **S4 Verify** runs the checkpoint gates from `evidence-led-frontend` directly (contrast, focus, CTA hierarchy, consistency, factual groundedness) and the motion render check, rather than wiring in an external checker.
- **S5 Deliver** carries its own static and motion delivery rules.
- README, stage table, and `THIRD-PARTY-NOTICES.md` rewritten to match. The repo is now fully original with no peer-dependency list.

## 1.3.0 · 5 November 2026

Motion is now a stage. The stack covered static interfaces end to end and said nothing about work that moves, so a reel, an explainer, a promo, or an animated title fell outside it. This closes that gap.

### Added
- **S2M Generate: Motion**, a new branch of Generate for any deliverable that moves. Original work, no vendored skills. Four steps: a doctrine gate (name the job of every motion or cut it), a script pass for anything narrated (hook, stakes, promise, beats, re-hooks, proof, payoff, scored and rewritten until it holds), a build-and-edit pass that keeps the render reproducible and the footage matched to the voiceover, and an audio pass on licensed music cut to the beat.
- **Verify by render** in S4. A motion piece is not done because the build passed. Render it and pull frames across the whole run: captions readable over the footage, no card flash at the edges, footage matching the spoken line, moves landing on the beat.
- **Motion delivery** in S5. The right aspect per platform, faststart, and the caption file, alternate hooks, and facts sheet handed over so the next edit does not start cold.

### Changed
- Stage map, routing logic, and the anti-skipping rule now carry the motion path. README stage table and tagline updated to match.
- HyperFrames referenced as the build peer dep (`npx skills add heygen-com/hyperframes`). Script and motion-direction craft come from peer skills installed separately, in keeping with the repo rule that stages are the product and skills are swappable.

---

## 1.2.1 · 14 September 2026

Repository renamed to `Design-Intelligence-Skill`.

### Changed
- Clone URL in the README, and `homepage` and `repository` in `plugin.json`, now point at the new name.
- The local git remote was still pointing at `kish-design-intelligence`, two renames behind. GitHub redirected it, which is why nothing appeared broken. Updated.

Nothing about the skills changed. The plugin name and the slash command are still `design-intelligence`, so no reinstall is needed. GitHub redirects the old URLs, but anything hardcoding them should be updated rather than relying on that.

---

## 1.2.0 · 14 September 2026

The repo is now entirely original work. No vendored skills.

### Added
- **`evidence-led-frontend`**, a new S2 generate skill written from scratch. It allows exactly two sources for any design decision: a measured reference value, or a named checkpoint ID from the MX/BX/AIX framework. Anything else has to be declared as an assumption. It emits a decision ledger *before* the code rather than after.
  - Measured baseline built from this project's own extraction runs against four live sites on 2026-07-26: display type 101px to 172px, no Inter, no pure black or white, one hot accent or none.
  - Checkpoint gates mapped to real framework IDs (`acc_01`, `acc_02`, `acc_03`, `acc_06`, `cvr_01`, `cvr_03`, `con_01` as hard gates, nine more as should-pass).
  - Anti-pattern list reframed as counter-evidence, so every entry states a reason you can argue with instead of a rule to obey.

### Removed
- `skills/design-taste-frontend/` and `skills/redesign-existing-projects/`, which were verbatim copies of [Leonxlnx/taste-skill](https://github.com/Leonxlnx/taste-skill). `evidence-led-frontend` replaces the need for them. Install taste-skill directly if you want the style presets, they compose well with this repo.

### Changed
- README, orchestrator routing, and `THIRD-PARTY-NOTICES.md` updated to match. The Settings section is now The Decision Ledger.

---

## 1.1.0 · 14 September 2026

Documentation and compliance pass. No skill behaviour changed.

### Added
- `LICENSE` (MIT). The repo previously shipped with no license file at all while the README claimed MIT.
- `THIRD-PARTY-NOTICES.md`, with the required copyright notice for the two skills redistributed from [Leonxlnx/taste-skill](https://github.com/Leonxlnx/taste-skill).
- `assets/banner.svg`, a Designerama-branded README banner.
- `CHANGELOG.md`, this file.
- `.claude-plugin/marketplace.json`, so the repo can be added as a Claude Code marketplace.

### Fixed
- **Install commands pointed at a repository that does not exist.** The README told people to clone `kishanrama/kish-design-intelligence`. The actual repo is `Verifux/Design-Intelligence`. Anyone following the old README got a 404.
- **Attribution.** `design-taste-frontend` and `redesign-existing-projects` were presented as included alongside the original skills, with no credit to upstream. They are now labelled as redistributed, with a link to the source and the reason they are vendored.
- `plugin.json` name and homepage now match the real repository.
- Removed every em dash and en dash from the documentation, matching the rule the skills themselves enforce.

### Changed
- README rewritten: stage table, skills split into original versus redistributed, a "which one should I use" section, the three dials documented, and an ecosystem section covering taste-skill, 21st.dev, and Refero.

---

## 1.0.0 · 30 July 2026

Initial release.

- Six-stage orchestrator (`design-intelligence`) with routing and an anti-skipping rule.
- `taste-arbitrage`: five-question weak-vs-strong copy test.
- `mastery-loop`: session operating system with named weakness patterns.
- `design-taste-frontend` and `redesign-existing-projects` vendored in.
- `references/public-gallery-sources.md`: extraction guides for Awwwards, Dribbble, CSS Design Awards, and Mobbin.
