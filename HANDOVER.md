# Handover Notes

Read this first in any new session on this repo. Written in English per the language convention in `CLAUDE.md`. Rationale for each decision lives in `DECISIONS.md`.

## What's true as of 2026-08-21

- Repo `dwg7/chukei` created and cloned to `/Users/hfu/Downloads/chukei` (see D1 for the GitHub-account note — always operate as `hfu`, never `handygeospatial`).
- Nothing has shipped yet. This session's job was to set up the repo and write this handover package; the actual Chukei prompt has not been drafted.
- **Deadline**: hfu has a lightning talk proposed for the Hokkaido Regional Survey Department's internal study session (社内勉強会), titled roughly "地図をコパイロットや源内で出したい" ("I want to get maps out using Copilot or Gennai"), happening **about one week out from 2026-08-21** (so roughly late August 2026 — confirm the exact date with hfu). The plan is for that talk to double as the pilot's launch: staff hear about Chukei, then start using it and giving feedback.
- hfu has already confirmed **GENNAI_PROMPT.md runs successfully on real Gennai today**, and that Gennai's system-prompt character limit is more generous than the earlier design assumption (`build-gennai-prompt.mjs`'s own comments record an earlier, mistaken size-driven exclusion that was reverted once this was tested — see the D13/D15 references inside `reference/GENNAI_PROMPT.md.snapshot-2026-08-21.md`'s own header). Also confirmed: **Gennai renders Markdown**, so a Markdown hyperlink in a response will be clickable — no need to fall back to a raw pasted URL.

## The core design decision: what Chukei changes vs. GENNAI_PROMPT.md

