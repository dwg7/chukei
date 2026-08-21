# Decisions Log

ADR-lite log for this project. English per `CLAUDE.md`'s language convention. Append new decisions at the top, oldest at the bottom, following the pattern that worked well in the sibling `staccato_un_opengis` presentation project.

---

### D8 — Pin a snapshot of spiccato's GENNAI_PROMPT.md and its build script in `reference/`
**Date**: 2026-08-21
**What**: Copied `dwg7/spiccato`'s `GENNAI_PROMPT.md` and `scripts/build-gennai-prompt.mjs` (as of that date) into this repo's `reference/` folder, suffixed `.snapshot-2026-08-21`.
**Why**: Chukei is a direct fork of this prompt and its generation mechanism. Pinning a snapshot means a fresh session can read the exact structure being forked from without a network round-trip to GitHub, while the filename makes clear it's a point-in-time copy, not a live sync — check spiccato's `main` branch if working on anything the snapshot might not cover.

### D7 — Reuse spiccato's catalog-embedding build script rather than hand-copying the catalog
**Date**: 2026-08-21
**What**: Plan to fork `scripts/build-gennai-prompt.mjs` into `scripts/build-chukei-prompt.mjs`, reusing its fetch/format/noise-filtering logic against the same `hfu/layers-martin` and `stars.optgeo.org` catalogs. Not yet implemented.
**Why**: `hfu/layers-martin` updates daily (~1,873 layers as of this writing). A hand-copied catalog snapshot would go stale the same way a manually-maintained one always does. Reusing the proven fetch/format logic avoids re-deriving it and keeps Chukei's catalog listing correct by construction.

### D6 — Chukei's prompt is a narrow fork of GENNAI_PROMPT.md, not a rewrite
**Date**: 2026-08-21
**What**: The only planned change to the inherited prompt content is the final-response-format instruction — collapse it from "build a link + add a one-line description of what it shows" down to a fixed terse format: `地図を用意しました。[地図](<link>)。ちゅうけい<version>`. Everything else (catalog embedding, anti-fabrication rules for `source_id`/`style_id`, the two-catalog structure, bbox-guessing policy, Cartographer-capability notes) is inherited unchanged.
**Why**: GENNAI_PROMPT.md already encodes a lot of hard-won design (see its own D13/D15-equivalent history around a mistaken size-driven catalog trim that was reverted after real testing, and the documented `lcmfc2`/`lcmfc2_1` fabrication incident). Re-deriving that from scratch would be wasted and risky. The only genuinely new requirement is the end-user response format for this specific, more non-technical pilot audience.

### D5 — Version tag is a literal build-time constant, never AI-computed
**Date**: 2026-08-21
**What**: The `ちゅうけい2026-09-02`-style tag appended to every response is a hardcoded string baked into the prompt at build/publish time (bumped manually or by a release step whenever the prompt is revised and redeployed to Gennai), with an optional same-day suffix (`...02a`, `...02b`) for rapid iteration days. Gennai is never asked to generate the date itself.
**Why**: Two reasons. First, the base prompt already tells the model not to trust its own sense of the current date for `provenance.generated_at` — the same caution applies here. Second, the entire purpose of the tag is to let a piece of user feedback be traced back to the exact prompt revision that produced it; that only works if the tag is fixed per-deploy, not computed per-response.

### D4 — Feedback form: paste the generated link, not the original question; add one structured field
**Date**: 2026-08-21
**What**: Design the Microsoft Forms feedback channel to primarily ask staff to paste the Chukei-generated spiccato link (which losslessly encodes the resolved Map Intent), rather than retype their original question. Add one structured multiple-choice field ("Did this match what you expected? — yes / no / partially") alongside a free-text impressions field.
**Why**: Retyping a question is real friction for busy staff and this pilot's success depends on actually getting feedback. The link is already the artifact that matters most for debugging a mismatch, and pasting it is near-zero-effort. A structured field makes it possible to track improvement over prompt revisions quantitatively, not just anecdotally.

### D3 — Language split: English docs/code, Japanese generated output
**Date**: 2026-08-21
**What**: All repo documentation, code, comments, commit messages, and this decisions log are written in English, matching `dwg7/spiccato`'s treatment as an international project. The Chukei prompt text itself, and every response it produces, is Japanese — its entire audience is Japanese-speaking GSI staff.
**Why**: hfu's explicit instruction. Keeps the `dwg7` org's documentation consistently readable internationally while keeping the actual product correctly localized for its real, single-language audience.

### D2 — Repo created public under `dwg7`, matching sibling repos
**Date**: 2026-08-21
**What**: `gh repo create dwg7/chukei --public`.
**Why**: Consistent with `dwg7/spiccato` and the DWG7 (Smart Maps) working group's stated vision of keeping this kind of work open. No sensitive data (no staff names, no actual survey content, no real feedback-form responses) is planned to live in this repo — only the prompt design and process documentation.

### D1 — Always operate as the `hfu` GitHub account, never `handygeospatial`
**Date**: 2026-08-21
**What**: Verified via `gh auth status` before creating the repo that only the `hfu` account was authenticated, and confirmed `hfu` is a member of the `dwg7` org before running `gh repo create`.
**Why**: hfu flagged that a past session mistakenly operated as `handygeospatial` instead of `hfu`. Recorded here as a standing check for any future repo/GitHub operation in this project: confirm `gh auth status` shows `hfu` as the active account first.
