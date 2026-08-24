# Feedback form (Microsoft Forms)

**Live** (2026-08-24): https://forms.cloud.microsoft/r/X8VyNySW5s

Question set for the Microsoft Forms channel referenced in `HANDOVER.md`, so pilot feedback from Hokkaido Regional Survey Department staff can be collected consistently and correlated back to a specific `CHUKEI_PROMPT.md` revision via its version tag. hfu built the live form directly rather than from this file field-by-field. **Verified against the live form 2026-08-24** (this session, via browser) ahead of the internal release — it has drifted slightly from the original 3-field design below (field 2's wording differs, and a 4th optional field was added); this file has been updated to match what's actually live, which is the source of truth from here on.

**Decided** (2026-08-22, hfu): anonymous only, no name/section field. The pilot-expectation-setting note ("this is a pilot, please report odd results") lives on the lightning talk's slide, not inside the form itself — keep the form purely functional.

**Superseded** (2026-08-24, GitHub issue #1, `DECISIONS.md` D21): the original plan below assumed staff would reach this form some other way (a pinned link, the talk slide) and then paste Chukei's response into it. That's no longer the only path — the form's URL is now embedded as a `[フィードバックする](...)` link directly in *every* Chukei response (success or not-found), per `CHUKEI_PROMPT.md`'s "応答フォーマット" section, so reaching the form is one click from whatever Chukei just said. The "Distribution" section below is updated accordingly; the field design itself (paste-the-response as field 1) is unaffected and still the right design.

## Fields (as actually live, verified 2026-08-24)

**1. ちゅうけいが返した地図リンク（https://...）を貼り付けてください。**
Type: Text, long answer (Multi Line Text). **Required.**

In practice this ends up being "paste the whole response" in most cases anyway, since staff copy the message containing the link. Why the link/response and not just a retyped question: for a successful query the link alone losslessly encodes the resolved Map Intent (`DECISIONS.md` D4's original rationale) — pasting it is near-zero-effort compared to retyping what was asked.

**2. 表示された地図は期待にどの程度合っていましたか**
Type: Choice (Single choice). **Required.**
Options: ○期待どおり / △一部違う / ×違う

This is the structured field (`DECISIONS.md` D4) that lets revisions be tracked quantitatively across prompt versions. Note: live wording/options differ from this file's original draft (was "はい/いいえ/一部") — the live wording is what matters.

**3. 本当は何を見たかったですか。欲しかった情報や、期待との違いを自由に記入してください。**
Type: Text, long answer. Optional.

Secondary free-text field for cases where the pasted response alone doesn't explain a mismatch — particularly the "not found" case, where there's no link to infer intent from, and any case where "△一部違う"/"×違う" was selected above and the reason isn't obvious from the response text. Also the natural place to explain *why* a "近い" (best-effort) response missed the mark, since `CHUKEI_PROMPT.md` deliberately never puts that reasoning in the response itself (D22).

**4. 追加コメントとして、改善提案や気付いた点があれば記入してください。**
Type: Text, long answer. Optional. **Not in the original 3-field design** — added directly in Forms, presumably for general suggestions that don't fit "what did you actually want" (field 3).

No name, section, or contact field (anonymous-only, per the decision above) — the live form's own boilerplate ("it will not automatically collect your details like name and email address unless you provide it yourself") confirms this.

## Microsoft Forms setup notes

- Turn **off** "Record name" (org-tenant setting under Forms' response options) so responses aren't silently tied to a Microsoft 365 identity even though no name field exists on the form itself. (Consistent with the live form's own privacy notice, but that notice doesn't prove this setting is off — worth double-checking directly in Forms if it matters.)
- Response scope: "Only people in my organization can respond" is fine (keeps it to GSI staff) — this does not by itself record who responded, as long as "Record name" above is off.
- Leave "Shuffle question order" off — the fields build on each other (paste response → structured rating → free text → general comments) and shuffling would be confusing for no benefit.
- Do not enable "One response per person" — that setting requires sign-in and would conflict with the anonymous-only decision.

## Distribution

Primary path (as of D21): embedded directly in every Chukei response via `[フィードバックする](...)`, so no separate distribution step is needed for staff who are already using Chukei — the link is always one click away from whatever they just asked. The lightning talk slide still carries the pilot/report-odd-results framing (per the decision above) as the expectation-setting moment, but is no longer the only — or even the primary — way staff reach the form.
