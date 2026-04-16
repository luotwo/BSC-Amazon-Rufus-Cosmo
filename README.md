# BSC-Amazon-Rufus-Cosmo

一个可重复使用的 Claude Code 技能，用于围绕 `COSMO + Rufus + Listing 转化` 审计 Amazon ASIN，并输出基于证据的诊断结果与可直接落地的改写方案。

它适合以下工作流：
- 分析某个 ASIN 为什么不容易被 Amazon AI 搜索理解
- 诊断 Listing 的曝光、点击和转化问题
- 重写标题、Bullet、Q&A、Backend Search Terms
- 生成图片卖点与 A+ 内容方向
- 产出运营团队可以直接执行的交付物

## 这个技能做什么

给定一个 ASIN，这个技能会产出一份结构化审计结果，默认回答四个核心问题：
1. 当前哪里失分
2. 为什么失分
3. 应该先改什么
4. 改完后怎么写

这个技能坚持“先证据，后判断”：
- 有数据就写事实
- 没拿到的数据就标注为 `未获取到`
- 不把猜测写成事实
- 不把运营经验伪装成页面现状

## 适用场景

当用户提出以下需求时，适合使用本技能：
- ASIN 分析
- COSMO 审计
- Rufus 适配度检查
- Listing 改写
- 语义盲区分析
- Q&A 优化
- 后台搜索词改写
- 图片卖点规划
- A+ 内容规划

示例请求：

```text
请基于真实证据，分析 B0D5NJ1CKG
```

```text
请基于真实证据，帮我做 B0D5NJ1CKG 的 COSMO + Rufus 审计，不要猜测，缺失字段标注未获取到
```

```text
请基于真实证据，分析 B0D5NJ1CKG，输出完整 10 板块 COSMO + Rufus 报告，并给我优化后的标题、5条 Bullet、Backend Search Terms、6条 Q&A、图片卖点和 A+ 方案，结果保存到 OutPut 目录
```

## 输出结构

一次完整运行通常覆盖以下 10 个板块：
1. 产品概览
2. 算法评分卡
3. 语义检索盲区分析
4. COSMO 节点诊断
5. Rufus 问答能力测试
6. 用户行为信号诊断
7. 竞品差异化可提取性
8. 改进优先级方案
9. 优化后文案
10. 图片卖点与 A+ 创意方案

## 仓库结构

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

## 使用前准备

在使用本技能前，请确认以下条件：
- 当前环境可以使用 Claude Code
- 本技能目录已在本地可访问
- 已配置 `sorftime` MCP，用于产品事实、评论和竞品关键词证据
- 已配置 `sif-mcp`，用于广告、流量、趋势和经营数据证据
- 如果需要同步飞书，已安装并登录 `lark-cli`

本工作流中常见的 MCP 配置路径：
- `D:\ClaudeCode\Amazon-COSMO\.mcp.json`
- `C:\Users\Administrator\.claude\settings.json`

建议先检查：

```bash
claude mcp list
lark-cli auth status
```

## 使用方法

在 Claude Code 中，直接给出 ASIN 即可开始。

最简单的提示词：

```text
分析 B0D5NJ1CKG
```

证据优先提示词：

```text
请基于真实证据，分析 B0D5NJ1CKG，站点 US
```

完整交付提示词：

```text
请基于真实证据，分析 B0D5NJ1CKG，输出完整 10 板块 COSMO + Rufus 报告，并给我优化后的标题、5条 Bullet、Backend Search Terms、6条 Q&A、图片卖点和 A+ 方案，结果保存到 OutPut 目录
```

更多示例可参考：
- `docs/USAGE.md`
- `examples/example-prompts.md`

## 输出位置

生成结果应统一保存到：

```text
OutPut/<ASIN>/
```

常见输出文件包括：
- `feishu_clean_report.md`
- `section1_2.md`
- `section7_8.md`
- `section9.md`
- `section10.md`
- 其他过程产物或报告文件

## 本技能遵循的规则

- 先取证，再判断
- 缺失字段标注为 `未获取到`
- 不把猜测写成事实
- 缺少经营证据时，不把广告或业务判断写成确定结论
- 不把 token、Authorization header、cookie 等敏感信息写入报告
- 不回退到旧的 HTML 模板输出流程

## 说明

- `OutPut/<ASIN>/` 下的本地 Markdown 文件是源文件。
- 如果同步飞书，飞书文档只是交付形态，不是唯一源文件。
- 如果 `sorftime` 不可用，缺失证据应明确保留为 `未获取到`。
- 如果 `sif-mcp` 不可用，经营侧判断应保持非确定性表达。

## License

详见 `LICENSE`。
