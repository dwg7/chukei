# Feedback form (Microsoft Forms)

Question set for the Microsoft Forms channel referenced in `HANDOVER.md`, so pilot feedback from Hokkaido Regional Survey Department staff can be collected consistently and correlated back to a specific `CHUKEI_PROMPT.md` revision via its version tag. Not yet created in Microsoft Forms — this is the spec to build it from.

**Decided** (2026-08-22, hfu): anonymous only, no name/section field. The pilot-expectation-setting note ("this is a pilot, please report odd results") lives on the lightning talk's slide, not inside the form itself — keep the form purely functional.

## Fields

**1. Chukeiの回答を、そのまま貼り付けてください**
Type: Text, long answer. Required.
Placeholder/help text: 「地図を用意しました。[地図](...)。ちゅうけい2026-08-22」のような回答全体をコピーして貼り付けてください。リンクが無い「見つかりませんでした」という回答だった場合も、その文章をそのまま貼り付けてください。

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

Link goes out via the lightning talk (the slide carries the pilot/report-odd-results framing per the decision above), then presumably stays available afterward for ongoing pilot feedback — confirm with hfu whether it should also be pinned somewhere longer-lived (e.g. alongside wherever the Gennai saved-prompt link/instructions are shared with staff) once the talk has happened.
