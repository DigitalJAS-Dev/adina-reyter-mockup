# Brief for Claude Code: Adina Reyter Holiday Gift Guide

You are working in a local copy of Adina Reyter's Shopify theme: Prestige 7.3.6 by Maestrooo, heavily customized.

## Goal
Build the Holiday Gift Guide landing page and the persona collection page to match the approved mock-ups.
- **Source of truth for structure, copy and styling:** `BUILD-SPEC.md`.
- **Visual reference:** the HTML in `prototype/`. Treat it as reference only and do not copy its markup into the theme.

## Rules
- **Reuse before you build.** Before writing anything new, inspect `sections/`, `snippets/` and `config/settings_schema.json`, and use Prestige's existing sections and settings wherever they can achieve the design: Announcement bar, Header, Collection list, Featured collection, Image with text, Rich text, main collection.
- **Keep custom code separate.** Put all custom code in new files only:
  - `sections/gg-*.liquid` and `snippets/gg-*.liquid`
  - `assets/gift-guide.css`
  - `templates/page.gift-guide.json` and `templates/collection.gift-guide.json`

  Do not edit Prestige core files unless unavoidable. If a core edit is needed, keep it minimal, comment it, and list it in a summary.
- **Start from the starter code.** Begin with `theme-starter/` and adapt its selectors and markup to the real theme. Its CSS class names for Prestige internals are guesses.
- **Fonts:** use only the fonts the theme already loads (Domaine, Mundial, EB Garamond). Do not add Newsreader or Mulish; they are prototype stand-ins only.
- **No discounts:** no discount or gift-with-purchase messaging. That belongs to a different campaign.
- **Keep accessibility:** alt text on all images, a visible focus state on links, and the theme's existing announcement bar controls.
- **Content lives in the admin:** products, collections and images are set up in Shopify admin. Reference collections by handle in template JSON using the handles in the spec, and flag anything that needs to be created.

## Workflow
1. **Plan first.** Read `BUILD-SPEC.md`, then explore the theme. Report back with a plan before editing:
   - which spec item maps to which existing section or setting
   - what needs custom code
   - any core files you would need to touch
2. **Build.** Build the landing template, then the collection template.
3. **Check.** Preview with `shopify theme dev` and compare against `prototype/landing-desktop.html`, `collection-desktop.html` and the mobile files at 390px wide. Check alignment: on the desktop landing page, the top tile row, the product rows and the banner center seam share edges.
4. **Summarize.** List every file created or changed, every setting to configure in the theme editor, and any open questions.
