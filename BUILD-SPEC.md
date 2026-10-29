# Adina Reyter Holiday Gift Guide: Build Spec

**Launch:** Nov 16 (runs to Dec 25)  
**Theme:** Prestige 7.3.6 (Maestrooo), heavily customized copy (`AR [Fall Launch 2] …`). Confirm all section names and settings below against the actual theme files before building.  
**Reference:** open the files in `prototype/` in a browser. They are the approved mock-ups, not production code.

> Scope note: The Joy of Collecting (Dec 8–13) is a separate campaign. The tiered discount (15% off 2, 20% off 3+) and the free gift with purchase are **not** part of the gift guide and should not appear on these pages.

---

## 1. Design tokens

### Colours

| Token | Hex | Use |
|---|---|---|
| Ink | `#1C1B19` | Body text, nav, icons, CTA links |
| Headline | `#000000` | Main intro headline (matches their `.collection-title`) |
| Body secondary | `#3D3A35` | Banner story text |
| Muted | `#6B655D` | Eyebrows, prices, inactive jump-bar links |
| Panel | `#F8F6F5` | Banner story panels, promo bar background (their `--background`) |
| Product image ground | `#F3F0EB` | Baked into product photos (no change needed) |
| Hairline | `#E0D8CB` / `#E8E1D6` | Jump bar underline, header border |
| Gift Guide nav label | `#7A5B2A` | "Gift Guide" link text |
| Starburst | `#A27C3F` stroke, `#C9A96E` centre | Nav icon |
| Bow fill | `#BED0DD` | Signature packaging blue, offset fill behind the bow line art |

### Type (all fonts already loaded in the theme)

| Element | Font | Size (desktop / mobile) | Notes |
|---|---|---|---|
| Intro headline | Domaine, 400 | 32px / 26px | Sentence case, letter-spacing 0.48px, `#000`. Same as their `.collection-title` |
| Overline ("Adina's Gift Guide") | Domaine | 14px / 12px | Uppercase, letter-spacing 3px / 2.5px, muted |
| Banner title ("For the Stacker") | Domaine | 56px / 38px | |
| Banner eyebrow ("Gift edit 01") | Domaine | 13px / 12px | Uppercase, letter-spacing 3px |
| Banner story | Mundial | 18px / 15px | `#3D3A35` |
| Section heading ("Best sellers") | Mundial 500 | 28px / 20px | Uppercase, letter-spacing 5px / 3px (their "Our most wanted" style) |
| Top tile labels | Mundial | 14px / 12px | Each word capitalized (`text-transform: capitalize`), letter-spacing 0.04em |
| Jump bar label ("Shop gifts") | Domaine | 28px / 20px | |
| Jump bar links | Mundial | 13px / 11px | Uppercase, letter-spacing 0.18em |
| Product name / price | Domaine / Mundial | 15px / 14px | Existing product card |
| "Gift Guide" nav label | EB Garamond italic | 18px | Mixed case, no uppercase transform |
| CTA links | Mundial 600 | 13px | Use their existing `.link` style (uppercase, underline that wipes on hover) |

### Layout
- Content max-width **1360px**, side padding **40px** desktop / **20px** mobile.
- Desktop landing page sections share one grid and line up top to bottom, with **20px** gutters:
  - **Top tile row:** 6 equal columns.
  - **Product rows:** 4 equal columns.
  - **Split banners:** two flush 50/50 halves, no gap between story and image.
  - **Alignment:** outer edges and the centre line match across all three.
- Mobile: 2-column product grids. Banners stack (image on top, story below). The top tile row becomes a horizontal swipe row.

---

## 2. Landing page (new page template, e.g. `page.gift-guide`)

Sections in order. **Effort:** **Native** = theme editor settings only · **CSS** = needs styling in `gift-guide.css` · **Custom** = new section or snippet (starter code in `theme-starter/`).

| # | Section | Prestige section (verify) | Effort |
|---|---|---|---|
| 1 | Announcement bar | Announcement bar, autoplay 5s | Native |
| 2 | Header | Header | Native + CSS |
| 3 | Intro: bow, overline, headline | Rich text, or `gg-intro` starter | Native / Custom |
| 4 | Top tile row (6) | Collection list | Native + CSS |
| 5 | "Shop gifts" jump bar | `gg-jump-bar` starter | Custom |
| 6 | Best sellers | Featured collection | Native + CSS |
| 7–14 | 4 × (split banner + 4 products) | Image with text + Featured collection | Native + CSS |
| 15 | Footer | Existing | Native |

