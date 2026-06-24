---
name: us-sanctions-zhejiang-monitoring
description: 适用于处理美国制裁与管制清单相关任务，尤其是 OFAC SDN、BIS Entity List、DoD 1260H/CMC、NS-CMIC、FCC Covered List、State/ISN 等清单的中国/香港主体匹配、浙江命中识别、制裁原因分析、清单口径区分、Excel/Word 差异比对，以及涉浙企业制裁监测会议或报告准备。
---

# U.S. Sanctions Zhejiang Monitoring

Use this skill to build a traceable, reviewable sanctions/control-list dataset for Chinese entities, then identify Zhejiang-linked people and companies and compare outputs against Word/Excel reports.

## Core Rule

Do not merge all U.S. lists into one undifferentiated “sanctions” bucket. Always preserve the list source and legal effect:

- **OFAC SDN**: blocking sanctions, asset freeze, U.S. persons transaction ban, possible secondary sanctions.
- **BIS Entity List**: export-control licensing restrictions, usually no asset freeze.
- **DoD 1260H/CMC**: Chinese military company identification and defense procurement restriction, not an OFAC asset-freeze list.
- **NS-CMIC**: securities/investment restriction.
- **FCC Covered List**: U.S. government communications equipment procurement/funding restriction.
- **State/ISN or DTC lists**: nonproliferation, defense trade, or related list-specific restrictions.

For details, read `references/us-list-taxonomy.md`.

## Standard Workflow

1. **Lock the scope**
   - Confirm date range, list sources, geography, and whether Hong Kong/Macau/Taiwan should be included.
   - State whether “China-related” means nationality/address only, or also foreign individuals linked to China/Hong Kong entities.
   - State whether vessels, aircraft, aliases, and list-change records are included.

2. **Collect official records first**
   - Start with official sources: OFAC Recent Actions/SDN details, Federal Register or BIS pages, DoD 1260H PDFs/pages, FCC Covered List, and ITA Consolidated Screening List where useful.
   - Keep source URLs per row. Do not rely only on media summaries for row-level facts.
   - When an official full data file lacks reliable list dates, use official recent-action pages or Federal Register dates for additions.

3. **Normalize records**
   - Keep fields for date, source list, action type, record type, official English name, Chinese name, address, programs/tags, linked-to entity, IDs, source URL, and raw official entry.
   - Preserve official spellings even when they differ from Chinese工商 common names.
   - Add a separate normalized/common-name field when the official Chinese rendering is awkward or wrong.

4. **Detect Zhejiang linkage**
   - Mark strong hits when official entries include Zhejiang, Hangzhou, Ningbo, Zhoushan, Wenzhou, Jinhua, Cixi, Yuyao, Yinzhou, or Zhejiang USCC/address evidence.
   - Mark “needs confirmation” when a Hong Kong/offshore entity has a Zhejiang address, Zhejiang branch, Zhejiang controller, or indirect link but no clear registration evidence.
   - For individuals, distinguish location/nationality from corporate linkage. A foreign individual linked to a Hong Kong/China entity should be captured only if the user’s scope includes “associated foreign persons.”

5. **Classify reasons**
   - Summarize reasons from official programs/tags and press releases:
     - `NPWMD` / `IFSR`: WMD nonproliferation / Iran financial sanctions.
     - `IRAN-CON-ARMS-EO`: Iran conventional arms procurement/supply.
     - `IRAN-EO13846` / `IRAN-EO13902`: Iran petroleum, petrochemical, shipping, trade, or related sectors.
     - `RUSSIA-EO14024`: Russia-related harmful foreign activities / defense-industrial support.
     - `SDGT`: counterterrorism.
   - Label inferred business context as “preliminary” unless the official source explicitly states it.

6. **Compare report vs dataset**
   - Compare by source-list口径 first, then by all-list口径.
   - Report three categories: matched, report-only, dataset-only.
   - For mismatches, identify whether the reason is true omission, different list type, date range mismatch, vessel/person exclusion, foreign-linked-person exclusion, or official/common-name spelling difference.

7. **Output reviewable artifacts**
   - Prefer an `.xlsx` workbook with sheets such as `摘要`, `浙江命中`, `全量记录`, `来源覆盖`, and `差异比对`.
   - Include row-level source links and raw official text.
   - In final summaries, clearly state coverage limitations and sources not yet fully integrated.

## Known Pitfalls

- Do not call DoD 1260H/CMC an OFAC-style sanction; describe it as Chinese military company identification plus defense procurement restriction.
- Do not treat “Subject to Secondary Sanctions” as universal. It appears on many OFAC entries but must be checked per row.
- Do not drop a foreign individual automatically if the task asks for people associated with China/Hong Kong entities.
- Do not count vessels as companies unless the user explicitly includes vessels.
- Do not treat an offshore/Hong Kong company with a Zhejiang address as a confirmed Zhejiang registered company without additional evidence.
- Do not equate the official OFAC Chinese display name with the PRC工商 registered name; keep both when they differ.

## Useful Official Sources

- OFAC Recent Actions: `https://ofac.treasury.gov/recent-actions`
- OFAC SDN Search: `https://sanctionslist.ofac.treas.gov/Home/SdnList`
- Federal Register API: `https://www.federalregister.gov/api/v1/documents.json`
- BIS Entity List page: `https://www.bis.doc.gov/index.php/policy-guidance/lists-of-parties-of-concern/entity-list`
- ITA Consolidated Screening List CSV: `https://data.trade.gov/downloadable_consolidated_screening_list/v1/consolidated.csv`
- DoD 1260H/CMC page: `https://www.defense.gov/pubs/cmc-list/`
- FCC Covered List: `https://www.fcc.gov/supplychain/covered-list`
