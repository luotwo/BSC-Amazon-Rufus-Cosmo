# BSC-Amazon-Rufus-Cosmo

一个面向新手的 Claude Code+SofttimeMCP+Sif MCP 技能，用来分析 Amazon ASIN 在 `COSMO + Rufus + Listing 转化` 上的表现，并输出可以直接落地的改写建议。

你可以把它理解成：
- 先帮你收集产品、评论、关键词、经营侧证据
- 再判断这个 Listing 是曝光差、点击差、转化差，还是预期错配
- 最后直接给出标题、Bullet、Q&A、Backend Search Terms、图片卖点、A+ 方案
<img width="313" height="676" alt="image" src="https://github.com/user-attachments/assets/2e41475a-e72c-4ed4-9e09-bd71db131209" />
<img width="384" height="1103" alt="image" src="https://github.com/user-attachments/assets/07db4850-76e5-4c27-83a9-d8ea02c06649" />


如果你平时会说这些话，这个技能就适合你：
- 分析这个 ASIN
- 看下这个 listing 为什么卖不好
- 帮我做 COSMO 审计
- 帮我做 Rufus 审计
- 帮我重写亚马逊文案
- 帮我补图片卖点和 A+ 方案

## 这个仓库包含什么

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

说明：
- `SKILL.md`：技能主规则
- `README.md`：新手说明书
- `docs/USAGE.md`：快速使用指南
- `examples/example-prompts.md`：可直接复制的提示词
- `OutPut/<ASIN>/`：每个 ASIN 的本地输出目录

## 先看这 3 个前提

在正式使用前，请先确认：
1. 你已经安装并能打开 Claude Code
2. 你已经把这个技能仓库放到本地
3. 你已经配置好 `sorftime` 和 `sif-mcp`

如果你只是想先跑起来，重点先完成这 3 件事：
- 配 `sorftime`
- 配 `sif-mcp`
- 用 `claude mcp list` 确认两个 MCP 都已连接

## 第一步：把仓库放到本地

你可以用 `git clone`，也可以直接下载 ZIP。

例如放到：

```text
D:\BSCSkills\BSC-Amazon-Skills-main\BSC-Amazon-Rufus-Cosmo
```

建议保留这个目录结构，不要随意改名和拆目录。

## 第二步：配置 sorftime MCP

`sorftime` 负责提供：
- 产品基础信息
- 评论和差评证据
- 竞品关键词或竞品表达

### 1）常见配置文件位置

通常把 `sorftime` 写在项目级 MCP 配置里：

```text
D:\ClaudeCode\Amazon-COSMO\.mcp.json
```

### 2）推荐写法

把下面内容写进 `.mcp.json` 的 `mcpServers` 里。

```json
{
  "mcpServers": {
    "sorftime": {
      "type": "streamableHttp",
      "url": "https://mcp.sorftime.com?key=<YOUR_SORFTIME_KEY>"
    }
  }
}
```

请把 `<YOUR_SORFTIME_KEY>` 换成你自己的 key。

### 3）注意事项

- 不要把真实 key 提交到 GitHub
- 不要把真实 key 写进 README、报告文件、截图
- 如果你已经有别的 MCP 配置，不要覆盖整个文件，只新增 `sorftime` 那一段

## 第三步：配置 sif-mcp

`sif-mcp` 负责提供：
- 广告结构数据
- 流量和趋势数据
- 经营侧证据
- 用于辅助判断曝光、点击、转化、广告结构问题

### 1）常见配置文件位置

通常把 `sif-mcp` 写在 Claude Code 用户级配置里：

```text
C:\Users\Administrator\.claude\settings.json
```

### 2）推荐写法

如果你的环境使用 `settings.json` 承载 MCP，可以按下面的结构补充：

```json
{
  "mcpServers": {
    "sif-mcp": {
      "type": "http",
      "url": "https://mcp.sif.com/mcp",
      "headers": {
        "Authorization": "Bearer <YOUR_SIF_TOKEN>"
      }
    }
  }
}
```

请把 `<YOUR_SIF_TOKEN>` 换成你自己的 token。

### 3）注意事项

- 不要把真实 token 提交到 GitHub
- 不要把 Authorization header 写进仓库文档或 `OutPut` 结果目录
- 如果你的 `settings.json` 里已经有别的配置，按原结构合并，不要整文件覆盖

