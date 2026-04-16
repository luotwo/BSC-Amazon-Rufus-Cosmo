# BSC-Amazon-Rufus-Cosmo

A reusable Claude Code skill for auditing Amazon ASINs across `COSMO + Rufus + Listing conversion`, then turning the findings into evidence-based rewrite actions.

It is designed for workflows like:
- auditing why an ASIN is not being understood well by Amazon AI search
- diagnosing Listing visibility, click-through, and conversion gaps
- rewriting titles, bullets, Q&A, and backend search terms
- generating image messaging and A+ content directions
- producing deliverables that an operations team can directly use

## What this skill does

Given an ASIN, the skill helps produce a structured audit that answers four core questions:
1. Where the listing is losing points
2. Why it is losing points
3. What should be fixed first
4. How the improved copy should be written

The skill is evidence-first:
- if data exists, it is treated as evidence
- if data is missing, it should be marked as `未获取到`
- assumptions should not be written as facts
- operational experience should not be disguised as current listing truth

## Best fit

Use this skill when the user asks for things like:
- ASIN analysis
- COSMO audit
- Rufus readiness review
- listing rewrite
- semantic blind spot diagnosis
- Q&A optimization
- backend search term rewrite
- image selling point planning
- A+ content planning

Example requests:

```text
请基于真实证据，分析 B0D5NJ1CKG
```

```text
请基于真实证据，帮我做 B0D5NJ1CKG 的 COSMO + Rufus 审计，不要猜测，缺失字段标注未获取到
```

```text
请基于真实证据，分析 B0D5NJ1CKG，输出完整 10 板块 COSMO + Rufus 报告，并给我优化后的标题、5条 Bullet、Backend Search Terms、6条 Q&A、图片卖点和 A+ 方案，结果保存到 OutPut 目录
```

## Output structure

A full run is expected to cover these 10 sections:
1. Product overview
2. Algorithm scorecard
3. Semantic retrieval blind spot analysis
4. COSMO node diagnosis
5. Rufus Q&A readiness test
6. User behavior signal diagnosis
7. Competitor differentiation extractability
8. Improvement priority plan
9. Optimized copy
10. Image selling points and A+ concept plan

## Repository structure

```text
BSC-Amazon-Rufus-Cosmo/
├─ SKILL.md
├─ README.md
├─ LICENSE
├─ docs/
│  └─ USAGE.md
├─ examples/
│  └─ example-prompts.md
└─ OutPut/
   └─ <ASIN>/
```

## Requirements

Before using the skill, confirm the following:
- Claude Code is available in your environment
- the skill folder is available locally
- `sorftime` MCP is configured for product facts, reviews, and competitor keyword evidence
- `sif-mcp` is configured for advertising, traffic, trend, and business evidence
- if Feishu sync is needed, `lark-cli` is installed and logged in

Common local MCP config locations used in this workflow:
- `D:\ClaudeCode\Amazon-COSMO\.mcp.json`
- `C:\Users\Administrator\.claude\settings.json`

Recommended check commands:

```bash
claude mcp list
lark-cli auth status
```

## Usage

Start with a direct ASIN request in Claude Code.

Minimal prompt:

```text
分析 B0D5NJ1CKG
```

Evidence-first prompt:

```text
请基于真实证据，分析 B0D5NJ1CKG，站点 US
```

Full deliverable prompt:

```text
请基于真实证据，分析 B0D5NJ1CKG，输出完整 10 板块 COSMO + Rufus 报告，并给我优化后的标题、5条 Bullet、Backend Search Terms、6条 Q&A、图片卖点和 A+ 方案，结果保存到 OutPut 目录
```

For more examples, see:
- `docs/USAGE.md`
- `examples/example-prompts.md`

## Output location

Generated reports should be stored under:

```text
OutPut/<ASIN>/
```

Typical generated files may include:
- `feishu_clean_report.md`
- `section1_2.md`
- `section7_8.md`
- `section9.md`
- `section10.md`
- other generated report artifacts

## Rules this skill follows

- evidence first, then judgment
- mark missing fields as `未获取到`
- do not turn assumptions into facts
- do not write advertising or business conclusions as certainties when business evidence is unavailable
- do not write secrets, tokens, authorization headers, or cookies into reports
- do not fall back to legacy HTML template output

## Notes

- The local Markdown files under `OutPut/<ASIN>/` are treated as the source artifacts.
- If Feishu is used, the Feishu document is only the synced delivery form.
- If `sorftime` is unavailable, missing evidence should stay explicitly marked as `未获取到`.
- If `sif-mcp` is unavailable, business-side conclusions should remain non-definitive.

## License

See `LICENSE`.
