# Changelog

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
