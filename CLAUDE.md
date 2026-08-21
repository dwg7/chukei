# Chukei — Project Context

This file is persistent context for Claude Code sessions working in this repository (`/Users/hfu/Downloads/chukei`, `dwg7/chukei` on GitHub). If a session starts here, read this file, then read `HANDOVER.md` for the current status.

**Language convention**: documentation, code, comments, commit messages, and DECISIONS.md/HANDOVER.md entries in this repo are written in **English** — `dwg7` (like its sibling `dwg7/spiccato`) is treated as an international project. The generated artifact itself — the Chukei prompt text, and every response it produces for end users — is written in **Japanese**, because its end users are Japanese-speaking GSI (Geospatial Information Authority of Japan) staff and the whole point is a Japanese-language concierge experience. Chat with hfu (the maintainer) happens in Japanese regardless of which repo is open.

## What this project is

Chukei (ちゅうけい) is a Staff-role prompt, in the Staccato architecture (`UNopenGIS/staccato-spec`), purpose-built for one real deployment: Hokkaido Regional Survey Department (北海道地方測量部) staff asking for maps in plain Japanese through 源内 (Gennai), Japan's government-wide generative AI system (built on AWS's Generative AI Use Cases OSS, operated via the Digital Agency). Gennai can hold a saved system prompt and render Markdown, but has no live internet access — so, like `dwg7/spiccato`'s `GENNAI_PROMPT.md`, the entire usable catalog has to be embedded directly in the prompt text.

**The name**: 伊能忠敬 (Ino Tadataka), Japan's most famous cartographer/surveyor, paired against 源内 (Hiraga Gennai, the Edo-period polymath the AI system is named after). Reading 忠敬 with its on'yomi gives "ちゅうけい" (Chukei) — which is simultaneously a homophone-ish pun on 中継 ("relay"), exactly describing what the Staff role does: relay the user's plain-language question to the Cartographer. One name, two meanings, both accurate.

## Relationship to sibling repos

- **`dwg7/spiccato`** — the Cartographer implementation this deploys against (`https://dwg7.github.io/spiccato/`). Its `GENNAI_PROMPT.md` (built by `scripts/build-gennai-prompt.mjs`) is Chukei's direct ancestor and the base to fork from. A pinned snapshot of both lives in `reference/` in this repo (see below) so this repo doesn't need network access to spiccato just to get started — but treat spiccato's `main` branch as the source of truth for anything beyond what's already been forked in.
- **`hfu/layers-martin`** — the Library: Japan's GSI open geodata (`layers.txt`), converted into a Martin-compatible static catalog (currently ~1,873 layers, updated by a daily scheduled GitHub Action). This is the catalog Chukei's prompt embeds.
- **`UNopenGIS/staccato-spec`** — the architecture spec (User/Staff/Cartographer/Library, Map Intent format). Still an informal v0.1 draft by hfu, not an officially ratified UN/DWG7 standard — say so plainly if asked.
- **Origin**: this whole line of work grew out of a talk, "Staccato: how to make your enterprise AI agent a map maker," hfu gave at the UN Open GIS Initiative Featured Talk (2026-08-19) as a DWG7 (Smart Maps working group) member. That talk's closing slide named "a smarter staff" and "a bigger library" as future work — Chukei is the concrete execution of "a smarter staff," tested on real users for the first time.

## Reference material in this repo

`reference/` holds a pinned snapshot (fetched 2026-08-21) of spiccato's `GENNAI_PROMPT.md` and `build-gennai-prompt.mjs`, so you can read the exact prompt structure and generation mechanism without a network round-trip. Full detail on how to use them is in `HANDOVER.md`.

## Continuity files

- Reasoning and rationale for each decision → `DECISIONS.md` (ADR-lite format, append-only, matches the pattern that worked well in the `staccato_un_opengis` presentation project)
- "What's the state right now, what's next" → `HANDOVER.md` — **read this first in any new session**
