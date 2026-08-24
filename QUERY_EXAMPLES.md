# Realistic query examples

A dozen plain-language queries a Hokkaido Regional Survey Department (北海道地方測量部) staff member could plausibly type into Gennai, grounded in real Hokkaido geography, administration, and disaster history — not generic placeholder questions. Built for two purposes: (1) give the lightning talk and pilot launch more reality than the three formula-driven demo queries in `TALK_PREP.md` can carry alone, (2) serve as a dry-run test set — see "Dry-run results" below, where each query was run against `CHUKEI_PROMPT.md` the same way `TALK_PREP.md`'s demo queries were (playing Chukei's role manually, since real Gennai access is still blocked per `HANDOVER.md`).

Every `source_id`/`style_id` referenced below was grep-verified against the actual generated `CHUKEI_PROMPT.md`, not assumed.

## The 12 queries

1. **「厚真町の斜面崩壊の分布を確認したい」** — 2018年北海道胆振東部地震(厚真町で大規模な斜面崩壊)の実務を想定。防災対応部門からの典型的な依頼。
2. **「有珠山の火山土地条件図を見せて」** — 有珠山は2000年噴火の記憶が新しく、道内の火山防災で頻出する固有名詞。
3. **「十勝岳の火山災害情報がほしい」** — 十勝岳も活火山、道東側の担当者が扱う可能性。
4. **「北海道駒ヶ岳周辺の火山情報を教えて」** — 道南側の火山、渡島半島担当を想定。
5. **「樽前山の赤色立体地図を見たい」** — 苫小牧近郊、赤色立体地図という具体的な図法名を職員が知っている前提のクエリ。
6. **「石狩川流域の洪水浸水想定区域を知りたい」** — 道内最大の一級河川、防災部門の定番。
7. **「札幌市の人口集中地区(DID)を確認したい」** — 都市計画・統計系の依頼、測量部が受けそうな行政照会。
8. **「十勝・釧路沿岸の津波浸水想定を見たい」** — 千島海溝地震(北海道・三陸沖後発地震注意情報の対象)を想定した、道東太平洋岸への切実な関心。
9. **「北海道の活断層を確認したい」** — 全道スケールでの照会。都市圏活断層図の性質上、カバレッジが薄い可能性がある(下記「近い」ケース参照)。
10. **「厚真町周辺の被災前後の空中写真を比較したい」** — 「前後」比較を求めているが、このカタログに厚真の被災前画像は無い(下記「近い」ケース参照)。
11. **「江別市周辺の土地条件図がほしい」** — 札幌近郊だが整備済み平野の外れの可能性がある、カバレッジ制約の典型例(下記「近い」ケース参照)。
12. **「北海道の地籍調査の進捗状況を教えて」** — 地図レイヤーではなく行政統計そのものを聞いており、このカタログには無い。意図的な「見つからない」ケース。

## Dry-run results

Response format and version tag (`ちゅうけい2026-08-24a`) per `CHUKEI_PROMPT.md`'s "応答フォーマット" section, applied by hand exactly as the prompt specifies. **Updated 2026-08-24 twice**: first for GitHub issue #1 (`DECISIONS.md` D21) — every response became 3 paragraphs (map/not-found line, `[フィードバックする](https://forms.cloud.microsoft/r/X8VyNySW5s)`, version tag) instead of 1 line; then for GitHub issue #2 (`DECISIONS.md` D22) — the first paragraph now distinguishes a direct match (`[地図](<link>)を用意しました。`) from a best-effort substitute (`近い[地図](<link>)を用意しました。`). Three of this file's 12 cases (9, 10, 11) turn out to be exactly the "近い" scenario issue #2 describes — they were already flagged as coverage/best-effort risk cases back when this file was first written (D19), before "近い" existed as a way to signal that to the user. To keep this file readable, the full 3-paragraph block is shown once (case 1); every other case shows only the first (varying) paragraph, since the feedback-link and version-tag paragraphs are always identical.

