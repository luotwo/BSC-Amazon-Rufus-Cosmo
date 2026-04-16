# Usage Guide

## Quick Start

1. Open Claude Code in the project environment.
2. Make sure the skill directory is available at:
   - `D:\BSCSkills\BSC-Amazon-Skills-main\BSC-Amazon-Rufus-Cosmo`
3. Confirm the required MCPs are configured:
   - `sorftime` for product facts, reviews, and competitor keyword evidence
   - `sif-mcp` for advertising, traffic, and trend evidence
4. Ask Claude to analyze an ASIN.

Example:

```text
分析 B0D5NJ1CKG
```

## Minimum Run Checklist

Before you start a real ASIN audit, quickly confirm the following:

- `SKILL.md`, `README.md`, and `docs/USAGE.md` are present in the skill folder
- the `OutPut` directory exists and is writable in the current session
- `claude mcp list` shows both `sorftime` and `sif-mcp`
- if Feishu sync is needed, `lark-cli auth status` shows a logged-in user
- you already have the target ASIN, such as `B0D5NJ1CKG`

If all five checks pass, you can usually run the full workflow directly.

## MCP Setup

Before running the skill, confirm Claude Code can access both required MCP servers:

- `sorftime`: product detail, reviews, competitor keywords
- `sif-mcp`: ad structure, traffic, trend, and other business evidence

Common config file locations:

- Project-level MCP config: `D:\ClaudeCode\Amazon-COSMO\.mcp.json`
- User-level Claude config: `C:\Users\Administrator\.claude\settings.json`

Recommended check command:

```bash
claude mcp list
```

You should verify:

- `sorftime` exists and can be called
- `sif-mcp` exists and is connected
- no expired login or authorization errors are present

If `sorftime` is unavailable, the report must mark missing fields as `未获取到`.
If `sif-mcp` is unavailable, do not write definitive advertising conclusions.
Do not save tokens, authorization headers, or cookies into repo docs or `OutPut` files.

## Recommended Prompt Patterns

### Full audit

```text
请基于真实证据，分析 B0D5NJ1CKG，输出完整 10 板块 COSMO + Rufus 报告，并把结果保存到 OutPut 目录
```

### Audit + rewrite

```text
请基于真实证据，分析 B0D5NJ1CKG，并给我优化后的标题、5条 Bullet、Backend Search Terms、6条 Q&A、图片卖点和 A+ 方案；不要猜测，缺失字段标注未获取到
```

### Audit + Feishu sync

```text
请基于真实证据，分析 B0D5NJ1CKG，生成完整报告，保存到 OutPut 目录，并同步到飞书
```

## Output Location

All report files should be stored under:

`D:\BSCSkills\BSC-Amazon-Skills-main\BSC-Amazon-Rufus-Cosmo\OutPut\<ASIN>\`
