# 生成提示词模板（锁风格用）

调用 image_gen / image_edit 时，**把「风格锁」整段原样带上**，只替换「主题变量」。
禁止改写风格锁措辞——措辞变了画风就会漂。

---

## 1. 风格锁（Style Lock）— 原样粘贴

```
flat editorial doodle illustration, thick uniform black ink outline (marker pen, round caps, closed shapes), pure flat color fills only, no gradients, no shadows, no texture, no noise,
naive Japanese picture-book style for adults, slightly top-down view, no perspective grid,
simple shapes: triangle mountains, blob trees, oval clouds,
white ceramic plate or bowl as the framing device containing a tiny world,
tiny simplified human figure with two-dot eyes, small head, calm pose, outdoor casual clothes,
muted pastel background, limited palette of sage green, olive, dusty peach, cream, cool blue-gray, salmon orange,
clean magazine infographic feel, The North Face Japan editorial style, generous white space,
text-free illustration (no lettering in the image)
```

### 风格锁中文对照（写报告/说明用，不进提示词）
粗黑马克笔均匀勾线、闭合路径、纯平涂无渐变无阴影无纹理；日式成人大人向绘图本；略俯视无透视网格；概括几何形；白瓷盘/碗作画框装着小世界；豆豆眼小人、静姿态、户外休闲装；鼠尾草绿/橄榄/蜜桃/奶油/冷灰蓝/鲑鱼橙的克制色板；干净杂志图解感；大量留白；**画面内不写字**。

---

## 2. 主题变量槽

| 槽 | 说明 | 示例 |
|---|---|---|
| `[SUBJECT]` | 照片提取的核心物件/生物 | `a snow mountain peak` |
| `[VESSEL]` | 承载隐喻的餐具 | `a white ceramic dinner plate` |
| `[WORLD]` | 器皿里装的世界 | `pine forest, a blue river, small farm fields` |
| `[FIGURE]` | 人物动作（可空） | `a tiny person sitting on the plate rim fishing` |
| `[ACCENT]` | 点睛色物体 | `a salmon-orange tent` |

---

## 3. 组合公式

### 3.1 主视觉（原型 A/E）
```
[风格锁],
hero illustration: [VESSEL] containing [WORLD], [FIGURE], [ACCENT],
centered composition on a solid [背景色名] background,
poster illustration, high quality, clean line art
```

### 3.2 照片转主题插画（image_edit 输入照片时）
```
[风格锁],
redraw this photo's subject as: [VESSEL] containing [WORLD] with [FIGURE],
keep the subject identity of the photo ([SUBJECT]),
solid [背景色名] background, text-free illustration
```

### 3.3 数据图解（原型 D）
```
[风格锁],
infographic scene: [WORLD] with bold flat arrows and white number label boxes with black outline,
numbers in salmon orange, same thick black outline style,
solid [背景色名] background, no real text (placeholder boxes only)
```

---

## 4. 背景色名对照（进提示词用英文）

| HEX | 提示词英文 |
|---|---|
| `#EEEDD9` | `cream sage beige background` |
| `#EED4C5` | `dusty peach pink background` |
| `#D4D8C1` | `pale sage green background` |
| `#D1D7E3` | `cool lavender gray background` |
| `#F0E3C3` | `warm sand yellow background` |

---

## 5. 负面清单（negative prompt）

```
gradient, shadow, glow, 3D render, photorealistic, watercolor, oil paint, texture, grain, neon colors, CMYK print, anime cel shading, dramatic action pose, multiple metaphors, text, letters, watermark, logo
```

---

## 6. 文案生成规则（不是图，是排版文案）

1. **英文大标题**：1–3 个词，ALL CAPS。例：`LOW CARBON EATING` / `MEAT` / `SEAFOOD`
2. **副标**：中文（或用户语言）1–2 句，≤ 32 字。反问或诗意陈述，不出现感叹号堆砌
3. **正文**：3–5 句。结构 = 现象 → 一个具体数字/事实 → 温和行动倡议
4. **reference**：`reference:` + 来源机构/报告名。没有真来源就写「内部素材整理」，禁止编造假文献
5. **语气自检**：删掉所有「震撼」「触目惊心」「刻不容缓」「最后的机会」类词

### 标题词库（可直接用或仿写）
- 主题型：MEAT / SEAFOOD / PLANTS / SOIL / FOREST / RIVER / SNOW / TRAIL / CAMP / GEAR
- 主张型：LOW CARBON EATING / EAT FOR THE OUTDOORS / TASTE THE WILD / SMALL PLATE BIG WORLD

---

## 7. 尺寸

| 用途 | 尺寸 |
|---|---|
| 社交竖版海报 | `1024x1536`（生成）→ 画布 1080×1440 |
| 方形 | `1024x1024` |
| 宽横幅 | `1536x1024` |

生成插画时 **不要**在图里写字；文字由排版层叠加，保证字体调性可控。
