<h1 align="center">多风格品牌 PPT 生成器</h1>

<p align="center"><code>space-multi-design-ppt.skill</code></p>

<p align="center"><em>「同一份内容，可以长成 62 种品牌气质的演示稿」</em></p>

<p align="center">
  <img alt="Agent Skills Standard" src="https://img.shields.io/badge/Agent%20Skills-Standard-5aa524?style=for-the-badge">
  <img alt="Brand Systems" src="https://img.shields.io/badge/Brand%20Systems-62-c8a500?style=for-the-badge">
  <img alt="Output" src="https://img.shields.io/badge/Output-HTML%20%C2%B7%20PPTX%20%C2%B7%20PDF-1888c8?style=for-the-badge">
  <img alt="Runtime" src="https://img.shields.io/badge/Runtime-Claude%20Code%20%C2%B7%20Codex%20%C2%B7%20Cursor-7b2bd9?style=for-the-badge">
</p>

多风格品牌 PPT 生成器（Space Multi Design PPT）是一个品牌设计风格驱动的 AI 幻灯片生成 Skill。

它把一段文章、BP、周报、产品介绍或课程内容，转成带真实品牌设计语言的演示稿。你可以指定 Apple、Notion、Claude、Stripe、Linear、Tesla 等风格，也可以让它根据内容智能推荐 5 种匹配风格，并提供第 6 个「智能匹配」选项。

它不是让 AI 随机做一套“看起来还行”的 PPT。