**1. Announcement bar.** Two rotating messages, no discount messaging:
- "The Holiday Gift Guide is here. Find their forever piece." Link to the gift guide.
- "Complimentary shipping on orders over $100"

**2. Header**
- **Logo:** centered on its own row, larger, with the nav centered underneath. Check whether Prestige's header layout setting supports "logo centered, menu below". If not, this is CSS.
- **Nav item:** add "Gift Guide" as the **first** menu item, linking to the gift guide page.
- **Nav styling:** EB Garamond italic, 18px, `#7A5B2A`, mixed case, with `assets/svg/nav-starburst.svg` (13px) to the left. Target it with CSS on the link's `href`; see `gift-guide.css`.

**3. Intro**, centered:
- `assets/svg/bow.svg` at about 70px wide desktop and 50px mobile.
- Overline: "Adina's Gift Guide".
- Headline: "'Tis the season to be charming".
- No subhead.

**4. Top tile row.** Collection List with 6 items, image ratio **4:5**, title below the image. Mobile: horizontal carousel.

| Order | Label | Links to | Image |
|---|---|---|---|
| 1 | Gift By Price | Gifts collection sorted low to high, e.g. `/collections/gifts?sort_by=price-ascending` | Product shot `tile-gift-by-price.jpg` |
| 2 | Best Sellers | Existing best sellers collection | Product shot `tile-best-sellers.jpg` |
| 3–6 | The Charm Collector, The Stacker, The Sentimentalist, The Sterling Devotee | Each persona's own collection page | Lifestyle images (see section 5) |

Product shots on the first two tiles keep them visually distinct from the four on-model persona tiles.

**5. "Shop gifts" jump bar** (Custom: `theme-starter/sections/gg-jump-bar.liquid`).
- **Contents:** label "Shop gifts", then links that scroll down this page: Best Sellers, The Charm Collector, The Stacker, The Sentimentalist, The Sterling Devotee.
- **States:** the active link is underlined in ink; the others are muted with no underline. Mobile: horizontal scroll.
- **Anchors:** each target section needs a stable anchor. Add a `gg-anchor` section, with an `id` setting, directly above each target.
- **Why it doesn't duplicate the tiles:** the top tiles link out to the separate collection pages; this bar moves within the landing page.

**6. Best sellers.** Featured collection with 4 products, from the existing best sellers collection.
- **Heading:** "BEST SELLERS" in their uppercase Mundial heading style.
- **CTA:** "Shop all best sellers" as a `.link`, right-aligned on the heading row.
- **Products:** `3-diamond-amigos-curve-posts, the-collector-necklace, groovy-diamond-initial-charm-necklace-on-rolo-chain, celestial-diamonds-wide-huggie-hoops`

**7–14. Gift edits.** For each persona, two sections:
- **a. Image with text**
  - Story panel and image 50/50, flush with no gap. Image side alternates (story left on edits 1 and 3, right on 2 and 4).
  - Panel background `#F8F6F5`; content vertically centered, padding about 56px.
  - Content: eyebrow "Gift edit 0N", title, story, then the CTA link "Shop all 20 pieces" to the persona collection.
- **b. Featured collection:** 4 products from the persona collection, no heading.

| Edit | Title | Story | Image |
|---|---|---|---|
| 01 | For the Charm Collector | Start a strand she'll keep adding to: a chain now, a new charm or bead every year after. | `charm-collector.jpg` |
| 02 | For the Stacker | Huggies, cuffs and posts, made to be worn three at a time. | `stacker.jpg` |
| 03 | For the Sentimentalist | Initials, birthstones and hearts: pieces that stand for someone. | `sentimentalist.jpg` |
| 04 | For the Sterling Devotee | The same signature charms and chains, in sterling silver. | `sterling.jpg` |

