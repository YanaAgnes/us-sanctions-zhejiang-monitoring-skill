---
name: us-sanctions-zhejiang-monitoring
title: US Sanctions Zhejiang Monitoring
version: 0.1.0
language: zh-CN
---

# US Sanctions Zhejiang Monitoring

当用户要求采集、核对或分析美国制裁/管制清单中的中国或浙江相关主体时，使用本技能。

## 任务目标

构建可追溯的美国清单数据底表，识别涉浙企业和个人，并按清单口径解释法律后果、制裁原因和报告差异。

## 必须遵守的口径

不要把所有美国清单统称为同一种“制裁”：

- OFAC SDN：资产冻结、美国人交易禁止，可能有次级制裁。
- BIS Entity List：出口管制许可证限制，通常不冻结资产。
- DoD 1260H/CMC：中国军事企业识别和国防采购限制，不是 OFAC 式资产冻结。
- NS-CMIC：证券/投资限制。
- FCC Covered List：通信设备采购和政府资金限制。
- State/ISN/DTC：按具体清单解释，不要推定 SDN 后果。

## 标准流程

1. 锁定范围：日期、来源、地区、是否包含香港/澳门/台湾、是否包含船舶/航空器/外籍关联人。
2. 优先采官方源：OFAC Recent Actions、SDN Search、Federal Register/BIS、DoD 1260H、FCC、ITA CSL。
3. 结构化字段：日期、来源清单、动作类型、主体类型、英文名、中文名、地址、清单标签、Linked To、ID、来源链接、官方原文。
4. 识别浙江：Zhejiang、Hangzhou、Ningbo、Zhoushan、Wenzhou、Jinhua、Cixi、Yuyao、Yinzhou、USCC、注册地址、法人/股东关系。
5. 分类原因：基于官方 program/tag 和新闻稿；推断内容标为“初步判断”。
6. 比对报告：先同清单口径比对，再全口径比对；输出 matched、report-only、dataset-only。
7. 输出结果：优先 Excel，包含摘要、浙江命中、全量记录、来源覆盖、差异比对。

## 易错点

- 不要把 1260H/CMC 写成 SDN 制裁。
- 不要默认所有 OFAC 记录都有次级制裁，逐条看 `Subject to Secondary Sanctions`。
- 不要自动丢弃与中国/香港企业相关的外籍个人，除非用户明确排除。
- 不要把船舶算作企业，除非用户明确纳入。
- OFAC 中文名可能不是工商登记名，需同时保留官方名和规范名。

## 常用官方源

- OFAC Recent Actions: https://ofac.treasury.gov/recent-actions
- OFAC SDN Search: https://sanctionslist.ofac.treas.gov/Home/SdnList
- Federal Register API: https://www.federalregister.gov/api/v1/documents.json
- BIS Entity List: https://www.bis.doc.gov/index.php/policy-guidance/lists-of-parties-of-concern/entity-list
- ITA CSL CSV: https://data.trade.gov/downloadable_consolidated_screening_list/v1/consolidated.csv
- DoD 1260H/CMC: https://www.defense.gov/pubs/cmc-list/
- FCC Covered List: https://www.fcc.gov/supplychain/covered-list
