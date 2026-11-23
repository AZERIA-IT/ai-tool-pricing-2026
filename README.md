# AI tool prices

Public list prices of AI creative tools, read on each vendor's own pricing page on the date shown. Promotional prices excluded.

- Tools: 51
- Priced plan rows: 183
- Checked on: 2026-11-22
- Source: https://twistavo.com/ai-tool-pricing
- Licence: CC BY 4.0 (see `LICENSE`)
- Attribution: "Twistavo (twistavo.com/ai-tool-pricing)"

## Files

- `data/plans.csv` and `data/plans.json`: one row per plan that has a price.
- `data/tools.csv`: one row per tool.

The data files are generated from the records behind twistavo.com/ai-tool-pricing by `scripts/seo/export-tool-pricing-dataset.mjs` in the Twistavo code base. No value is typed by hand.
- `LICENSE`: full text of CC BY 4.0.

## Columns: plans.csv and plans.json

| Column | Meaning |
|---|---|
| `tool` | Tool name, as on its page on twistavo.com |
| `tool_slug` | Slug used in the page URL |
| `category` | Category used on twistavo.com (for example `video`, `image`, `voice`) |
| `plan` | Plan name as listed on the vendor page |
| `price` | Price as listed, copied exactly (for example `$21`, `€11`, `$0`) |
| `period` | Billing text as listed (for example `per month, billed monthly`) |
| `alt_price` | Second price shown for the same plan, copied exactly. Empty when none (`null` in JSON) |
| `region_short` | Region and currency the page was served in (for example `France, USD`) |
| `checked_on` | Date the page was read (YYYY-MM-DD) |
| `source_url` | Vendor pricing page the price comes from |
| `page_url` | Tool page on twistavo.com |
| `kind` | `one-time` (paid once), `usage` (pay as you go, no recurring fee) or `recurring`, when the vendor page states it. Empty when not stated (`null` in JSON); such a plan is read as a regular plan |

## Columns: tools.csv

`tool`, `slug`, `category`, `checked_on`, `source_url` and `page_url` have the same meaning as above.

| Column | Meaning |
|---|---|
| `free_plan` | `yes` if the vendor page lists a free plan, else `no` |
| `cheapest_plan` | Lowest regular paid plan. Free plans, one-time and pay-as-you-go prices are not counted |
| `cheapest_price` | Price of that plan, copied from `plans.csv` |
| `cheapest_period` | Billing text of that plan, copied from `plans.csv` |
| `entry_plan` | One-time or pay-as-you-go option to start paying, copied from `plans.csv`. Empty when the tool has none |
| `entry_price` | Price of that option, copied from `plans.csv` |
| `entry_period` | Billing text of that option, copied from `plans.csv` |
| `entry_kind` | `one-time` or `usage`, from the `kind` column |
| `entry_cheaper` | `yes` if the one-time price is below the stated price of every regular paid plan in the same currency, else `no` |

Ranking rule for `cheapest_*`: paid plans come first. A plan priced above 0 that is not marked `one-time` or `usage` is ranked by its price a month: a price whose billing text says per month or monthly is compared as listed; a price whose billing text says per year, yearly or annual is divided by 12 for the comparison only. The divided value is not published. Ties go to the first plan listed. A plan whose billing text states neither is not ranked; when no paid plan is ranked, the first paid plan listed is used. A tool with no regular paid plan shows its $0 plan, or nothing when it has none. Amounts are not converted between currencies.

Rule for `entry_*`: a one-time purchase above 0 comes first (the cheapest, in the currency of the cheapest regular paid plan when there is one), else the first pay-as-you-go plan. A one-time price is called cheaper (`entry_cheaper` = `yes`) only when it is below the stated price of every regular paid plan in the same currency. A regular plan's first charge is never below its stated price, so no period or currency is converted to say so. Pay as you go is never called cheaper: a rate and a plan price differ in unit.

## Methodology

1. Each vendor pricing page is fetched with a plain curl request, logged out. Its visible text is saved.
2. Each value is copied from that saved text. Nothing is rounded or converted. The only calculations are the ranking rule for `cheapest_*` and the comparison for `entry_cheaper`.
3. Promotional, discounted, first-month and struck-through prices are left out. Where a page shows a regular price next to a promotion, the regular price is kept. A plan shown only with a promotion is left out.
4. A tool is included when its record has at least 3 FAQ entries and either 2 plans with a price above 0, or 1 free plan and 1 plan with a price above 0.
5. The `checked_on` date applies to every value in its row. Prices change. Check the vendor page before you rely on a number.

## Changes

### 2026-11-23

The files are now generated from the site's records instead of being copied by hand, so they follow the rules of twistavo.com/ai-tool-pricing.

- `plans.csv` and `plans.json`: new `kind` column (`one-time`, `usage`, `recurring` or empty), set on 18 rows where the vendor page states it.
- `plans.csv` and `plans.json`: new row for Remove.bg "Pay-as-you-go, 3 credits" (€3, one-time purchase), read on the same 2026-11-22 page. 182 rows become 183.
- `tools.csv`: new `entry_plan`, `entry_price`, `entry_period`, `entry_kind` and `entry_cheaper` columns, filled for the 9 tools with a one-time or pay-as-you-go option.
- `tools.csv`: Upscale.media `cheapest_*` was empty because its paid plan's billing text says "billed yearly" and not "per year". It now shows that plan, as the site does.
- No price, period or other existing value changed. Columns of the first release keep their order; new columns are added at the end.

