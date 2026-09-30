---
name: tnf-poster-style
description: |
  Generate photo-to-poster work locked to The North Face Japan「LOW CARBON EATING」flat editorial doodle style (BranD). Use when the user asks for a poster/插画/海报 in this TNF style, "北面画风", "同款插画海报", photo-to-illustration poster with consistent line-art + typography + character tone, or asks to extract a theme from a photo and render it as a magazine-style flat doodle poster. Triggers on phrases like: TNF 海报, 北面插画, LOW CARBON EATING 风格, 餐具装世界, flat doodle poster, 照片转插画海报. Do NOT use for photorealistic posters, generic Canva-style layouts, 3D renders, watercolor, or decks/slides (use pptx skills instead).
---

# TNF Poster Style

从照片提取主题，按 TNF「LOW CARBON EATING」编辑插画体系出同调性海报。画风、文案、排版、人物必须同时锁死——只锁插画不锁字级，风格会散。

## Inputs to collect

缺哪项就问哪项，不要齐上：

1. **源材料**：照片路径（可选）或纯主题描述
2. **主张**：海报要说什么（一句话）。没说就从照片推断后向用户确认
3. **文案语言**：中文 / 日文 / 英文 / 中英混（默认中文正文 + 英文大标题）
4. **原型**：A/B/C/D/E。没说默认 A，见 `references/layout-archetypes.md`
5. **品牌元素**：是否保留 THE NORTH FACE logo。没说就**不放 logo**，只留系列眉标

## Procedure

### 1. 读参考（风格锁）
读 `references/style-dna.md`。后续每一步对照其「自检清单」。
原因：色板、线宽、字级、反模式都写死在那里，凭印象生成必漂。

### 2. 从照片提取主题（有照片时）
用图像理解读照片，产出 6 行主题卡：

```
SUBJECT: 画面核心物件/生物/场景（名词）
WORLD:   放进器皿里的「世界」意象（≤4 个元素）
VESSEL:  白盘 / 白碗（二选一）
FIGURE:  小人动作，或「不要人物」
ACCENT:  一个点睛色物体（鲑鱼橙/芥末黄优先）
CLAIM:   海报主张一句话
```

提取规则：
- 照片写实内容要**转译成隐喻**，不要照抄照片写实构图
- 优先套「器皿装世界」母题；照片主题装不进器皿时，改用「小人站在巨大食物/地景上」变体
- 主题平庸（纯产品摆拍）→ 主动提出隐喻方向，让用户选

### 3. 选原型与背景色
读 `references/layout-archetypes.md` 选型；背景色按主题映射：

| 主题 | 背景 |
|---|---|
| 通用 / 封面 | `#EEEDD9` |
| 肉类 / 食物 | `#EED4C5` |
| 植物 / 土壤 / 山野 | `#D4D8C1` |
| 海洋 / 水 / 数据 | `#D1D7E3` |
| 浪费 / 餐桌 / 温情 | `#F0E3C3` |

### 4. 生成插画（锁风格）
读 `references/prompt-templates.md`，按组合公式拼 prompt：

- 风格锁整段原样粘贴，只填主题变量槽
- 带上负面清单
- `image_gen` 尺寸按「尺寸」表；插画**不写字**
- 生成后目检：线是否粗黑均匀、是否平涂、是否出现渐变/文字/多隐喻
- 不合格 → 只改主题变量重试，**不要改风格锁**；连续 3 次不过 → 降级为更简构图（减少 WORLD 元素）

### 5. 写文案
按 `references/prompt-templates.md` §6：

- 英文大标题 1–3 词 ALL CAPS
- 副标 ≤32 字，反问或诗意陈述
- 正文 3–5 句：现象 → 一个数字/事实 → 温和倡议
- 没有真来源就写「内部素材整理」，禁止编造假文献
- 语气自检：删恐吓词

### 6. 排版合成
输出竖版海报（默认 1080×1440）：

- 优先用 HTML/CSS 生成再截图/转 PDF，字体指定：
  - 英文标题：`Helvetica Neue, Arial, sans-serif` Bold
  - 中文：`Noto Sans SC, Source Han Sans SC, sans-serif`
- 或用 Pillow 按 `style-dna.md` §6.3 字级表叠加文字
- 严格保持「巨大标题 + 细小正文」的字级断层，中间不要过渡字级
- 外边距 ≥8% 画幅宽

### 7. 自检交付
对照 `style-dna.md` §9 清单逐条打勾，再把图交给用户。
不过的项要重做，不要带着问题交付。

## Output contract

交付给用户：

1. **成品海报图**（PNG/JPG，1080×1440 或用户指定）
2. **主题卡**（6 行，第 2 步格式）——方便用户核对主题理解
3. **一句话说明**：选了哪个原型、为什么是这个背景色

中间产物（prompt、草稿图）不主动交付。

## Failure handling

| 情况 | 处理 |
|---|---|
| image_gen 连续 3 次风格不符 | 减 WORLD 元素 / 换更简器皿构图；仍失败则回报用户并附失败样张说明卡在哪条规则 |
| 照片糊/看不清 | 先问用户要清晰图或文字描述，不要硬猜主题 |
| 用户要写实/3D/水彩 | 明确本 skill 不匹配，拒绝硬套；可改走 imagegen 通用流程 |
| 用户要在图里烧字 | 说明本体系「图不带字、字走排版层」；若坚持烧字，接受并注明风格偏差 |
| 文案需要真实数据 | 用 websearch 查证；查不到就删数字改写定性表述，禁止编造 |
| image_gen 403 / 会员未开通 | 如实告知用户生成服务不可用；改交付「锁好风格的 prompt 全文 + 排版骨架 + 主题卡」，由用户在可用环境出图 |

## Examples

**Input**：一张雪山照片，「做成北面画风的海报，主题是护雪」

**Process**：
- 主题卡 SUBJECT=雪山雪线 / WORLD=雪山+针叶林+融雪河 / VESSEL=白圆盘 / FIGURE=盘沿小人测量雪线 / ACCENT=鲑鱼橙帐篷 / CLAIM=留住雪线
- 原型 A，背景 `#D4D8C1`
- image_gen 用风格锁 + 主视觉公式
- 标题 `SNOW LINE`，副标「雪线退一寸，山就少一年」，正文 3 句带 1 个定性事实

**Output**：1080×1440 海报 + 主题卡 + 「原型 A / 植物山野用鼠尾草底」

---

## Windows (win32) platform notes

- 路径与合成脚本用 PowerShell；Python 用 `& $env:MIMO_PYTHON`
- 合成示例（Pillow 叠字）：

```powershell
& $env:MIMO_PYTHON -c "from PIL import Image,ImageDraw,ImageFont; im=Image.open('plate.png'); ..."
```

- HTML 海报转图：起本地静态服务后用内置浏览器截图，或 `$env:MIMO_SOFFICE` 不适用时用 Playwright 截屏
