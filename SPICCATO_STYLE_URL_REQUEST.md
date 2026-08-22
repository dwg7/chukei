# Prompt for the spiccato Claude Code session

Not a chukei-repo artifact — this is prep text for hfu to hand to the *separate* Claude Code session working in `dwg7/spiccato`, per hfu's request (2026-08-22). Delete or archive once that request has been delivered and resolved one way or the other; it doesn't need to stay in this repo long-term.

---

I maintain `dwg7/chukei`, a Staff-role prompt for spiccato that runs on 源内 (Gennai), a government AI system with no internet access and a saved-system-prompt-only interface. Chukei's audience is non-technical government staff (Hokkaido Regional Survey Department) typing plain-language questions — not GIS engineers.

Chukei's whole design promise is that every response collapses to one line: a short sentence plus a single clickable spiccato link (`地図を用意しました。[地図](<link>)。ちゅうけい<version>`). That works today for individual layers: spiccato's `#q=` URL scheme already lets it build

```
https://dwg7.github.io/spiccato/#q=catalog=<catalog uri>&type=<catalog_type>&req=<source_id1[|label1],source_id2[|label2],...>&opt=<...>&bbox=<west,south,east,north>&name=<name>
```

— `req`/`opt` reference individual `source_id`s from a Martin-compatible catalog, and this whole thing is one link, no paste step, nothing scary to hand a non-technical user.

The gap: spiccato also supports complete, pre-symbolized thematic maps referenced by `style_id` (e.g. Hokkaido's `vlcm`/`vbm` volcanic land-condition styles, from the `stars-optgeo` catalog, `type=martin`) via a Map Intent's `required_styles`/`optional_styles`. But as far as I can tell, there's no way to reference a `style_id` through the `#q=` URL scheme — the only path today is pasting a full Map Intent YAML block into spiccato's own form UI, e.g.:

```yaml
spec_version: "map-intent/v2"
goal: "北海道の火山土地条件図を示す。"
area: {name: "<地名>", bbox: [<west>, <south>, <east>, <north>]}
catalog_context:
  active_catalogs:
    - {id: "stars-optgeo", type: "martin", uri: "https://stars.optgeo.org/catalog"}
required_styles:
  - {style_id: "vlcm", label: "火山土地条件図"}
optional_styles:
  - {style_id: "vbm", label: "火山基本図"}
```

For spiccato's own documented audience (people who read `STAFF_PROMPT.md` and already understand Map Intent as a concept), pasting YAML into a form is a completely reasonable interaction. But for Chukei, it's the only case where the one-line-response promise breaks down — handing a non-technical user a raw YAML block and telling them to paste it somewhere is intimidating, not friendly, and undermines the whole point of the terse response format.

**The ask**: would it be straightforward to extend the `#q=` URL scheme so `required_styles`/`optional_styles` can also be expressed as URL parameters, analogous to how `req`/`opt` already express layer `source_id`s? Something like `rstyle=<style_id1[|label1],...>&ostyle=<style_id2[|label2],...>` (naming entirely up to whatever's most consistent with the existing scheme) that resolves into `required_styles`/`optional_styles` the same way `req=` resolves into `required_layers`.

If that's a small, additive change — a new optional URL param, with the YAML-paste path staying exactly as-is for anything more complex than "one or two required/optional styles plus a bbox" — that's exactly what I want, and it removes the YAML-dump problem for this specific, common case without touching anything else spiccato does.

If it turns out to be more involved than that (e.g. styles carry something layers don't — a style's own default viewport, symbology parameters that don't map cleanly onto a URL param, etc.), let me know why, and I'll take that back to Chukei and just have it stop using style_id-based responses entirely (fall back to only ever emitting `req`/`opt` against individual layers, dropping the vlcm/vbm pre-symbolized-style feature from Chukei's side rather than spiccato's).

Not asking for any change to the YAML-paste flow itself — that should stay exactly as it is.