## Licence

Creative Commons Attribution 4.0 International (CC BY 4.0). You may copy, share and adapt the data, including commercially. Give credit as "Twistavo (twistavo.com/ai-tool-pricing)", indicate the licence, and say if you changed the data. Full text: `LICENSE`.

## Notes

- Tools are third-party products. Their names, prices and terms belong to their vendors.
- Currency and region follow the page as read (`region_short`). Prices in other regions or currencies can differ.

## Tools

- [AIVA](https://twistavo.com/ai-tool-pricing/aiva) (music)
- [Akool](https://twistavo.com/ai-tool-pricing/akool) (avatar)
- [Animaker](https://twistavo.com/ai-tool-pricing/animaker) (video)
- [Captions](https://twistavo.com/ai-tool-pricing/captions) (editing)
- [Cartesia](https://twistavo.com/ai-tool-pricing/cartesia) (voice)
- [Civitai](https://twistavo.com/ai-tool-pricing/civitai) (image)
- [Cleanup.pictures](https://twistavo.com/ai-tool-pricing/cleanup-pictures) (editing)
- [Clipping Magic](https://twistavo.com/ai-tool-pricing/clipping-magic) (bgremoval)
- [Colossyan](https://twistavo.com/ai-tool-pricing/colossyan) (avatar)
- [Creatomate](https://twistavo.com/ai-tool-pricing/creatomate) (video)
- [DeepAI](https://twistavo.com/ai-tool-pricing/deepai) (image)
- [DeeVid AI](https://twistavo.com/ai-tool-pricing/deevid) (video)
- [Erase.bg](https://twistavo.com/ai-tool-pricing/erase-bg) (bgremoval)
- [Filmora](https://twistavo.com/ai-tool-pricing/filmora) (video)
- [Freepik](https://twistavo.com/ai-tool-pricing/freepik) (image)
- [Inworld AI](https://twistavo.com/ai-tool-pricing/inworld) (voice)
- [Kits.ai](https://twistavo.com/ai-tool-pricing/kits-ai) (voice)
- [LALAL.AI](https://twistavo.com/ai-tool-pricing/lalal-ai) (music)
- [LTX Studio](https://twistavo.com/ai-tool-pricing/ltx-studio) (video)
- [Lumen5](https://twistavo.com/ai-tool-pricing/lumen5) (video)
- [Mage.Space](https://twistavo.com/ai-tool-pricing/mage-space) (image)
- [Magic Hour](https://twistavo.com/ai-tool-pricing/magic-hour) (video)
- [MakeUGC](https://twistavo.com/ai-tool-pricing/makeugc) (avatar)
- [Munch](https://twistavo.com/ai-tool-pricing/munch) (video)
- [Neural Frames](https://twistavo.com/ai-tool-pricing/neural-frames) (video)
- [OpusClip](https://twistavo.com/ai-tool-pricing/opus-clip) (video)
- [Photoroom](https://twistavo.com/ai-tool-pricing/photoroom) (image)
- [PixAI](https://twistavo.com/ai-tool-pricing/pixai) (image)
- [Pixelbin](https://twistavo.com/ai-tool-pricing/pixelbin) (upscaling)
- [Pixelcut](https://twistavo.com/ai-tool-pricing/pixelcut) (bgremoval)
- [Pixlr](https://twistavo.com/ai-tool-pricing/pixlr) (image)
- [Playground AI](https://twistavo.com/ai-tool-pricing/playground) (image)
- [Polycam](https://twistavo.com/ai-tool-pricing/polycam) (3d)
- [Powtoon](https://twistavo.com/ai-tool-pricing/powtoon) (video)
- [Rask AI](https://twistavo.com/ai-tool-pricing/rask-ai) (dubbing)
- [Removal.AI](https://twistavo.com/ai-tool-pricing/removal-ai) (bgremoval)
- [Remove.bg](https://twistavo.com/ai-tool-pricing/remove-bg) (bgremoval)
- [Renderforest](https://twistavo.com/ai-tool-pricing/renderforest) (video)
- [Resemble AI](https://twistavo.com/ai-tool-pricing/resemble-ai) (voice)
- [Riverside](https://twistavo.com/ai-tool-pricing/riverside) (editing)
- [Scenario](https://twistavo.com/ai-tool-pricing/scenario) (image)
- [Sonix](https://twistavo.com/ai-tool-pricing/sonix) (editing)
- [Spline](https://twistavo.com/ai-tool-pricing/spline) (3d)
- [Steve AI](https://twistavo.com/ai-tool-pricing/steve-ai) (video)
- [Submagic](https://twistavo.com/ai-tool-pricing/submagic) (editing)
- [Suno](https://twistavo.com/ai-tool-pricing/suno) (music)
- [Tavus](https://twistavo.com/ai-tool-pricing/tavus) (avatar)
- [Topaz Labs](https://twistavo.com/ai-tool-pricing/topaz-labs) (upscaling)
- [TopView](https://twistavo.com/ai-tool-pricing/topview) (avatar)
- [Upscale.media](https://twistavo.com/ai-tool-pricing/upscale-media) (upscaling)
- [Voice.ai](https://twistavo.com/ai-tool-pricing/voice-ai) (voice)
