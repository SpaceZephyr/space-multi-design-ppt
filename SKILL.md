---
name: space-design-slide-codex
description: 品牌设计风格驱动的幻灯片生成器。将用户内容智能匹配到 62 个顶级品牌设计系统（Apple、Notion、Claude、Stripe、Linear、Tesla 等），拉取真实品牌设计规范（DESIGN.md）后生成像素级还原品牌风格的 HTML 幻灯片，可导出 PPTX/PDF。用户要求"做 PPT"、"做个 slide"、"生成演示文稿"、"design slide"、"用 XX 风格做幻灯片"、"把这篇文章做成 deck"、提到 presentation/keynote/路演/汇报材料，或发来一段内容希望变成幻灯片时，都应使用本 skill——即使用户没有提到"品牌"或"设计风格"。
---

# Space Design Slide Codex

把任意内容变成带顶级品牌设计语言的幻灯片。核心思路：不靠凭空发挥的"好看"，而是通过 getdesign.md 拉取 62 个真实品牌的精确设计规范（颜色、字体、间距、圆角、阴影的具体数值），用这些 token 驱动 HTML 幻灯片渲染，保证风格可信且一致。

## 工作流总览

```
进度清单（逐项勾选）：
- [ ] Step 1: 接收并分析内容
- [ ] Step 2: 风格决策（用户指定 → 直接用；未指定 → 5+1 推荐）⚠️ 必须
- [ ] Step 3: 拉取品牌 DESIGN.md 并提取设计 token
- [ ] Step 4: 生成大纲（简短确认）
- [ ] Step 5: 逐页生成 HTML 幻灯片
- [ ] Step 6: 合成单文件 deck.html（默认交付物）
- [ ] Step 7: 按需导出 PPTX / PDF
- [ ] Step 8: 交付与总结
```

**语言规则**：所有与用户的交流、幻灯片文案语言跟随用户输入语言（用户中文则全中文，技术名词和品牌名保留英文）。

## Step 1: 接收并分析内容

内容可能是：粘贴的文字、文件（md/docx/pdf/txt）、或一个主题（"帮我做一个关于 XX 的 PPT"）。

1. 若是文件，读取内容；若只是主题，先与用户确认要点或自行调研补全内容
2. 分析内容，得出：
   - **核心信息**（一句话）与 3-5 个支撑点
   - **受众**（高管/技术/大众/投资人/学习者）
   - **内容信号**（用于风格匹配，见 Step 2）
   - **建议页数**：<1000 字 → 5-8 页；1000-3000 字 → 8-15 页；>3000 字 → 12-20 页
3. 深度分析方法见 `references/outline-guide.md`（信息层级、受众适配、视觉机会点）

## Step 2: 风格决策 ⚠️ 必须

### 情况 A：用户已指定风格 → 直接用，跳过推荐

用户说"用 Stripe 风格"、"做成苹果的感觉"、"Notion 那种"时，对照 `references/brand-registry.md` 找到 slug，直接进入 Step 3。支持混搭（"Notion 配色 + Linear 排版"→ 两个 slug 都拉取）。

### 情况 B：用户未指定 → 展示 5+1 推荐

根据 Step 1 的内容信号，从 `references/brand-registry.md` 的匹配标签中选出 **5 个与内容最匹配的品牌风格**，在聊天中展示给用户（每个一句话介绍），并附上第 6 项「智能匹配」：

```
根据你的内容，我推荐以下设计风格：

1. **Stripe** — 紫色渐变 + 300 字重优雅排版，金融科技质感
2. **Linear** — 超级极简 + 精准间距 + 紫色点缀，效率工具气质
3. **Vercel** — 黑白精准 + Geist 字体，开发者极简美学
4. **Notion** — 暖色极简 + 衬线标题，柔和知识感
5. **Claude** — 赭石强调色 + 编辑级排版，温暖智识感

6. **智能匹配** — 我根据内容气质直接选择最合适的风格（含混搭）

回复编号或品牌名即可，也可以直接说其他品牌（共支持 62 个）。
```

要求：
- 5 个推荐必须**真的和内容匹配**（科技产品内容别推 Ferrari，儿童教育内容别推 Binance），依据 registry 中每个品牌的匹配标签
- 一句话介绍用 registry 中的风格描述，突出"选它会得到什么视觉效果"
- 用户选「智能匹配」时，选出最贴合的 1 个品牌（或 2 个混搭），**告知用户选了什么及理由**再继续
- 保持推荐有新鲜感：匹配度接近时可轮换，不要每次都推同样 5 个

## Step 3: 拉取 DESIGN.md 并提取 token

```bash
mkdir -p /tmp/design-md-tmp/<slug> && cd /tmp/design-md-tmp/<slug> && npx -y getdesign@latest add <slug> 2>&1
cat /tmp/design-md-tmp/<slug>/DESIGN.md
```

