# Lightning talk prep

Prep material for the Hokkaido Regional Survey Department internal study session (社内勉強会) lightning talk that doubles as Chukei's pilot launch. Format and tone per hfu's explicit direction (2026-08-22, see `HANDOVER.md` "Lightning talk direction"): **5 minutes of talk, 8 minutes of live demo**. Skip conceptual/architectural framing entirely — the message is "I built this, here's how to use it, give me feedback," not a design pitch. This file is the outline/script; the actual slide deck (if any) is out of scope for this repo unless hfu wants it built here too.

Structural headers below are in English per this repo's convention; the actual talk content is in Japanese, since that's literally what gets said to the audience.

## Talk outline (5 min)

Keep this lean — the instruction was explicitly to skip philosophical/architectural content, so resist the urge to explain Staccato, spiccato, or the Library here. If it's not needed to get to the demo, cut it.

1. **フック(30秒)** — 地図が欲しいとき、今どうしているか(GISソフトを開く、レイヤーを探す、担当者に頼む…)を一言。
2. **一言で言うと(30秒)** — 「源内に日本語で聞くと、地図のリンクが返ってくる」。これだけ言えば十分 — 仕組みの説明はしない。
3. **名前の由来(20秒、遊び心)** — 伊能忠敬(忠敬→ちゅうけい)と源内のダジャレ。軽く笑いを取る程度で十分、掘り下げない。
4. **大事なメッセージ(30秒)** — 「これはパイロット版です。**崩れます。遊んでください。** 変な結果が出たら、それも含めて教えてほしい」。ここが今日一番伝えたいこと。
5. **デモへ(残り時間)** — 「じゃあ実際にやってみます」で最小限の前置きだけ、すぐ画面へ。

Total: ~2分の内容だが、間や質疑の余地を見て5分に収まるよう現地で調整。

## Demo script (8 min)

Four short queries, each showing a different facet, plus one deliberate "break it" query to make the "遊んで良い" message concrete rather than just stated. Suggested pacing ~90 sec each; adjust live.

1. **普通のレイヤー検索**: 「札幌市の土砂災害警戒区域を教えて」→ リンクが返る → 開いてspiccatoで表示されるところを見せる。(元は`CHUKEI_PROMPT.md`「例」節1件目そのままの「土砂災害警戒区域を教えて」だったが、地名が無いとbboxが北海道全域規模の当てずっぽうになり結果が読みにくいため、地名を足した — ドライラン検証で判明、2026-08-22)
2. **複数レイヤー+ラベル**: 「石狩川の治水について考えたい」→ パネルに分かりやすい名前(治水地形分類図、洪水浸水想定区域)が出る様子を見せる。(同「例」節2件目)
3. **完成品スタイル**: 「北海道の火山土地条件図を見たい」→ リンクが返る(YAMLダンプではない — 経緯は`DECISIONS.md` D16/D17参照)。本番の`https://dwg7.github.io/spiccato/`で実リンクを開いて確認済み(2026-08-22): パネルに「火山土地条件図、火山基本図 を表示。」、必須の火山土地条件図がチェック済み・任意の火山基本図が未チェック、コンソールエラーなし。デモで安心して使ってよい。
4. **わざと壊す**: このカタログに存在しない/曖昧すぎる質問をぶつけて、「見つかりませんでした」の terse な応答を見せる。**ここが今日のデモの肝** — 失敗しても静かに、変な言い訳もせず終わる様子を見せることで、「壊しても大丈夫」を言葉でなく体験させる。
5. **(時間が余れば)フィードバックフォームへの導線**: 実際にChukeiの回答をコピーして`FEEDBACK_FORM.md`ベースのフォームに貼る様子を見せ、「これをやってください」で締める。

## Q&A prep

Distilled from `JUSTIFICATION.md` — full detail lives there if a question goes deeper than this. Keep answers short and honest; don't overclaim official status.

**Q: これは公式のDWG7の成果物ですか?**
A: 「DWG7メンバーが、DWG7の共有スペースで公開している実験です。DWG7として正式に採択されたものではありません — ただDWG7自体、トップダウンで承認して回るような組織ではなく、メンバーが公開の場で作って共有する、というのが元々の運営スタイルです」(`JUSTIFICATION.md`の締めの引用そのまま使ってよい)。

**Q: なぜ`dwg7`組織の下に置いているのですか?**
A: DWG7自身のミッション「地理空間分野の新技術を実運用でテストする」に直接合致していること、`spiccato`からの明確な派生であること、DWG7の憲章が「LLMユーザーやAIシステム自身」の参加を明示的に歓迎していること。

**Q: Copilot版もあるんですか?**
A: 「Copilot版が無いわけではないです。ただ、今のところ技術者向けのテイストのものになります — spiccato側の`STAFF_PROMPT.md`(カタログをその場で取得できる版)がそれです。今回、勉強会に向けてフレンドリーに作り込んだのは源内版(ちゅうけい)だけです。ちなみに源内版のプロンプト自体はただのテキストなので、Copilotに貼っても動くと思います — ただ今回はそちらのテストはしていません」。**避けたい言い方**: 「Copilot版はありません」(誤り — 技術者向けの選択肢は既にある)。

**Q: 地図データの出どころは? セキュリティ的に大丈夫?**
A: リンクの先は国土地理院ほかのオープンデータのみ(`hfu/layers-martin`)。源内自体が庁内限定のシステムなので、質問・利用は庁内に閉じている。

**Q: 間違った地図・変な結果が出たらどうすればいい?**
A: フィードバックフォームに、Chukeiの回答をそのまま貼って教えてほしい。これはパイロットで、そのために作った仕組み(`FEEDBACK_FORM.md`)。

## Resolved: style_id応答のYAMLダンプ問題(D16→D17→D18)

2026-08-22に発見、同日中に解消・本番確認済み。経緯は`DECISIONS.md` D16/D17/D18参照。spiccato側が`#q=`URL形式に`rstyle`/`ostyle`パラメータを追加(テスト110+13件パス)、push・GitHub Pages再デプロイ済み、本番URLで実リンクを開いて動作確認済み(このセッション自身のブラウザツールで直接検証)。`CHUKEI_PROMPT.md`/`scripts/build-chukei-prompt.mjs`は既に更新済み。デモクエリ3はブロッカー無し。