Product picks used in the mock-up are placeholders until the merch team sends final SKUs:
- **For the Charm Collector** (landing preview, 4 products):
   - `the-collectors-charm-pack`, The Collector's Charm Pack ($3,998)
   - `the-everyday-chain-necklace`, The Everyday Chain Necklace ($1,794)
   - `groovy-solitaire-diamond-mini-charm`, Groovy Solitaire Diamond Mini Charm ($398)
   - `ivy-league-mini-bead-pack`, Ivy League Mini Bead Pack ($200)
- **For the Stacker** (landing preview, 4 products):
   - `celestial-diamonds-wide-huggie-hoops`, Celestial Diamonds Wide Huggie Hoops ($998)
   - `diamond-amigos-chain-posts`, Diamond Amigos Chain Posts ($898)
   - `pave-ear-cuff`, Pavé Ear Cuff ($498)
   - `wide-celestial-diamond-ear-cuff`, Wide Celestial Diamond Ear Cuff ($998)
- **For the Sentimentalist** (landing preview, 4 products):
   - `groovy-diamond-initial-charm-necklace-on-rolo-chain`, Groovy Diamond Initial Charm Necklace on Rolo Chain ($3,096)
   - `groovy-birthstone-mini-charm-collar-necklace`, Groovy Birthstone Mini Charm Collar Necklace ($1,696)
   - `sealed-with-love-diamond-and-gemstone-charm-necklace`, Sealed with Love Diamond and Gemstone Charm Necklace ($1,446)
   - `love-story-charm-bracelet`, Love Story Charm Bracelet ($4,792)
- **For the Sterling Devotee** (landing preview, 4 products):
   - `station-chain-necklace-in-sterling-silver`, Station Chain Necklace ($550)
   - `groovy-diamond-initial-charm-necklace-on-station-chain-in-sterling-silver`, Groovy Diamond Initial Charm Necklace on Station Chain ($848)
   - `baguette-horseshoe-signet-ring-in-sterling-silver`, Baguette Horseshoe Signet Ring in Sterling Silver ($498)
   - `groovy-pearl-diamond-cone-hinged-charm-in-sterling-silver`, Groovy Pearl + Diamond Cone Hinged Charm ($398)

---

## 3. Persona collection page (new collection template, e.g. `collection.gift-guide`)

Applied to all four persona collections. 20 products each, plus the gift card.

1. **Back link** "Back to the gift guide" at the top.
2. **Persona tabs:** The Charm Collector, The Stacker, The Sentimentalist, The Sterling Devotee.
   - Style: same text-link style as the jump bar; current page underlined.
   - Build: a menu plus a small snippet (Custom), or Prestige's collection navigation if available.
3. **Collection banner:** split story + image as on the landing page; eyebrow "Gift edit 01", title, story.
4. **Toolbar:** item count + sort.
5. **Product grid:**
   - Layout: 4 columns desktop, 2 mobile, existing product cards with the "+" quick add.
   - **Gift card:** the existing digital gift card product, added to each persona collection as normal. It appears as a regular product card, not a banner.
6. **Editorial block mid-grid** (after product 8 desktop / 12 mobile): image `editorial-collector.jpg` + "How a strand grows" + 2–3 lines from Adina + CTA link.
   - Check whether this Prestige version supports promotion or content blocks inside the collection grid. If not, it's Custom.
7. **"More gift edits":** collection list of the other three personas (image + Domaine title).

Charm Collector sample assortment used in the mock-up (20):
1. `the-collector-necklace`
2. `the-collectors-charm-pack`
3. `the-luck-charm-pack`
4. `the-love-charm-pack`
5. `the-everyday-chain-necklace`
6. `the-go-to-necklace`
7. `groovy-solitaire-diamond-mini-charm`
8. `groovy-geometric-diamond-heart-mini-charm`
9. `groovy-pearl-diamond-cone-hinged-charm`
10. `groovy-geometric-diamond-heart-hinged-charm`
11. `groovy-geometric-diamond-rectangle-big-bead`
12. `ivy-league-mini-bead-pack`
13. `velvet-crush-big-bead-pack`
14. `wrapped-in-cashmere-mini-bead-pack`
15. `french-kiss-diamond-rager-necklace`
16. `rugby-stripes-diamond-rager-necklace`
17. `spacer-mini-bead-pack`
18. `diamond-boot-mini-charm`
19. `station-chain-necklace`
20. `oval-charm-clip-new`