**1. 厚真町の斜面崩壊 — 直接対応**(`req=20180906hokkaido_iburi_hokaichi`, `opt=20180906hokkaido_atsuma_digital`)
> [地図](https://dwg7.github.io/spiccato/#q=catalog=https://hfu.github.io/layers-martin/catalog.json&req=20180906hokkaido_iburi_hokaichi|斜面崩壊・堆積分布図&opt=20180906hokkaido_atsuma_digital|厚真町周辺&bbox=141.75,42.6,142.0,42.8&name=厚真町)を用意しました。
>
> [フィードバックする](https://forms.cloud.microsoft/r/X8VyNySW5s)。
>
> ちゅうけい2026-08-24a

「斜面崩壊・堆積分布図」という主題が要求とそのまま一致するので「地図」のまま(「近い」は付けない)。

**2. 有珠山の火山土地条件図 — 直接対応**(`rstyle=vlcm`, `ostyle=vbm` — stars-optgeoのスタイルを優先。D20参照)
> [地図](https://dwg7.github.io/spiccato/#q=catalog=https://stars.optgeo.org/catalog&type=martin&rstyle=vlcm|火山土地条件図&ostyle=vbm|火山基本図&bbox=140.65,42.42,141.0,42.65&name=有珠山)を用意しました。(以下、フィードバックリンクとバージョンタグは省略 — ケース1と同一)

**3. 十勝岳 — 直接対応**(`req=vlcd_tokachi` — 道南〜道央の範囲外なのでlayers-martinのままでよい)
> [地図](https://dwg7.github.io/spiccato/#q=catalog=https://hfu.github.io/layers-martin/catalog.json&req=vlcd_tokachi|十勝岳&bbox=142.5,43.3,142.9,43.55&name=十勝岳)を用意しました。(以下省略)

**4. 北海道駒ヶ岳 — 直接対応**(`rstyle=vlcm`, `ostyle=vbm` — 渡島半島(道南)なのでstars-optgeoのスタイルを優先。D20参照)
> [地図](https://dwg7.github.io/spiccato/#q=catalog=https://stars.optgeo.org/catalog&type=martin&rstyle=vlcm|火山土地条件図&ostyle=vbm|火山基本図&bbox=140.5,41.95,140.85,42.15&name=北海道駒ヶ岳)を用意しました。(以下省略)

**5. 樽前山赤色立体地図 — 直接対応**(`req=tarumaered`)
> [地図](https://dwg7.github.io/spiccato/#q=catalog=https://hfu.github.io/layers-martin/catalog.json&req=tarumaered|赤色立体地図（樽前山周辺）&bbox=141.2,42.55,141.55,42.8&name=樽前山)を用意しました。(以下省略)

**6. 石狩川流域の洪水浸水想定 — 直接対応**(`req=01_flood_l2_shinsuishin_data`, `opt=01_flood_l1_shinsuishin_newlegend_data`)
> [地図](https://dwg7.github.io/spiccato/#q=catalog=https://hfu.github.io/layers-martin/catalog.json&req=01_flood_l2_shinsuishin_data|洪水浸水想定区域（想定最大規模）&opt=01_flood_l1_shinsuishin_newlegend_data|洪水浸水想定区域（計画規模（現在の凡例））&bbox=141.25,43.0,141.85,43.4&name=石狩川下流域)を用意しました。(以下省略)

**7. 札幌市のDID — 直接対応**(`req=did2020`, `opt=did2015`)
> [地図](https://dwg7.github.io/spiccato/#q=catalog=https://hfu.github.io/layers-martin/catalog.json&req=did2020|人口集中地区 令和2年（総務省統計局）&opt=did2015|人口集中地区 平成27年（総務省統計局）&bbox=141.15,42.95,141.55,43.25&name=札幌市)を用意しました。(以下省略)

**8. 十勝・釧路沿岸の津波浸水想定 — 直接対応**(`req=04_tsunami_newlegend_data`)
> [地図](https://dwg7.github.io/spiccato/#q=catalog=https://hfu.github.io/layers-martin/catalog.json&req=04_tsunami_newlegend_data|津波浸水想定（想定最大規模）&bbox=143.0,42.0,145.5,43.2&name=十勝・釧路沿岸)を用意しました。(以下省略)

**9. 北海道の活断層 — 「近い」ケース(issue #2 適用)**(`req=afm`)
> 近い[地図](https://dwg7.github.io/spiccato/#q=catalog=https://hfu.github.io/layers-martin/catalog.json&req=afm|活断層図（都市圏活断層図）&bbox=139.0,41.3,148.9,45.7&name=北海道全域)を用意しました。(以下省略)
>
> **注記**: `afm`(都市圏活断層図)は主要都市圏を対象とした図で、北海道全域を均等にカバーしているとは限らない — issue #2の「対象地域がレイヤーのカバレッジに含まれるか確信が持てない」に該当するので「近い」を付ける。D19時点ではこのカバレッジの薄さを応答文で説明できず(1行圧縮の制約上)利用者に伝わらなかったが、今は「近い」の一言でこの不確かさが伝わる — issue #2はまさにこのケースのために作られた。

**10. 厚真町の被災前後比較 — 「近い」ケース(issue #2 適用)**(`req=20180906hokkaido_atsuma_0906do,20180906hokkaido_atsuma_0911do`)
> 近い[地図](https://dwg7.github.io/spiccato/#q=catalog=https://hfu.github.io/layers-martin/catalog.json&req=20180906hokkaido_atsuma_0906do|厚真川地区（9/6撮影）,20180906hokkaido_atsuma_0911do|厚真川地区（9/11撮影）&bbox=141.75,42.6,142.0,42.8&name=厚真町)を用意しました。(以下省略)
>
> **注記**: このカタログには厚真町の被災「前」の基準画像が見当たらず、9/6・9/11撮影(いずれも震災後)の2時期を返すのが精一杯 — issue #2の「要求された対象の一部にしか対応できない」に該当するので「近い」を付ける。判断理由(前画像が無いこと)は応答に書かない。詳しい経緯を知りたければフィードバックフォームの自由記入欄で拾える。

**11. 江別市周辺の土地条件図 — 「近い」ケース(issue #2 適用)**(`req=lcm25k_2012`)
> 近い[地図](https://dwg7.github.io/spiccato/#q=catalog=https://hfu.github.io/layers-martin/catalog.json&req=lcm25k_2012|数値地図25000（土地条件）&bbox=141.4,43.05,141.65,43.2&name=江別市)を用意しました。(以下省略)
>
> **注記**: `lcm25k_2012`は「整備済み平野の一部」限定 — ケース9と同じく「対象地域がレイヤーのカバレッジに含まれるか確信が持てない」に該当するので「近い」を付ける。

**12. 北海道の地籍調査の進捗状況 — 意図した「見つからない」ケース**
> 該当する地図データが見つかりませんでした。もう少し具体的に教えていただけますか。
>
> [フィードバックする](https://forms.cloud.microsoft/r/X8VyNySW5s)。
>
> ちゅうけい2026-08-24a
>
> 地籍調査の進捗率は行政統計であって地図レイヤーではないため、このカタログはそもそも扱っていない。ベストエフォートの代替も構成できないので「近い」ではなく従来通りの見つからない応答になる。terseな not-found 応答がそのまま機能する、想定通りの結果。not-foundでもフィードバックリンクは省略されない(D21) — 「見つからなかった」という報告こそ拾う価値がある。

## Findings worth carrying forward

- **9件の成功ケースは全てフォーマット・ID実在性に問題なし**。
- **解決済み(D20)**: ケース2(有珠山)で発見した、カタログをまたぐ同名/類似候補の優先順位が未文書化だった問題。hfuの指示で「火山土地条件図/火山基本図は、個別火山名で聞かれた場合でもstars-optgeoのスタイル(`vlcm`/`vbm`)を優先する」という明確なルールを`CHUKEI_PROMPT.md`に追加した。対象の火山が道南〜道央の範囲外(ケース3の十勝岳など)の場合のみ、layers-martinの`vlcd_<火山名>`にフォールバックする。ケース2・4を上記の通り更新済み。
- **解決済み(D22、issue #2)**: D19時点で「バグではないが、応答文からは分からないカバレッジ・ベストエフォートのリスク」として意図的に含めていたケース9・10・11は、いずれも issue #2 が定義する「近い」の典型例そのものだった。今は該当ケースで応答に「近い」が付くようになり、応答文だけを見ても直接対応かベストエフォートかが利用者に伝わる。設計時に意図的に残しておいた「既知の制約」ケースが、後続issueの受け入れ基準を検証する具体例としてそのまま機能した形。
- **ケース10のベストエフォート代替は設計通り機能する**が、判断理由(前画像が無いこと)自体は応答文に書かない設計のまま — 「近い」はあくまで「直接対応ではない」という事実だけを伝える一言で、理由までは説明しない。理由を知りたければフィードバックフォームの自由記入欄で拾う、という役割分担は変わらない(`FEEDBACK_FORM.md`のフィールド3)。