从 DESIGN.md 提取并记录（建议写入工作目录 `design-tokens.md` 备查）：

- **颜色**：背景 / 表面 / 文字主次 / 强调色 / 边框
- **字体**：font-family、字号层级、字重、行高、字间距（若品牌字体不可用，注明最接近的 Google Fonts / 系统字体回退）
- **间距与圆角**：基础单位、组件 radius
- **阴影**：各层级 box-shadow
- **气质关键词**：留白程度、对比强度、装饰倾向

**严格执行规范里的具体数值**——规范写 `rgba(0,0,0,0.95)` 就不要写 `#000`，字间距 `-2.125px` 就不要四舍五入。这是本 skill 与"随手做个好看 PPT"的本质区别。

混搭时：以主品牌为骨架，从副品牌提取指定维度（颜色/排版/布局）融合，并在 deck 注释中说明来源。

**降级**：npx 失败（无网络/无 Node）时，使用 `references/brand-registry.md` 中该品牌的风格描述作为设计方向，告知用户这是近似还原。

## Step 4: 生成大纲

按 `references/outline-guide.md` 生成 `outline.md`：封面 + 内容页 + 封底，每页标注：标题（叙事式，讲结论不贴标签）、要点、布局类型、视觉元素。

把大纲**简要**展示给用户确认（不用逐字，列出页码+每页标题即可）。用户没意见或说"直接来"就继续；已经确认过一次流程的老用户可跳过。

## Step 5: 逐页生成 HTML 幻灯片

输出目录结构：

```
design-slide/{topic-slug}/
├── source.md            # 原始内容
├── design-tokens.md     # 提取的品牌 token
├── outline.md
├── slides/
│   ├── 01-cover.html
│   ├── 02-{slug}.html ...
├── deck.html            # 单文件整合（默认交付物）
├── {topic-slug}.pptx    # 按需
└── {topic-slug}.pdf     # 按需
```

每页是独立的 1280×720 HTML。制作规范（尺寸、防溢出、布局模板、token 应用方式）详见 `references/slide-html-guide.md`——**生成第一页前必读**。

内容质量规则（详见 outline-guide）：
- 每页只讲一个观点；标题叙事化（"用量 6 个月翻倍"而非"关键数据"）
- 数据标注来源；禁用占位符；禁 AI 套话（"让我们一起探索"之类）
- 封底不是"谢谢观看"，要有行动号召或记忆点

## Step 6: 合成 deck.html

所有单页完成后，运行合成脚本把 slides/ 打包成带键盘翻页、全屏演示、页码指示的单文件 deck：

```bash
python3 <SKILL_DIR>/scripts/build_deck.py design-slide/{topic-slug}/slides --output design-slide/{topic-slug}/deck.html --title "标题"
```

deck.html 支持：←/→/空格翻页、F 全屏、G 网格总览、URL hash 定位页码。

## Step 7: 按需导出 PPTX / PDF

用户要 pptx 或 pdf 时：

```bash
pip install playwright python-pptx img2pdf --break-system-packages 2>/dev/null; python3 -m playwright install chromium 2>/dev/null
python3 <SKILL_DIR>/scripts/export_deck.py design-slide/{topic-slug}/slides --pptx design-slide/{topic-slug}/{topic-slug}.pptx
python3 <SKILL_DIR>/scripts/export_deck.py design-slide/{topic-slug}/slides --pdf design-slide/{topic-slug}/{topic-slug}.pdf
```

原理：Chromium 无头截图每页 HTML（2x 分辨率）→ 全幅贴入 16:9 PPTX / 合成 PDF。若 playwright 不可用，告知用户并交付 deck.html（浏览器里"打印为 PDF"也是可行方案）。

## Step 8: 交付

展示 deck.html（及导出文件），总结：使用的品牌风格及关键 token、页数、如何演示（打开 deck.html 按 F 全屏）。询问是否需要：调整个别页（直接改对应 slides/NN-*.html 后重跑 build_deck）、换风格重渲染（token 换掉、结构复用）、导出 PPTX/PDF。

## 可选：AI 图像模式

用户明确要"插画感/手绘感的图片幻灯片"且环境有 `LABNANA_API_KEY` 时，走图像生成管线（每页由 GPT-image-2 渲染为图片）：见 `references/image-mode.md`。默认**不**走此模式——HTML 模式文字精准、无需 API key、可编辑。

## 错误处理速查

| 问题 | 处理 |
|---|---|
| npx getdesign 失败 | 用 registry 风格描述近似还原，告知用户 |
| 品牌不在 62 个之内 | 列出最接近的 3 个替代品牌让用户选 |
| playwright 装不上 | 交付 deck.html，建议浏览器打印导出 PDF |
| 内容太长（>5000 字） | 建议拆成多个 deck 或聚焦一条主线 |
| 品牌字体无法加载 | 用 registry/DESIGN.md 中的回退字体，注释说明 |
