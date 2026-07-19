# career-destination-report

Cursor Agent Skill：按**专业**与**目标国家/地区**调研就业去向与顶尖用人企业，产出 **Word 汇总 + CareerAtlas 可视 HTML**。

## 安装

```bash
# 克隆到个人 skills 目录
git clone https://github.com/zhuzhu0833-star/career-destination-report.git \
  ~/.cursor/skills/career-destination-report
```

将 `zhuzhu0833-star` 替换为实际 GitHub 用户名或组织名。安装后重启 Cursor 或新开 Agent 对话即可发现该 skill。

依赖（生成 Word 时）：

```bash
pip3 install python-docx
```

## 调用方式

- `/career-destination-report`
- 「做一份就业去向和顶尖用人企业报告」
- 「Finance 专业，英国和新加坡就业报告」

## 产出前询问（强制）

Agent 会先确认：

1. **专业**（可自填）
2. **目标国家/地区**（多选 1–3：北美 / 美国 / 加拿大 / 中国大陆 / 香港 / 英国 / 新加坡 / 澳洲 / 其他）

## 交付物

| 文件 | 命名 |
|------|------|
| Word | `{专业}专业就业去向与顶尖用人企业汇总.docx` |
| HTML | `{专业}就业报告可视化.html` |

默认写到当前工作区根目录。

## 目录结构

```
career-destination-report/
├── SKILL.md
├── reference.md
├── README.md
├── templates/
│   └── report-visual.html
└── scripts/
    └── build_docx.py
```

## 本地生成 Word 示例

```bash
python3 scripts/build_docx.py \
  --major Marketing \
  --major-zh 市场营销 \
  --regions "北美,中国大陆" \
  --json /path/to/content.json \
  --out ./市场营销专业就业去向与顶尖用人企业汇总.docx
```

`content.json` 字段说明见 `reference.md`。

## License

MIT
