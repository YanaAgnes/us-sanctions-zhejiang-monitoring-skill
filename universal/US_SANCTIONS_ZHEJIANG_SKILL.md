# Skill: US Sanctions Zhejiang Monitoring

Version: `0.1.0`

Use this skill when asked to collect, normalize, compare, or explain U.S. sanctions/control-list records involving Chinese, Hong Kong, or Zhejiang-linked people and entities.

## Core Behavior

Preserve list type and legal effect. Do not merge OFAC SDN, BIS Entity List, DoD 1260H/CMC, NS-CMIC, FCC Covered List, and State/ISN/DTC records into one undifferentiated sanctions category.

## List Effects

- OFAC SDN: blocking sanctions, asset freeze, U.S. persons transaction ban, possible secondary sanctions.
- BIS Entity List: export-control licensing restrictions, usually no asset freeze.
- DoD 1260H/CMC: Chinese military company identification and defense procurement restriction; not an OFAC asset-freeze list.
- NS-CMIC: securities/investment restriction.
- FCC Covered List: U.S. government communications equipment procurement/funding restriction.
- State/ISN/DTC: list-specific nonproliferation, defense trade, or related restrictions.

## Workflow

1. Confirm date range, sources, geography, and inclusion/exclusion rules.
2. Use official sources first and keep source URLs per row.
3. Normalize date, source list, action type, entity/person type, English name, Chinese name, address, program tags, linked-to entity, IDs, raw official entry, and source URL.
4. Identify Zhejiang links from official addresses, province/city terms, USCC, and corporate relationship evidence.
5. Separate confirmed Zhejiang from needs-confirmation offshore/Hong Kong links.
6. Summarize reasons from official tags and press releases; mark inference as preliminary.
7. Compare reports and datasets by same-list scope first, then all-list scope.
8. Output traceable tables with matched, report-only, and dataset-only categories.

## Zhejiang Hit Terms

Use strong evidence terms such as `Zhejiang`, `Hangzhou`, `Ningbo`, `Zhoushan`, `Wenzhou`, `Jinhua`, `Cixi`, `Yuyao`, `Yinzhou`, and official PRC IDs or registration addresses. Treat offshore entities with Zhejiang addresses as needs-confirmation unless registration/control evidence is clear.

## Pitfalls

- Do not call DoD 1260H/CMC an OFAC-style sanction.
- Do not assume secondary sanctions for every OFAC row.
- Do not drop foreign individuals associated with China/Hong Kong entities when the scope includes linked persons.
- Do not count vessels as companies unless explicitly in scope.
- Preserve both official OFAC names and normalized PRC工商-style names when they differ.
