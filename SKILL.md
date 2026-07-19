---
name: career-destination-report
description: >-
  Researches major-specific career destinations and top employers by country/region,
  then delivers a Word summary plus a CareerAtlas-style visual HTML report. Use when
  the user asks for /career-destination-report, 就业去向, 顶尖用人企业, 就业报告,
  career destination, employment outlook by major, or top employers for a major.
---

# Career Destination Report（专业就业去向 → Word + 可视 HTML）

## 如何调用

1. **显式调用**：`用 /career-destination-report 做就业报告`
2. **自然触发**：`就业去向和顶尖用人企业`、`帮我出一份就业报告`
3. **带参数**：`Finance 专业，英国和新加坡的就业去向报告`

Skill 路径：`~/.cursor/skills/career-destination-report/SKILL.md`

## Quick start

1. **产出前必须询问**专业 + 目标国家/地区（见 Step 0）——即使用户已部分说明，也要确认未给全的项。
2. **检索**就业去向、岗位类型、顶尖雇主（见 [reference.md](reference.md)）。
3. **生成 Word**：`scripts/build_docx.py`（或等价 python-docx 逻辑）。
4. **生成 HTML**：基于 [templates/report-visual.html](templates/report-visual.html) 填入研究内容。
5. **交付**两个文件路径 + 一句结论。

默认输出目录：当前工作区根目录。可按用户指定路径调整。

## Workflow checklist

```
- [ ] Step 0: 专业 + 国家/地区已确认（AskQuestion）
- [ ] 官方/权威源检索完成（按选定地区）
- [ ] Word 已生成：{专业}专业就业去向与顶尖用人企业汇总.docx
- [ ] HTML 已生成：{专业}就业报告可视化.html
- [ ] 文内引用主要来源；交付路径给用户
```

## Step 0 — 产出前询问（强制）

**在任何检索或写文件之前**，用 AskQuestion 一次问清以下两项。若 AskQuestion 不可用，则在对话中用清晰选项追问，等用户回答后再继续。

### Q1 — 专业（必填）

Header: `专业`

Options（可按语境增删，必须含「其他」）:

- Marketing / 市场营销
- Computer Science / 计算机
- Finance / 金融
- Accounting / 会计
- Business Analytics / 商业分析
- 其他，我自行填写

若选「其他」，请用户在聊天中粘贴专业中英文名。

### Q2 — 目标国家/地区（必填，多选 1–3）

Header: `目标市场`

Allow multiple（1–3）:

- 北美（美国+加拿大）
- 美国
- 加拿大
- 中国大陆
- 香港
- 英国
- 新加坡
- 澳洲
- 其他，我自行填写

若用户消息已明确给出专业与地区（例如「CS，北美和中国」），可跳过已明确项，只追问缺失项。

### 可选参数（有默认则不问）

| 参数 | 默认 | 说明 |
|------|------|------|
| 输出目录 | 当前工作区根目录 | 用户指定则用之 |
| 语言 | 中文（专有名词可中英并列） | 除非用户要求英文全文 |

## Step 1 — 研究

按 [reference.md](reference.md) 检索，覆盖：

1. 宏观就业前景（增长、薪资量级、供需趋势）
2. 十大左右就业方向 / 典型岗位
3. 典型晋升路径（3–4 条轨道）
4. **每个选定地区**的顶尖用人企业（按行业分组：科技、快消/消费、金融、咨询/专业服务等，视专业调整）
5. 地区对比要点（若 ≥2 个地区）
6. 求职准备建议（硬技能 / 软技能 / 地区差异化）

优先权威源；标注来源；勿编造精确薪资或排名——不确定时写区间或「示意」。

## Step 2 — 生成 Word

优先运行：

```bash
python3 ~/.cursor/skills/career-destination-report/scripts/build_docx.py \
  --major "Marketing" \
  --major-zh "市场营销" \
  --regions "北美,中国大陆" \
  --out "/path/to/{专业}专业就业去向与顶尖用人企业汇总.docx" \
  --json /path/to/content.json
```

`content.json` 结构见 [reference.md](reference.md)。若脚本不可用，可用 python-docx 按同一章节结构手写生成，章节不得省略：

1. 专业概况与就业前景  
2. 主要就业方向  
3. 典型职业路径  
4. 各地区顶尖用人企业（一节一地区）  
5. 地区对比（多地区时）  
6. 求职准备建议  
7. 主要参考来源  

文件名：`{专业简称或中文}专业就业去向与顶尖用人企业汇总.docx`

## Step 3 — 生成可视化 HTML

1. 复制 [templates/report-visual.html](templates/report-visual.html)  
2. 替换所有 `{{PLACEHOLDER}}`（见模板顶部注释）  
3. 按选定地区生成雇主 Tab（1–3 个 panel）  
4. 保持 CareerAtlas 视觉：青绿 `#0d7a78` + 琥珀 `#d4920a` + 珊瑚强调；字体 Fraunces / Noto Serif SC / Noto Sans SC  
5. **禁止**紫色渐变、Inter/Roboto 默认栈、奶油底+赤陶的泛 AI 审美  

文件名：`{专业}就业报告可视化.html`

HTML 必须包含：Hero、关键数据卡、热度条（可示意）、就业方向、晋升路径、雇主 Tabs、对比表（多地区）、求职清单、来源。

## Step 4 — 交付

向用户返回：

- Word 绝对路径  
- HTML 绝对路径（提示可双击用浏览器打开）  
- 一句关键结论（就业主赛道 + 最值得冲的雇主类型）  

**不要**主动 commit / push 用户工作区仓库。本 skill 仓库本身的维护除外。

## 设计与文风

- 咨询顾问口吻，直接、可扫读；少空话。  
- 表格优先于长段落。  
- 雇主列表为「高频目标雇主」，勿声称官方完整排名。  
- 日期写整理当日。  

## 示例

**用户**：`帮我做一份就业去向报告`  
**Agent**：AskQuestion（专业 + 地区）→ 检索 → Word + HTML → 交付路径  

**用户**：`/career-destination-report Computer Science，北美和中国`  
**Agent**：参数已齐，直接研究并产出（可简短复述确认）。
