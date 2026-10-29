# Adina Reyter Holiday Gift Guide: Developer Handoff

Approved mock-ups and build materials for the Holiday Gift Guide (launch **Nov 16**) on Adina Reyter's Shopify store (Prestige 7.3.6, customized).

## What's in this folder

| Path | What it is |
|---|---|
| `BUILD-SPEC.md` | **Start here.** Section-by-section build plan: which Prestige section to use, settings, styles, copy, products, images and content setup. |
| `prototype/` | The approved mock-ups as standalone HTML. Open `landing-desktop.html` in a browser. Pages link to each other; the promo bar rotates, "+" adds to a demo bag count and the jump bar works. **Reference only, not production code.** |
| `assets/images/` | Full-size originals of every lifestyle and tile image, from Adina Reyter's own product photography (source URLs in the spec). |
| `assets/svg/` | Bow doodle, nav starburst and "+" icon as SVG files. |
| `theme-starter/` | Starter code for the few non-native pieces: `gift-guide.css`, plus the sections `gg-intro`, `gg-jump-bar` and `gg-anchor`, plus the bow and starburst snippets. Written against standard Prestige conventions and **not yet tested in their theme**. Check selectors against the real markup. |
| `CLAUDE.md` | Brief for building with Claude Code, if used. |

## Recommended workflow
1. **Work on a copy.** Duplicate the live theme in Shopify and work on the copy only; never edit the live theme.
2. **Pull it locally.** Run `shopify theme pull` on the copy into a git repo.
3. **Build.** Build the gift guide page template and the persona collection template per `BUILD-SPEC.md`, reusing Prestige sections wherever possible. Keep all custom code in new `gg-*` files and `gift-guide.css`, so Prestige updates don't overwrite it.
4. **Preview locally.** Run `shopify theme dev` and compare against the prototype.
5. **Share for review.** Push the copy back unpublished (`shopify theme push --unpublished`) and send the preview link for review.

## Notes
- **Fonts:** Domaine, Mundial and EB Garamond are already in the theme. The prototype shows free stand-ins (Newsreader and Mulish) unless those fonts are installed locally, so match font names from the spec, not from the prototype's rendering.
- **Placeholder product picks:** product picks in the prototype are placeholders until the merch team confirms final SKUs.
- **Joy of Collecting is out of scope:** the Dec 8 Joy of Collecting campaign (tiered discount and free gift with purchase) is separate. Nothing from it belongs on these pages.
