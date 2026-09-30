# tnf-poster-style

把照片/主题转成 The North Face 日本线「LOW CARBON EATING」同款平涂编辑插画海报的 MiMo Desktop / MiMoCode skill。画风、文案、排版、人物四层同时锁死，保证调性一致。

## 风格锚点

> 粗黑线平涂涂鸦 + 餐具盛放世界 + 冷静编辑排版

源自 BranD 杂志转载的 TNF 日本线环保内容系列：

- **插画**：马克笔均匀勾线、纯平涂、零渐变零阴影
- **母题**：白瓷盘/碗里装着山、海、土层、牧场——「餐桌连着户外」
- **人物**：豆豆眼小人，1:6 头身，静姿态，户外休闲装
- **排版**：巨大 ALL CAPS 英文标题紧挨细小正文，中间无过渡字级
- **色板**：5 个低饱和纸面背景色 + 13 色插画平涂色，全部锁定 HEX

## 安装

复制本仓库到 skill 目录（目录名 = skill ID）：

```powershell
# 全局（推荐，跨项目可用）
Copy-Item -Recurse . "$env:USERPROFILE\.config\mimocode\skills\tnf-poster-style"
```

新会话自动被扫描发现，无需注册。触发语句示例：

- 「用北面画风把这张照片做成海报」
- 「LOW CARBON EATING 风格」「餐具装世界」
- 「TNF 海报」「同款插画海报」「照片转插画海报」

不适用于：写实/3D/水彩海报、幻灯片（走 pptx skill）。

## 仓库结构

```
SKILL.md                     # 主流程：主题提取 → 锁风格生成 → 排版 → 自检
references/
  style-dna.md               # 画风锁死规范：线宽/色板/字级/反模式
  combinations.md            # 搭配库：配色配方 F1–F7 × 人物 P0–P6 × 母题 M1–M9
  layout-archetypes.md       # 版式原型 A–E
  prompt-templates.md        # Style Lock 提示词模板 + 文案语气规则
locales/                     # 插件页显示元数据
```

## 流程概览

1. 读 `references/style-dna.md` 锁画风
2. 从照片提取 6 行主题卡（SUBJECT / WORLD / VESSEL / FIGURE / ACCENT / CLAIM）
3. 选版式原型与背景色
4. 按 `references/prompt-templates.md` 粘贴 Style Lock 生成插画（图里不写字）
5. 按字级表排版合成
6. 对照 8 条自检清单验收

## License

供个人学习与非商业使用。原始风格参考 The North Face × BranD 视觉，版权归属原作者。
