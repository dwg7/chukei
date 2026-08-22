# Chukei (ちゅうけい)

A Staff-role prompt for 源内 (Gennai), Japan's government-wide generative AI system, purpose-built so Hokkaido Regional Survey Department staff can get a map by asking a plain-language question — no GIS training, no catalog to search.

Part of the [Staccato](https://github.com/UNopenGIS/staccato-spec) architecture (User / Staff / Cartographer / Library). Chukei is Staff; the Cartographer is [`dwg7/spiccato`](https://github.com/dwg7/spiccato); the Library is [`hfu/layers-martin`](https://github.com/hfu/layers-martin), a Martin-compatible catalog built from Japan's national geodata (国土地理院 / GSI).

**The name**: 伊能忠敬 (Ino Tadataka), Japan's best-known cartographer and surveyor, set against 源内 (the Edo-period polymath the AI system is named for). Read with its on'yomi, 忠敬 becomes "Chukei" — which doubles as a pun on 中継 ("relay"): exactly what the Staff role does, relaying a plain question through to a map.

## Status

Early setup. See `HANDOVER.md` for current status and next steps, `DECISIONS.md` for design rationale, `JUSTIFICATION.md` for why this project lives under `dwg7`.

## Language

Documentation and code in this repository are in English. The prompt itself, and everything it says to its users, is in Japanese — its users are Japanese-speaking GSI staff.

## License

[CC0 1.0 Universal](LICENSE), matching `dwg7/spiccato` and the other DWG7 repos.

## Related

- [`dwg7/spiccato`](https://github.com/dwg7/spiccato) — the Cartographer this deploys against, and the direct ancestor of Chukei's prompt (`GENNAI_PROMPT.md`)
- [`hfu/layers-martin`](https://github.com/hfu/layers-martin) — the Library / catalog
- [`UNopenGIS/staccato-spec`](https://github.com/UNopenGIS/staccato-spec) — the architecture spec (informal draft)

**Want to try this on Microsoft Copilot instead of 源内?** Chukei itself is Gennai-only for now (`DECISIONS.md` D15) — use [`hfu/layers-martin`'s `STAFF_PROMPT.md`](https://github.com/hfu/layers-martin/blob/main/STAFF_PROMPT.md) instead, the fetch-based sibling prompt this project forked its Gennai variant from.
