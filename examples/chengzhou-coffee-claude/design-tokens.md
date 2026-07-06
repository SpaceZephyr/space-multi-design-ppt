# Design Tokens — Claude（来源：getdesign `claude` DESIGN.md）

## 颜色
- 画布 canvas: `#faf9f5`（暖奶油色，禁用纯白）
- 柔和表面 surface-soft: `#f5f0e8`
- 卡片表面 surface-card: `#efe9de`
- 强奶油 surface-cream-strong: `#e8e0d2`
- 深色表面 surface-dark: `#181715`（数据/产品面板）
- 深色浮起 surface-dark-elevated: `#252320`
- 主强调色 primary (coral): `#cc785c`
- 强调按压 primary-active: `#a9583e`
- 辅助琥珀 accent-amber: `#e8a55a`
- 辅助青 accent-teal: `#5db8a6`
- 文字主 ink: `#141413`
- 正文 body: `#3d3d3a`
- 次级 muted: `#6c6a64` / muted-soft: `#8e8b82`
- 边框 hairline: `#e6dfd8` / hairline-soft: `#ebe6df`
- 深底文字 on-dark: `#faf9f5` / on-dark-soft: `#a09d96`
- 白 on-primary: `#ffffff`

## 字体
- 展示标题：Copernicus / Tiempos Headline（不可用）→ 回退 **Cormorant Garamond 500**；中文衬线回退 **Noto Serif SC / Songti SC**
- 正文/标签：StyreneB（不可用）→ 回退 **Inter**；中文回退 **Noto Sans SC / PingFang SC**
- 展示层级（字重一律 400，负字距是品牌关键）：
  - display-xl: 64px / 400 / lh 1.05 / ls -1.5px
  - display-lg: 48px / 400 / lh 1.1 / ls -1px
  - display-md: 36px / 400 / lh 1.15 / ls -0.5px
  - display-sm: 28px / 400 / lh 1.2 / ls -0.3px
- title-md: 18px / 500 / lh 1.4；body-md: 16px / 400 / lh 1.55
- caption: 13px / 500；caption-uppercase: 12px / 500 / ls 1.5px

## 间距与圆角
- 间距：4 / 8 / 12 / 16 / 24 / 32 / 48 / section 96px；卡片内 padding 32px
- 圆角：md 8px（按钮/输入）、lg 12px（内容卡片）、xl 16px（hero 容器）、pill 9999px（徽章）

## 阴影
- 色块优先、几乎无阴影；hover 罕见 `0 1px 3px rgba(20,20,19,0.08)`

## 气质关键词
- 暖奶油画布 + coral 点缀 + 深色数据面板三段式节奏（cream → cream-card → dark 交替）
- 衬线标题 400 字重 + 负字距，编辑级排版，"大字号优先于加粗"
- 装饰母题：Anthropic 四辐射尖芒 ✳ 记号、hairline 细线、coral 全出血 callout 卡

## 幻灯片映射约定
- 封面/封底：cream 画布 + coral callout 元素
- 数据页：surface-dark 面板承载大数字（on-dark 文字）
- 内容卡片：surface-card `#efe9de` + 12px 圆角 + 32px 内边距 + hairline 边框
- coral 只用于强调数字、徽章、CTA，不满屏使用
