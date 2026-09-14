# Third-party notices

**Nothing in `skills/` is third-party.** Every skill in this repository is original
work. There is no vendored code and no redistributed content, so this file exists
to record what is *referenced* rather than what is included.

---

## Referenced, not redistributed

These are named in the documentation and installed separately by the user. No
files from them are copied into this repository.

| Project | Source | Relationship |
|---|---|---|
| taste-skill | [Leonxlnx/taste-skill](https://github.com/Leonxlnx/taste-skill) | Composes with this repo. It provides visual style presets, this repo provides sequence and evidence. The README structure here follows its example. |
| 21st.dev skills and CLI | [21st.dev](https://21st.dev) | S2 component generation and catalogue search |
| Refero design skill and MCP | [referodesign/refero_skill](https://github.com/referodesign/refero_skill) | S1 reference research |
| scroll-world | [oso95/scroll-world](https://github.com/oso95/scroll-world) | S5 cinematic delivery |
| Claude Code Frontend Design Toolkit | [wilwaldon/Claude-Code-Frontend-Design-Toolkit](https://github.com/wilwaldon/Claude-Code-Frontend-Design-Toolkit) | S5 tool selection |

### History

Version 1.0.0 of this repository vendored two skills from taste-skill
(`design-taste-frontend` and `redesign-existing-projects`) so the six-stage chain
would work after a single clone. Version 1.2.0 replaced them with
`evidence-led-frontend`, which is original work built on this project's own
measured reference data and checkpoint framework. Those two files are no longer
present. Credit for them belongs to Leonxlnx, and the upstream repository remains
the place to get them.

---

## Sources cited in the skills

`evidence-led-frontend` and `references/public-gallery-sources.md` cite measured
observations from live public websites (Benjamin Creative, PZ Studio, Media.Monks,
Red Collar) and name four public galleries (Awwwards, Dribbble, CSS Design Awards,
Mobbin) as research sources.

Those citations are original measurements: font families, computed display sizes,
and colour values extracted from the rendered pages with a script. No assets,
markup, stylesheets, or copy from any of those sites are reproduced here, and
none of the cited sites are affiliated with or endorse this project.
