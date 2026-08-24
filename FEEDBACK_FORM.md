# Feedback form (Microsoft Forms)

**Live** (2026-08-24): https://forms.cloud.microsoft/r/X8VyNySW5s

Question set for the Microsoft Forms channel referenced in `HANDOVER.md`, so pilot feedback from Hokkaido Regional Survey Department staff can be collected consistently and correlated back to a specific `CHUKEI_PROMPT.md` revision via its version tag. hfu built the live form directly rather than from this file field-by-field — the sections below document the intended design and should be checked against the actual live form for drift if the two are ever suspected to disagree.

**Decided** (2026-08-22, hfu): anonymous only, no name/section field. The pilot-expectation-setting note ("this is a pilot, please report odd results") lives on the lightning talk's slide, not inside the form itself — keep the form purely functional.

**Superseded** (2026-08-24, GitHub issue #1, `DECISIONS.md` D21): the original plan below assumed staff would reach this form some other way (a pinned link, the talk slide) and then paste Chukei's response into it. That's no longer the only path — the form's URL is now embedded as a `[フィードバックする](...)` link directly in *every* Chukei response (success or not-found), per `CHUKEI_PROMPT.md`'s "応答フォーマット" section, so reaching the form is one click from whatever Chukei just said. The "Distribution" section below is updated accordingly; the field design itself (paste-the-response as field 1) is unaffected and still the right design.

## Fields

**1. Chukeiの回答を、そのまま貼り付けてください**
Type: Text, long answer. Required.
Placeholder/help text: 「[地図](...)を用意しました。(または「近い[地図](...)を用意しました。」) [フィードバックする](...)。ちゅうけい<version>」のような回答全体をコピーして貼り付けてください。リンクが無い「見つかりませんでした」という回答だった場合も、その文章をそのまま貼り付けてください。

Why the whole response and not just the link: for a successful query the link alone losslessly encodes the resolved Map Intent (`DECISIONS.md` D4's original rationale), but Chukei's terser format (D6/D9) also has a link-less "not found" response — pasting the full response text is the one field that works for both cases and still carries the version tag, so even a failed query stays traceable to the exact prompt revision that produced it.

**2. 期待どおりの地図でしたか?**
Type: Choice. Required. Single select.
Options: はい / いいえ / 一部

This is the one structured field (`DECISIONS.md` D4), letting revisions be tracked quantitatively across prompt versions rather than only read qualitatively from free text.

**3. 元々何を探していましたか?また、結果への感想があれば教えてください(任意)**
Type: Text, long answer. Optional.

Secondary free-text field for cases where the pasted response alone doesn't explain a mismatch — particularly the "not found" case, where there's no link to infer intent from, and any case where "partially" was selected above and the reason isn't obvious from the response text.

No other fields. No name, section, or contact field (anonymous-only, per the decision above) — keeping the form to three fields matters more than completeness, since busy staff are the audience and low friction is what makes the feedback loop actually work (D4).

## Microsoft Forms setup notes

- Turn **off** "Record name" (org-tenant setting under Forms' response options) so responses aren't silently tied to a Microsoft 365 identity even though no name field exists on the form itself.
- Response scope: "Only people in my organization can respond" is fine (keeps it to GSI staff) — this does not by itself record who responded, as long as "Record name" above is off.
- Leave "Shuffle question order" off — the three fields build on each other (paste response → structured yes/no/partial → free text) and shuffling would be confusing for no benefit.
- Do not enable "One response per person" — that setting requires sign-in and would conflict with the anonymous-only decision.

## Distribution

Primary path (as of D21): embedded directly in every Chukei response via `[フィードバックする](...)`, so no separate distribution step is needed for staff who are already using Chukei — the link is always one click away from whatever they just asked. The lightning talk slide still carries the pilot/report-odd-results framing (per the decision above) as the expectation-setting moment, but is no longer the only — or even the primary — way staff reach the form.