Read `reference/GENNAI_PROMPT.md.snapshot-2026-08-21.md` in full before writing anything — it is already very close to what Chukei needs. It already:
- Frames the AI as a "concierge," not a debugging assistant — it explicitly forbids narrating its own good behavior ("I didn't fabricate an ID" is banned as noise).
- Has a firm anti-fabrication rule for `source_id`/`style_id` with a documented real incident (`lcmfc2` vs. fabricated `lcmfc2_1`).
- Has an explicit, humane "not found" behavior: state the fact plainly, offer a best-effort alternative, don't narrate the refusal.
- Builds a single-line `https://dwg7.github.io/spiccato/#q=...` link (or, for whole published styles that can't be expressed as `#q=`, a Map Intent YAML block) and — this is the one thing to change — currently also **adds a one-line human description of what the link shows**.

**What hfu wants Chukei to do differently**: collapse the final response down to exactly one very short line, e.g. `地図を用意しました。[地図](<link>)。ちゅうけい2026-09-02` — i.e. drop the one-line description GENNAI_PROMPT.md currently adds, and append a fixed version tag. So the prompt-authoring task is narrow: fork `GENNAI_PROMPT.md`, keep essentially everything (catalog embedding, anti-fabrication rules, bbox-guessing policy, the two-catalog structure), and **replace only the final-response-format instruction** with the terser Chukei format below. Don't over-engineer this into a rewrite — it's a small, surgical change to an already-good prompt.

### The version tag is a build-time constant, not something Gennai computes

`build-gennai-prompt.mjs`'s own doc comment notes it deliberately does *not* embed a generation timestamp in `GENNAI_PROMPT.md`, to avoid diff noise. Chukei needs the opposite: the version tag (`ちゅうけい2026-09-02`) is the whole point — it's what lets hfu correlate a piece of feedback back to the exact prompt revision that produced it. So:
- The version string must be a **literal, hardcoded string baked into the prompt text at build/publish time** (a constant in the build script, bumped by hand or by a release script each time the prompt is revised and re-deployed to Gennai).
- It is **not** something the AI is asked to compute at response time — the base prompt already warns the model not to trust its own sense of the current date (`provenance.generated_at`... "現在日時を確信できない場合は省略してよい"). Never ask Gennai to generate today's date itself for this tag.
- Suggest a `YYYYMMDD` or `YYYY-MM-DD` date plus an optional single-letter suffix for same-day revisions during active iteration (`ちゅうけい2026-09-02a`, `...02b`) — see D4.

### The "not found" case needs its own terse Chukei-format wording

GENNAI_PROMPT.md's existing not-found guidance is good in substance but is written for the fuller response style. Chukei needs an equally terse not-found response that (a) still carries the version tag (so a failed query is still traceable in feedback), (b) states plainly that nothing matched, (c) invites a more specific question, (d) does not explain the model's internal anti-fabrication reasoning. Draft this alongside the success-path format — don't leave it as an afterthought, a bad first experience during the pilot week will cost more trust than a slow rollout would.

## The feedback loop

hfu wants a Microsoft Forms channel where staff report their question, Chukei's response, and their impression, so the two of you can iterate on the prompt from real usage. Two concrete improvements agreed on during design review, worth building in from day one rather than retrofitting later:

1. **Ask staff to paste the Chukei-generated link itself, not retype their question.** The link already losslessly encodes the resolved Map Intent (catalog, layers, bbox) — pasting it is one click, versus retyping a question is real friction for busy staff. Free-text "what did you actually want, and did this match?" stays as a secondary field for cases where the link alone doesn't explain the mismatch.
2. **Add one structured field** (e.g. a single "Did this match what you expected? — yes / no / partially" multiple-choice question) alongside the free-text impression field, so revisions can be tracked quantitatively over time rather than only qualitatively.

Also worth deciding before the form goes out (open questions for hfu, not yet decided):
- Anonymous vs. attributed feedback — attribution helps follow-up clarification, anonymity may get more candid criticism.
- A one-line expectation-setting note somewhere in the launch (lightning talk slide, or Chukei's own first-run response) that this is a pilot and odd results should be reported, not silently worked around.

## Catalog freshness

`hfu/layers-martin`'s catalog updates on a daily scheduled GitHub Action and currently holds ~1,873 layers (see `dwg7/spiccato` research notes in the sibling `staccato` project if more historical detail is needed — not duplicated here). Chukei's prompt embeds a catalog snapshot the same way `GENNAI_PROMPT.md` does, so it will drift stale the same way spiccato's would without a rebuild step. **Recommendation (not yet built): fork `build-gennai-prompt.mjs` into `scripts/build-chukei-prompt.mjs`, reusing its fetch/format logic wholesale**, and either (a) run it manually before each Gennai redeploy — matches how often hfu will actually be revising the prompt during active pilot iteration — or (b) add a scheduled GitHub Action that opens a PR (not a silent direct commit) when the catalog changes materially, so a human reviews before redeploying to Gennai (redeploying to Gennai is a manual, out-of-band step regardless — unlike spiccato, there's no CI/CD path directly into Gennai's saved-prompt slot). Start with (a); consider (b) once the pilot is past its first iteration cycle.

## What's actually left to do

1. Draft `CHUKEI_PROMPT.md` (or a build script + generated output, mirroring spiccato) — fork of `GENNAI_PROMPT.md` with the response-format section replaced per above. **Not started yet.**
2. Write `scripts/build-chukei-prompt.mjs` (fork of `build-gennai-prompt.mjs`) so the catalog embed isn't a one-time manual copy.
3. Test the drafted prompt against real Gennai before the lightning talk.
4. Draft the Microsoft Forms question set (see feedback-loop section above for the two must-have design choices).
5. Decide the open feedback-loop questions (anonymity, expectation-setting copy).
6. Prepare the lightning talk itself — likely its own short deck; out of scope for this repo unless hfu wants it tracked here too.

## Things to carry over from the `staccato` project (won't be in this repo's own memory otherwise)

Claude's persistent memory is scoped per working directory (`/Users/hfu/.claude/projects/-Users-hfu-Downloads/memory/` belongs to the `staccato` session's cwd, not this one) — so nothing from that project transfers automatically to a session rooted here. Everything actually load-bearing for Chukei has been folded into this file and `DECISIONS.md` already; the rest (UN talk logistics, slide-deck editing history) is genuinely out of scope for this repo and deliberately left behind.
