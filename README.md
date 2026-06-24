# US Sanctions Zhejiang Monitoring Skill

Version: `v0.1.0`

This repository packages a reusable agent skill for U.S. sanctions and control-list monitoring focused on Chinese and Zhejiang-linked people and entities.

## What It Does

- Collects and normalizes records from OFAC SDN, BIS Entity List, DoD 1260H/CMC, NS-CMIC, FCC Covered List, State/ISN, and related official sources.
- Preserves each list's legal effect instead of merging all sources into one generic "sanctions" bucket.
- Detects Zhejiang-linked companies and people using official addresses, city/province clues, IDs, and corporate relationship evidence.
- Compares generated Excel/CSV datasets against Word or Excel reports.
- Produces traceable outputs with source URLs and raw official text.

## Compatibility

The bundle includes formats for:

- Codex
- Claude Code / Cloud Code-style `SKILL.md` agents
- Work Buddy-style Markdown/JSON import
- Generic Markdown prompt-based agents

See [INSTALL.md](INSTALL.md) for installation details.

## Core Principle

Do not treat every U.S. list as the same type of sanction:

- OFAC SDN: blocking sanctions and possible secondary sanctions.
- BIS Entity List: export-control licensing restrictions.
- DoD 1260H/CMC: Chinese military company identification and defense procurement restriction.
- NS-CMIC: securities/investment restriction.
- FCC Covered List: communications equipment procurement/funding restriction.
