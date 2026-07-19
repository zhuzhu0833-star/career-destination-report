# Career Destination Report — Reference

## 检索源优先级

按选定地区选用权威源；能交叉验证的尽量 ≥2 源。

### 通用

- 国家/地区官方劳工统计（就业展望、薪资中位数）
- 大型招聘平台 / 人才市场报告（LinkedIn、Robert Half、本地等价）
- 顶尖高校就业质量报告 / 专业就业去向统计
- 企业官方校招 / 职能介绍页（Brand、PMM、投行、咨询等）
- 行业媒体对「热门雇主」「校招去向」的汇总（标注为二手）

### 地区速查

| 地区 | 优先源示例 |
|------|------------|
| 美国 / 北美 | BLS OOH；大学 career outcome；P&G/FAANG 等校招页 |
| 加拿大 | StatCan；Brainstorm Top Employer；银行/Shopify 等 |
| 中国大陆 | 高校就业质量报告；大厂/快消校招；行业协会报告 |
| 香港 | 高校 career report；金融/四大/政府相关招聘 |
| 英国 | ONS / Prospects；Times Top 100 Graduate Employers |
| 新加坡 | MOM；大学 career；金融/咨询/科技 hub 雇主 |
| 澳洲 | ABS；GradAustralia；Big 4 / 矿企 / 科技 |

### 按专业调整雇主分组

| 专业类型 | 优先分组 |
|----------|----------|
| Marketing / 商科营销 | 科技平台、快消、零售、广告代理、咨询 |
| CS / 数据 / AI | 科技大厂、金融科技、咨询（Tech）、创业公司 |
| Finance / 会计 | 投行/买方、商业银行、四大、企业财务、监管 |
| 工程 | 制造业、能源、科技硬件、工程咨询 |
| 设计 / 传媒 | 代理机构、互联网内容、品牌内部创意 |

不要机械套用 Marketing 分组；按专业重写分组标题与雇主。

---

## content.json 结构（供 build_docx.py）

```json
{
  "major": "Marketing",
  "major_zh": "市场营销",
  "regions": ["北美", "中国大陆"],
  "date": "2026-07-19",
  "outlook": {
    "summary": "一段宏观概述",
    "stats": [
      {"label": "营销经理就业增长", "value": "+6%", "note": "BLS 2024–2034"}
    ],
    "bullets": ["要点1", "要点2"]
  },
  "paths": [
    {
      "name": "品牌管理",
      "roles": "Brand Manager / ABM",
      "skills": "定位、跨部门",
      "industries": "快消、美妆"
    }
  ],
  "ladders": [
    {
      "title": "快消品牌线",
      "steps": ["助理品牌经理", "品牌经理", "高级品牌经理", "品类总监"]
    }
  ],
  "employers_by_region": {
    "北美": [
      {
        "group": "科技与互联网",
        "items": [
          {"name": "Amazon", "roles": "Brand / Growth", "badge": "发布量前列"}
        ]
      }
    ]
  },
  "compare": [
    {
      "dimension": "热门赛道",
      "cells": {"北美": "PMM / Growth", "中国大陆": "用户增长 / 内容电商"}
    }
  ],
  "skills": {
    "hard": ["Excel / SQL", "..."],
    "soft": ["跨部门沟通", "..."],
    "edge": ["AI 辅助投放", "..."]
  },
  "sources": [
    "U.S. BLS — ...",
    "..."
  ],
  "heat": [
    {"label": "增长 / Growth", "width": 92, "level": "高", "tone": ""}
  ]
}
```

`heat[].tone`：空字符串 | `amber` | `coral`（对应 HTML 条颜色）。

---

## Word 章节模板

### 一、专业概况与就业前景

- 专业能力边界（2–4 句）
- 宏观数据 bullets（带来源）
- 就业方向表（方向 / 典型岗位 / 能力侧重 / 常见行业）

### 二、典型职业路径

- 3–4 条晋升轨道 bullets

### 三、{地区}顶尖用人企业

每个选定地区单独一节（或一节内二级标题）：

- 按行业分组表格或 bullets
- 注明「高频目标，非官方完整排名」

### 四、地区对比（仅多地区）

- 维度表：热门赛道、入门通道、能力侧重、竞争态势、地理集中

### 五、求职准备建议

- 硬技能 / 软技能 / 差异化准备 / 作品集

### 六、主要参考来源

- 列表，可含 URL

---

## HTML 占位符一览

见 `templates/report-visual.html` 文件头注释。Agent 替换后不得残留 `{{`。

关键占位符：

| 占位符 | 含义 |
|--------|------|
| `{{MAJOR}}` | 英文或主显示专业名 |
| `{{MAJOR_ZH}}` | 中文专业名（可与 MAJOR 相同） |
| `{{REGIONS_LABEL}}` | 如「北美 · 中国大陆」 |
| `{{DATE}}` | 整理日期 |
| `{{HERO_LEAD}}` | Hero 副文案一句 |
| `{{OUTLOOK_LEAD}}` | 前景节导语 |
| `{{STATS_HTML}}` | 4 个 `.stat` 块 |
| `{{HEAT_HTML}}` | `.bar-row` 列表 |
| `{{PATHS_HTML}}` | `.path-item` 列表 |
| `{{LADDERS_HTML}}` | `.ladder-col` 列表 |
| `{{TABS_HTML}}` | Tab 按钮 |
| `{{PANELS_HTML}}` | 雇主 panel |
| `{{COMPARE_SECTION}}` | 整段对比 section（单地区可为空注释） |
| `{{SKILLS_HTML}}` | 三列技能 |
| `{{SOURCES_HTML}}` | `<li>` 列表 |

---

## AskQuestion 失败时的对话回退

```
在生成报告前需要确认：
1) 专业名称？（如 Marketing / CS / Finance，或其他请直接打出）
2) 目标国家/地区？（可多选，最多 3 个：北美 / 美国 / 加拿大 / 中国大陆 / 香港 / 英国 / 新加坡 / 澳洲 / 其他）
```

等齐答案再检索。

---

## 质量红线

- 不编造不存在的「官方排名第 N」
- 薪资写清币种与年份/来源口径
- 初级岗位承压、AI 影响等趋势需有出处或标明为行业观察
- 单地区时隐藏或省略「对比」大表，避免空列
