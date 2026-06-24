---
name: us-sanctions-zhejiang-monitoring
description: Collect, normalize, and compare U.S. sanctions and control-list records for Chinese or Zhejiang-linked people and entities. Use for OFAC SDN, BIS Entity List, DoD 1260H/CMC, NS-CMIC, FCC Covered List, State/ISN, Zhejiang hit detection, sanctions-reason analysis, and report comparison.
---

# U.S. Sanctions Zhejiang Monitoring

Build traceable U.S. sanctions/control-list datasets for Chinese and Zhejiang-linked entities. Preserve list type and legal effect.

## Core List Distinctions

- OFAC SDN: blocking sanctions, asset freeze, transaction ban, possible secondary sanctions.
- BIS Entity List: export-control license restrictions, usually no asset freeze.
- DoD 1260H/CMC: Chinese military company identification plus defense procurement restriction, not OFAC-style blocking.
- NS-CMIC: securities/investment restriction.
- FCC Covered List: communications equipment procurement/funding restriction.
- State/ISN/DTC: list-specific restrictions; do not infer SDN consequences.

## Workflow

1. Lock scope: date range, sources, geography, Hong Kong/Macau/Taiwan inclusion, vessels/aircraft, and foreign linked-person rules.
2. Collect official sources first: OFAC Recent Actions/SDN, Federal Register/BIS, DoD 1260H, FCC, ITA CSL.
3. Normalize fields: date, source list, action type, record type, English name, Chinese name, address, tags, linked-to entity, IDs, source URL, raw official entry.
4. Detect Zhejiang links using Zhejiang, Hangzhou, Ningbo, Zhoushan, Wenzhou, Jinhua, Cixi, Yuyao, Yinzhou, USCC, address, and corporate relation evidence.
5. Classify reasons from official tags and press releases; mark inferred context as preliminary.
6. Compare reports by same-list scope first, then all-list scope. Output matched, report-only, and dataset-only.
7. Produce Excel/CSV/Markdown outputs with source URLs and raw official text.

## Pitfalls

- Do not call 1260H/CMC an SDN sanction.
- Check `Subject to Secondary Sanctions` per row.
- Do not drop foreign individuals linked to China/Hong Kong entities when in scope.
- Do not count vessels as companies unless requested.
- Keep official OFAC names and normalized PRC工商 names when they differ.