---

## 4. Components and behaviour

- **Quick add "+"**
  - Use Prestige's existing product-card quick add: a 44px light square at the bottom right of the image.
  - Desktop: fades in on hover, and the plus rotates 90° on hover. Mobile: always visible.
  - No change expected.
- **CTA links:** their existing `.link` class (uppercase Mundial 600, letter-spacing 0.18em, 1px underline that shrinks on hover). **No filled buttons** on these pages.
- **Bow and starburst:** inline SVGs from `assets/svg/`. Line art in `#1C1B19`; the bow's fill sits offset (+3px, +3px) behind the lines.
- **Accessibility**
  - All images need alt text; the suggested alt text is in the prototype HTML.
  - Jump links keep a visible focus state.
  - The rotating announcement bar keeps Prestige's pause/arrow controls.

---

## 5. Content to set up in Shopify admin

**Collections:**
- `gifts` (for Gift By Price)
- Best sellers (existing)
- `gift-guide-charm-collector`, `gift-guide-stacker`, `gift-guide-sentimentalist`, `gift-guide-sterling-devotee`: 20 products each plus the digital gift card

**Navigation menus:**
- Main menu: add "Gift Guide" first.
- New menu `gift-guide-personas` with the 4 persona collections (for the tabs).

**Images:** upload to Files or set as collection images. Full-size originals are in `assets/images/`, all from Adina Reyter's own product imagery:

| File | Used for | Source product | Original URL |
|---|---|---|---|
| `charm-collector.jpg` | Banner: For the Charm Collector + tile | `station-chain-necklace` | https://cdn.shopify.com/s/files/1/1866/2257/files/Station-Chain-Necklace-Gold-Model.jpg |
| `stacker.jpg` | Banner: For the Stacker + tile | `premier-amigos-diamond-ear-cuff` | https://cdn.shopify.com/s/files/1/1866/2257/files/Premier-Amigos-Diamond-Ear-Cuff-Model.jpg |
| `sentimentalist.jpg` | Banner: For the Sentimentalist + tile | `the-icon-necklace` | https://cdn.shopify.com/s/files/1/1866/2257/files/AR_CORE_ECOM_LOOK_61_0008_Retouched.jpg |
| `sterling.jpg` | Banner: For the Sterling Devotee + tile | `station-chain-necklace-in-sterling-silver` | https://cdn.shopify.com/s/files/1/1866/2257/files/Station-Chain-Necklace-Silver-Model-2.jpg |
| `editorial-collector.jpg` | Collection page editorial block | `the-collector-necklace` | https://cdn.shopify.com/s/files/1/1866/2257/files/AR_CORE_ECOM_LOOK_70_0007_Retouched.jpg |
| `bracelets-friends.jpg` | Mobile landing full-bleed image | `choose-your-talisman-charm-bracelet-on-4mm-italian-chain` | https://cdn.shopify.com/s/files/1/1866/2257/files/Choose-Your-Talisman-Charm-Bracelet-on-4mm-Italian-Chain-Model.jpg |
| `tile-gift-by-price.jpg` | Top tile: Gift By Price (product shot) | `the-collectors-charm-pack` | https://cdn.shopify.com/s/files/1/1866/2257/files/The-Collectors-Charm-Pack_C.jpg |
| `tile-best-sellers.jpg` | Top tile: Best Sellers (product shot) | `the-collector-necklace` | https://cdn.shopify.com/s/files/1/1866/2257/files/The-Collectors-Necklace_Good-Luck-Diamond-Clover-Hinged-Charm-Diamond-Baguette-Big-Bead_C_be35f1f2-5ef3-4ce3-bdb2-536e9bd891bd.jpg |

---

## 6. Still to confirm with the client

- **Final products:** 20 SKUs per persona and the 4 to feature on the landing page.
- **Gift card:** minimum amount for the price shown on the card.
- **Editorial copy:** the "How a strand grows" text from Adina.
- **Shipping message:** confirm the $100 threshold.
- **Bow:** the current one is a placeholder doodle. An illustrator could redraw it in the brand hand.
- **Logo:** use the real logo file (the prototype uses typed text).
