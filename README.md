# Space Multi Design PPT

> 品牌设计风格驱动的 AI 幻灯片生成 Skill —— 把任意内容变成带顶级品牌设计语言的 Slide，支持输出 HTML / PPTX / PDF。

结合 [brand-design-md](https://github.com/SpaceZephyr/brand-design-md)（62 个真实品牌设计规范）与 [design-buddy/space-slide-deck](https://github.com/SpaceZephyr/design-buddy/tree/main/space-slide-deck)（幻灯片生成流程）。核心理念：**不靠凭空发挥的"好看"**——通过 [getdesign.md](https://getdesign.md) 拉取 Apple、Notion、Claude、Stripe、Linear、Tesla 等品牌的精确设计 token（颜色、字体、字距、圆角、阴影的具体数值），用真实规范驱动幻灯片渲染。

## 它是怎么工作的

```
你发内容 ──► 内容分析 ──► 风格决策 ──► 输出格式确认 ──► 拉取品牌 DESIGN.md ──► 生成 Slide
                              │
             ┌────────────────┴────────────────┐
             │ 你指定了风格（"用 Stripe 风格"）  │ 直接生成
             │ 你没指定风格                     │ 推荐 5 个匹配品牌（各一句话介绍）
             │                                 │ + 第 6 项「智能匹配」由 AI 选定并说明理由
             └─────────────────────────────────┘
```

## 输出格式

| 格式 | 适合场景 | 说明 |
|---|---|---|
| `deck.html` | 线上演示、追求视觉效果 | 单文件网页幻灯片，支持翻页、全屏、网格总览 |
| `.pptx` | 需要二次编辑、正式交付 | python-pptx 原生构建，文本框和形状可编辑 |
| `.pdf` | 归档、发送、打印 | 从 HTML 幻灯片导出，适合固定版式交付 |

**5+1 推荐示例**（发一份咖啡连锁 BP 后，Skill 的实际回复）：

> 1. **Stripe** — 紫色渐变 + 300 字重优雅排版，投资人看惯的金融科技质感
> 2. **Claude** — 奶油暖底 + 赭石强调色，和咖啡品牌的暖调天然契合
> 3. **Airbnb** — 珊瑚暖色 + 圆润 UI，适合讲社区与复购故事
> 4. **Shopify** — 深色电影感 + 荧光绿，创业增长叙事的现代锋利感
> 5. **Apple** — 极致留白，让 62% 毛利这些数字自己说话
> 6. **智能匹配** — 我根据内容气质直接选择最合适的风格（含混搭）

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

**Claude Code**：把本仓库克隆到 skills 目录

```bash
git clone https://github.com/SpaceZephyr/space-multi-design-ppt.git ~/.codex/skills/space-multi-design-ppt
```

**Claude Cowork / Claude.ai**：把仓库打包上传为 Skill（Settings → Capabilities → Skills）。

依赖：Node.js（`npx getdesign` 拉取设计规范）；输出 PPTX 需 `pip install python-pptx Pillow`；输出 PDF 需 Playwright/Chromium。

## 使用

```
把这篇文章做成 PPT                        # → 触发 5+1 风格推荐
用 Linear 风格把这份周报做成 slide         # → 指定风格直接生成
做一个 Tesla 风格的产品发布 deck，导出 pptx # → 生成 + 导出
用 Claude 风格生成 HTML 和 PDF             # → 同时输出 deck.html / PDF
Notion 配色 + Linear 排版，做个路演 PPT    # → 混搭风格
```

## 支持的 62 个品牌风格

Apple · Claude · Cursor · ElevenLabs · Figma · Framer · Lovable · Meta · MiniMax · Mintlify · Mistral · Notion · Ollama · OpenCode · PostHog · Raycast · Replicate · Resend · Runway · Sanity · Sentry · Supabase · Superhuman · Together AI · Vercel · VoltAgent · Warp · Webflow · X.AI · Zapier · Airtable · Cal.com · Clay · ClickHouse · Cohere · Composio · Expo · HashiCorp · IBM · Intercom · Linear · Miro · MongoDB · NVIDIA · Pinterest · Stripe · Binance · Coinbase · Kraken · Revolut · Wise · Airbnb · BMW · Ferrari · Lamborghini · Nike · Renault · Shopify · SpaceX · Spotify · Tesla · Uber

每个品牌的一句话风格与内容匹配标签见 [references/brand-registry.md](references/brand-registry.md)。

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

## 致谢

- [SpaceZephyr/brand-design-md](https://github.com/SpaceZephyr/brand-design-md) — 品牌设计规范获取
- [SpaceZephyr/design-buddy](https://github.com/SpaceZephyr/design-buddy) — space-slide-deck 幻灯片流程
- [getdesign.md](https://getdesign.md) — 品牌 DESIGN.md 数据源