它会先理解内容，再选择设计系统、输出格式和页面结构。核心依赖 [brand-design-md](https://github.com/SpaceZephyr/brand-design-md) 的 62 个真实品牌规范，以及 [getdesign.md](https://getdesign.md) 的 DESIGN.md token，让颜色、字体、字距、圆角和视觉节奏都有来源。

看效果 · 风格墙 · 安装 · 使用 · 输出格式 · 工作原理 · 诚实边界

## 案例展示

| FlowPilot · Notion | 橙洲咖啡 · Claude |
|---|---|
| <img src="https://raw.githubusercontent.com/SpaceZephyr/space-multi-design-ppt/main/examples/flowpilot-notion/preview.png" alt="FlowPilot · Notion" width="100%"> | <img src="https://raw.githubusercontent.com/SpaceZephyr/space-multi-design-ppt/main/examples/chengzhou-coffee-claude/preview.png" alt="橙洲咖啡 · Claude" width="100%"> |

## 风格墙

| Apple | Claude | Notion | Stripe |
|---|---|---|---|
| <img src="https://raw.githubusercontent.com/SpaceZephyr/space-multi-design-ppt/main/examples/style-gallery/images/apple.png" alt="Apple" width="100%"> | <img src="https://raw.githubusercontent.com/SpaceZephyr/space-multi-design-ppt/main/examples/style-gallery/images/claude.png" alt="Claude" width="100%"> | <img src="https://raw.githubusercontent.com/SpaceZephyr/space-multi-design-ppt/main/examples/style-gallery/images/notion.png" alt="Notion" width="100%"> | <img src="https://raw.githubusercontent.com/SpaceZephyr/space-multi-design-ppt/main/examples/style-gallery/images/stripe.png" alt="Stripe" width="100%"> |

| Linear | Tesla | Vercel | Figma |
|---|---|---|---|
| <img src="https://raw.githubusercontent.com/SpaceZephyr/space-multi-design-ppt/main/examples/style-gallery/images/linear.png" alt="Linear" width="100%"> | <img src="https://raw.githubusercontent.com/SpaceZephyr/space-multi-design-ppt/main/examples/style-gallery/images/tesla.png" alt="Tesla" width="100%"> | <img src="https://raw.githubusercontent.com/SpaceZephyr/space-multi-design-ppt/main/examples/style-gallery/images/vercel.png" alt="Vercel" width="100%"> | <img src="https://raw.githubusercontent.com/SpaceZephyr/space-multi-design-ppt/main/examples/style-gallery/images/figma.png" alt="Figma" width="100%"> |

| NVIDIA | Airbnb | Spotify | Miro |
|---|---|---|---|
| <img src="https://raw.githubusercontent.com/SpaceZephyr/space-multi-design-ppt/main/examples/style-gallery/images/nvidia.png" alt="NVIDIA" width="100%"> | <img src="https://raw.githubusercontent.com/SpaceZephyr/space-multi-design-ppt/main/examples/style-gallery/images/airbnb.png" alt="Airbnb" width="100%"> | <img src="https://raw.githubusercontent.com/SpaceZephyr/space-multi-design-ppt/main/examples/style-gallery/images/spotify.png" alt="Spotify" width="100%"> | <img src="https://raw.githubusercontent.com/SpaceZephyr/space-multi-design-ppt/main/examples/style-gallery/images/miro.png" alt="Miro" width="100%"> |

## 安装

多风格品牌 PPT 生成器基于开放的 Agent Skills 协议，可在 Claude Code、Codex、Cursor 等兼容 runtime 中运行。

### 方式一：让 Agent 安装

打开你正在用的 agent，告诉它：

```text
帮我安装这个 skill：https://github.com/SpaceZephyr/space-multi-design-ppt
```

### 方式二：手动安装

把本仓库克隆到 skills 目录：

```bash
git clone https://github.com/SpaceZephyr/space-multi-design-ppt.git ~/.codex/skills/space-multi-design-ppt
```

Claude Cowork / Claude.ai 可以把仓库打包上传为 Skill（Settings → Capabilities → Skills）。

依赖：Node.js（`npx getdesign` 拉取设计规范）；输出 PPTX 需 `pip install python-pptx Pillow`；输出 PDF 需 Playwright/Chromium。

## 使用

```
把这篇文章做成 PPT                        # → 触发 5+1 风格推荐
用 Linear 风格把这份周报做成 slide         # → 指定风格直接生成
做一个 Tesla 风格的产品发布 deck，导出 pptx # → 生成 + 导出
用 Claude 风格生成 HTML 和 PDF             # → 同时输出 deck.html / PDF
Notion 配色 + Linear 排版，做个路演 PPT    # → 混搭风格
```

## 输出格式

| 格式 | 适合场景 | 说明 |
| --- | --- | --- |
| `deck.html` | 线上演示、追求视觉效果 | 单文件网页幻灯片，支持翻页、全屏、网格总览 |
| `.pptx` | 需要二次编辑、正式交付 | python-pptx 原生构建，文本框和形状可编辑 |
| `.pdf` | 归档、发送、打印 | 从 HTML 幻灯片导出，适合固定版式交付 |

## 它能做什么

| 能力 | 说明 |
| --- | --- |
| 内容转演示稿 | 把文章、BP、周报、产品介绍、课程内容转成完整 Slide |
| 智能风格推荐 | 未指定风格时，推荐 5 种匹配品牌 + 1 个智能匹配选项 |
| 指定品牌风格 | 支持 Apple、Notion、Claude、Stripe、Linear、Tesla 等 62 种品牌设计语言 |
| 多格式交付 | 输出 `deck.html`、可编辑 `.pptx`，或固定版式 `.pdf` |
| 可追溯设计 token | 颜色、字体、字距、圆角、阴影来自 DESIGN.md，而不是凭感觉猜 |

## 支持的 62 个品牌风格

Apple · Claude · Cursor · ElevenLabs · Figma · Framer · Lovable · Meta · MiniMax · Mintlify · Mistral · Notion · Ollama · OpenCode · PostHog · Raycast · Replicate · Resend · Runway · Sanity · Sentry · Supabase · Superhuman · Together AI · Vercel · VoltAgent · Warp · Webflow · X.AI · Zapier · Airtable · Cal.com · Clay · ClickHouse · Cohere · Composio · Expo · HashiCorp · IBM · Intercom · Linear · Miro · MongoDB · NVIDIA · Pinterest · Stripe · Binance · Coinbase · Kraken · Revolut · Wise · Airbnb · BMW · Ferrari · Lamborghini · Nike · Renault · Shopify · SpaceX · Spotify · Tesla · Uber

每个品牌的一句话风格与内容匹配标签见 [references/brand-registry.md](references/brand-registry.md)。

## 工作原理

多风格品牌 PPT 生成器会把一次幻灯片任务拆成 5 层：

| 层次 | 说明 |
| --- | --- |
| 内容理解 | 提取核心信息、受众、支撑点和适合的页数 |
| 风格决策 | 用户指定则直接使用；未指定则按内容推荐 5+1 个品牌风格 |
| token 获取 | 通过 getdesign.md 拉取品牌 DESIGN.md，提取颜色、字体、间距和组件气质 |
| 页面生成 | HTML 模式生成 1280×720 独立页面；PPTX 模式生成可编辑文本框和形状 |
| 交付检查 | 合成 deck.html，或生成 PPTX/PDF，并检查文字溢出、重叠和版式问题 |

## 仓库结构

```
├── SKILL.md                      # Skill 主流程（8 步工作流）
├── references/
│   ├── brand-registry.md         # 62 品牌注册表：slug、风格描述、匹配标签、信号速查
│   ├── slide-html-guide.md       # 1280×720 HTML 幻灯片制作规范与布局模板
│   ├── pptx-native-guide.md      # python-pptx 原生可编辑 PPTX 构建规范
│   ├── outline-guide.md          # 内容分析、大纲格式、文案规则
│   └── image-mode.md             # 可选 AI 图像模式（需 LabNana API key）
├── scripts/
│   ├── build_deck.py             # slides/*.html → 单文件 deck.html（翻页/全屏/总览）
│   ├── export_deck.py            # HTML → PNG →  PPTX / PDF
│   └── generate_slide.py         # 图像模式生成器（来自 space-slide-deck）
├── evals/evals.json              # 测试用例（实测：断言通过率 100% vs 无 skill 基线 20%）
└── examples/                     # 实测案例与多风格图片画廊
```

## 质量基准

用 2 个真实场景测试（与无 skill 的 Claude 基线对比）：

| 指标 | 带 Skill | 无 Skill |
|---|---|---|
| 断言通过率（真实品牌 token / 推荐流程 / 叙事标题 / 数据准确） | **100%** | 20% |
| 典型差异 | 拉取真实 DESIGN.md，精确到 `-2.125px` 字距 | 凭记忆猜色值，标签式标题，无风格推荐 |

## 诚实边界

- 品牌风格是基于公开 DESIGN.md token 的设计语言迁移，不是品牌官方模板。
- HTML 的视觉还原更强；PPTX 的优势是可编辑，但复杂渐变和细节会做合理近似。
- 如果 getdesign.md 拉取失败，会使用内置品牌注册表做近似还原。
- PDF 导出依赖 Playwright/Chromium；PPTX 原生构建不依赖浏览器。

## 致谢

- [SpaceZephyr/brand-design-md](https://github.com/SpaceZephyr/brand-design-md) — 品牌设计规范获取
- [SpaceZephyr/design-buddy](https://github.com/SpaceZephyr/design-buddy) — space-slide-deck 幻灯片流程
- [getdesign.md](https://getdesign.md) — 品牌 DESIGN.md 数据源