## 第四步：检查 MCP 是否接入成功

配置完成后，在终端执行：

```bash
claude mcp list
```

你至少要看到：
- `sorftime`
- `sif-mcp`

理想状态是：
- 两个 MCP 都能显示出来
- `sif-mcp` 显示为已连接
- 没有授权失败、token 失效、登录过期之类报错

如果你还要同步飞书，再执行：

```bash
lark-cli auth status
```

如果提示未登录，请先登录：

```bash
lark-cli auth login
```

## 第五步：开始使用这个技能

### 最简单的提示词

如果你只是想先跑一下，直接说：

```text
分析 B0D5NJ1CKG
```

### 推荐提示词：证据优先

这是最推荐的新手写法：

```text
请基于真实证据，分析 B0D5NJ1CKG
```

### 指定站点的提示词

```text
请基于真实证据，分析 B0D5NJ1CKG，站点 US
```

### 做完整 COSMO + Rufus 审计

```text
请基于真实证据，帮我做 B0D5NJ1CKG 的 COSMO + Rufus 审计，不要猜测，缺失字段标注未获取到
```

### 直接要完整交付物

```text
请基于真实证据，分析 B0D5NJ1CKG，输出完整 10 板块 COSMO + Rufus 报告，并给我优化后的标题、5条 Bullet、Backend Search Terms、6条 Q&A、图片卖点和 A+ 方案，结果保存到 OutPut 目录
```

### 要求同步飞书

```text
请基于真实证据，分析 B0D5NJ1CKG，生成完整报告，保存到 OutPut 目录，并同步到飞书
```

## 这个技能会输出什么

一次完整运行，通常会输出以下 10 个板块：
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

其中第 9 和第 10 板块，通常是最容易直接拿去执行的内容。

## 输出会保存到哪里

默认输出目录：

```text
OutPut/<ASIN>/
```

例如：

```text
OutPut/B0D5NJ1CKG/
```

常见文件包括：
- `feishu_clean_report.md`
- `section1_2.md`
- `section7_8.md`
- `section9.md`
- `section10.md`

说明：
- 本地 `OutPut/<ASIN>/` 里的 Markdown 是源文件
- 如果同步飞书，飞书文档只是交付形态
- 不要把这个目录里的敏感数据提交到公开仓库

## 这个技能遵循的规则

- 先取证，再判断
- 缺失字段写 `未获取到`
- 不把猜测写成事实
- 不把行业常识写成该产品已经被证实的信息
- 没有经营侧数据时，不把广告和业务判断写成确定结论
- 不回退到旧 HTML 模板流程

## 新手最常见问题

### 1）为什么报告里会写“未获取到”

因为这个技能是证据优先。

没有拿到的数据，就应该明确写出来，而不是靠猜补齐。

### 2）为什么不是一上来就直接重写标题和 Bullet

因为先判断问题类型更重要。

一个 Listing 可能是：
- 曝光问题
- 点击问题
- 转化问题
- 预期错配问题

先判断，再改写，结果更可靠。

### 3）如果 sorftime 不可用怎么办

按规则处理：
- 缺失字段写 `未获取到`
- 不伪造产品、评论、竞品数据

### 4）如果 sif-mcp 不可用怎么办

按规则处理：
- 可以继续做 Listing / COSMO / Rufus 层面的证据分析
- 但不要把广告、流量、经营判断写成确定事实

## 更多参考

如果你想继续看更细的说明，可以再看：
- `docs/USAGE.md`
- `examples/example-prompts.md`
如果需要了解，共创，学习相关亚马逊运营Skill，请添加我们公众号和相关联系方式，进行分享相关亚马逊相关运营Skill源文件
![9f453825a605ac5a92149be126636dc4](https://github.com/user-attachments/assets/9680fd49-0f0f-4642-8601-462ca28f1c77)
![微信图片_20260409165035_4249_87](https://github.com/user-attachments/assets/16305816-7646-416e-9c37-e132bd592fa7)
---<img width="844" height="376" alt="image" src="https://github.com/user-attachments/assets/0c809a29-8dad-4fd0-b5ce-d439e250a60a" />
## License

详见 `LICENSE`。
