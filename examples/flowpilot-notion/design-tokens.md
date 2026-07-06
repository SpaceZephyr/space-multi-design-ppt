# Design Tokens — Notion（来源：getdesign `notion` DESIGN.md）

## 颜色
- 页面画布 canvas-soft: `#f6f5f4`（暖纸白，整页背景，非纯白）
- 卡片/表面 surface: `#ffffff`
- 文字主色 ink: `#000000`（按规范以 ~95% alpha 渲染 → `rgba(0,0,0,0.95)`）
- 文字次级 ink-secondary: `#31302e`；muted: `#615d59`；faint: `#a39e98`
- 结构强调（唯一）primary: `#0075de`（Notion 蓝，只用于 CTA / 链接 / 激活态）
- primary-active: `#005bab`
- 深靛夜幕 secondary: `#213183`（仅用于一处 hero 反色带 → 本 deck 用在封面）
- 贴纸装饰色（仅装饰，不做结构/CTA）：sky `#62aef0`、purple `#d6b6f6`、pink `#ff64c8`、orange `#dd5b00`、teal `#2a9d99`、green `#1aae39`
- 发丝线 hairline: `#e6e6e6`

## 字体
- NotionInter → 回退 `Inter, -apple-system, system-ui, "Segoe UI", Helvetica, Arial`；中文回退 `"PingFang SC", "Noto Sans SC", "Microsoft YaHei"`
- display-1: 64px / 700 / lh 1.0 / ls **-2.125px**
- display-2: 54px / 700 / lh 1.04 / ls -1.875px
- heading-1: 40px / 700 / lh 1.1 / ls -1px
- heading-2: 26px / 700 / lh 1.23 / ls -0.625px
- heading-3: 22px / 700 / lh 1.27 / ls -0.25px
- title: 20px / 600 / lh 1.4 / ls -0.125px
- body-md: 16px / 400 / lh 1.5（中文幻灯片正文放大至 17-18px，行高 1.6-1.7）
- caption: 14px / 400 / lh 1.43
- eyebrow: 12px / 600 / lh 1.33 / ls +0.125px

## 圆角
xs 4px · sm 5px · md 8px · lg 12px（feature card）· xl 16px · full 9999px（营销 pill CTA / 徽章）

## 间距
基础 8px：4 / 8 / 12 / 16 / 24 / 28 / 32；卡片内边距 24px

## 阴影
- Level 0：仅 1px hairline 边框
- Level 1（soft）：`rgba(0,0,0,0.01) 0 0.175px 1.041px, rgba(0,0,0,0.02) 0 0.8px 2.925px, rgba(0,0,0,0.027) 0 2.025px 7.847px, rgba(0,0,0,0.04) 0 4px 18px`
- Level 2：更深五层，末层 `rgba(0,0,0,0.05) 0 23px 52px`

## 气质
暖纸白画布、大留白、发丝线分隔；标题重（700）+ 大负字距，正文 400；唯一结构蓝 + 多彩贴纸点缀（仅装饰）；封面用一次深靛"夜幕"反色。定价 featured 卡用极性反转（黑底白字，rounded 16px）。
