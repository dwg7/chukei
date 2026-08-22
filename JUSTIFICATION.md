# Why Chukei belongs under `dwg7`

This document exists so that anyone — a DWG7 member browsing the org, a GSI staff pilot user, hfu explaining the project to a colleague, or a future Claude session — has a ready, honest answer to "is this actually DWG7 work, or is someone just using the org's name?" Written for the `dwg7/chukei` session; cross-referenced from `README.md` and `DECISIONS.md` (D12).

## DWG7's own charter, quoted

Per `https://unopengis.org/DWG7.html` (fetched 2026-08-16, during the Staccato UN talk prep — see the sibling `staccato_un_opengis` project's `DECISIONS.md` D16 for the original research):

- **Vision**: "keep web maps open"
- **Mission**: "test new technologies for future geospatial operations"
- Explicitly invites participation from "young professionals, large language model users, and AI systems themselves"
- Describes itself as "an open community of practice"
- Contribution channel: `UNopenGIS/7` on GitHub

## The argument

**1. Mission fit is direct, not analogical.** DWG7's mission is to *test new technologies for future geospatial operations*. Chukei is, literally, a new technology (a generative-AI Staff role) being tested in a real, current geospatial operation (Hokkaido Regional Survey Department staff getting maps for their actual survey work). This isn't a metaphorical stretch of the mission statement — it's close to a restatement of it.

**2. Vision fit holds even though the front door is closed.** 源内 (Gennai) is an internal government tool, not a public one — so it might look like this narrows access rather than keeping maps open. But look at what Gennai actually calls: an open-source Cartographer (`dwg7/spiccato`, CC0), an open-source, openly-licensed catalog (`hfu/layers-martin`, CC0, built from GSI's own open data), and an open architecture spec (`UNopenGIS/staccato-spec`). The *AI front end* is necessarily closed (it has to be, to reach government staff on their approved tooling), but the entire map-delivery stack behind it stays exactly as open as DWG7's vision asks for. Chukei is a closed door that opens onto an open house.

**3. The charter explicitly invites this kind of participant.** DWG7's own page names "large language model users" and "AI systems themselves" as welcomed contributors — not as a hypothetical, forward-looking aspiration, but as current, stated scope. A prompt that turns a government AI system into a geospatial operations tool is about as literal an instance of that invitation as exists.

**4. Institutional lineage is direct and traceable, not asserted.** Chukei is not an unrelated project parked under `dwg7` for convenience — it's a narrow, documented fork of work already living in the org (`dwg7/spiccato`'s `GENNAI_PROMPT.md` and its build script; see `DECISIONS.md` D6-D10). Anyone can `git log` or `git blame` their way from Chukei back to spiccato and see the derivation is real, not claimed.

**5. This is how the working group's own operating model works.** DWG7 describes itself as "an open community of practice," not a body that commissions work top-down and ratifies it by vote. hfu is a DWG7 member (his contributions trace back through `UNopenGIS/7`'s own issue history). A member building and sharing an experiment in the group's shared space, openly, is not a deviation from how DWG7 operates — it *is* how DWG7 operates. The same is true of `staccato-spec` and `spiccato`, both already hosted the same way.

**6. There's a public paper trail, and it predates Chukei.** hfu's UN Open GIS Initiative Featured Talk (2026-08-19), given as a DWG7 member, closed with two named next steps: "a smarter staff" and "a bigger library." That commitment was made publicly, in a DWG7-affiliated context, before Chukei existed. Chukei is the direct, first execution of "a smarter staff" — not a retroactive justification dressed up after the fact.

## The honest caveat — don't overclaim this

None of the above makes Chukei an **officially ratified DWG7 deliverable** in the sense of something the working group as a body reviewed and approved. It hasn't been. Neither has `staccato-spec`, and DWG7's own public page (as of the 2026-08-16 research) makes no mention of Staccato, Spiccato, or hfu by name. If asked directly — by a GSI colleague, in the lightning talk Q&A, or by anyone else — the accurate answer is:

> "This is a DWG7 member's experiment, built openly in DWG7's shared space, directly testing DWG7's own stated mission. It isn't an officially adopted DWG7 standard or deliverable — and that's fine, because DWG7 doesn't operate by top-down ratification. It operates by members building things in the open."

Say that plainly rather than implying formal endorsement that doesn't exist. This mirrors the same honest positioning already established for `staccato-spec` (see the sibling `staccato_un_opengis` project's `DECISIONS.md` D16 and its speaker-notes Q&A prep) — consistency here matters more than sounding more official than the project actually is.
