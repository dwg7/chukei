# Chukei (ちゅうけい)

A Staff-role prompt for 源内 (Gennai), Japan's government-wide generative AI system, purpose-built so Hokkaido Regional Survey Department staff can get a map by asking a plain-language question — no GIS training, no catalog to search.

Part of the [Staccato](https://github.com/UNopenGIS/staccato-spec) architecture (User / Staff / Cartographer / Library). Chukei is Staff; the Cartographer is [`dwg7/spiccato`](https://github.com/dwg7/spiccato); the Library is [`hfu/layers-martin`](https://github.com/hfu/layers-martin), a Martin-compatible catalog built from Japan's national geodata (国土地理院 / GSI).

**The name**: 伊能忠敬 (Ino Tadataka), Japan's best-known cartographer and surveyor, set against 源内 (the Edo-period polymath the AI system is named for). Read with its on'yomi, 忠敬 becomes "Chukei" — which doubles as a pun on 中継 ("relay"): exactly what the Staff role does, relaying a plain question through to a map.

## Status

Early setup. See `HANDOVER.md` for current status and next steps, `DECISIONS.md` for design rationale.

## Language

Documentation and code in this repository are in English. The prompt itself, and everything it says to its users, is in Japanese — its users are Japanese-speaking GSI staff.

## Related

- [`dwg7/spiccato`](https://github.com/dwg7/spiccato) — the Cartographer this deploys against, and the direct ancestor of Chukei's prompt (`GENNAI_PROMPT.md`)
- [`hfu/layers-martin`](https://github.com/hfu/layers-martin) — the Library / catalog
- [`UNopenGIS/staccato-spec`](https://github.com/UNopenGIS/staccato-spec) — the architecture spec (informal draft)
