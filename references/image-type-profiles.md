# 图片类型拆解规则

先把当前图片归入一个主导 `imageType`，再选择对应的公开拆解字段和 prompt 顺序。

这些 profile 只定义观察顺序和表达方式，不定义任何图片事实。每个具体细节必须来自当前图片或当前校准材料。

需要机器记录时也使用中文字段：

```text
图像类型 / 结构拆解 / 参考色卡 / 完整提示词 / 可选变体提示词
```

不要把同一套公开字段强行套到所有图片上。

## Routing

1. Decide `imageType.key`:

```text
photographic_portrait
anime_illustration
poster_design
commercial_product
product_still
space_landscape
ui_infographic
mixed_other
```

2. Choose the matching profile below. There is no external mother template.
3. Use only sections that help reproduce the current image. Render every evidence-backed section as its own public heading, in the profile order; do not collapse them into a generic breakdown list. Add `画面元素` only when props, text, or graphic components need a separate inventory.
4. 默认用中文人类可读区块展示。只有用户明确要求时才显示原始 JSON。
5. If the image combines categories, use the dominant profile and borrow 1-3 necessary sections from the secondary profile.
6. If a real-person fashion photograph also has obvious poster/magazine typography, logo placement, right-side or bottom layout blocks, or brand campaign structure, use the **Fashion Poster Portrait** hybrid profile below. Internally keep the key as `mixed_other` or `poster_design` depending layout dominance; publicly label it as `真人摄影时尚海报` when appropriate.
7. If any image type behaves like a poster, cover, magazine visual, music promo, or graphic layout, include the visible control fields that matter for the image, especially `主体可见性`, `局部视觉焦点`, `清晰度/遮挡地图`, `版式结构地图`, `图形元素功能`, `生成优先级`, and `失败风险`.
8. Ignore platform UI, creator marks, account numbers, app watermarks, or source overlays for routing. They should be omitted from the prompt and do not turn a portrait into a poster or layout profile.

## Evidence Gate

Profiles define candidate fields and wording style only. They do not define facts to insert.

Rules:

- Only output a section value when the current image visibly supports it or it is strongly inferable from composition, light, material, or perspective.
- Do not copy example values from previous samples into unrelated images.
- Do not force camera focal length, social-platform style, crop, compression, texture, body pose, facial occlusion, typography, or failure risks unless the current image actually shows them.
- If a profile suggests a field but the current image has no evidence for it, omit that field or write a narrower factual description.
- Color palette ratios must follow the current image's visible color distribution, not a previous sample.
- Do not create or refine an image-type profile from a single original image alone. A calibration update needs the current skill output, generated return image(s), exact generation settings, and user feedback or a clear visual target. Without that evidence, only update routing or process guards.

## Photographic Portrait

Use for real-person portraits, selfies, fashion/lifestyle photos, editorial photography.

Preferred public sections. Every evidence-backed section is required in the public output and must keep this order:

```text
图像类型
风格参考线索
风格/滤镜
摄影/构图
主体人物
身形轮廓
肤色/肤调
动作/姿态
微表情/情绪
造型
服装贴合度
服装材质
皮肤/光泽细节
场景/背景
光线/色彩
成像质感
成像签名
参考色卡
```

Rules:

- Do not force anime face fields.
- Fold eye/lip/brow details into `主体人物`, `微表情/情绪`, `造型`, and `皮肤/光泽细节`.
- Mention face shape only if it materially affects the generation.
- Use photography words only when supported: lens/crop, camera angle, direct flash, window light, film/CCD/phone flash, grain, overexposure, haze, compression.
- For close-up beauty, makeup, cosplay-adjacent, doll-like, or role-characterized real-person portraits, keep `imageType.key=photographic_portrait` unless the image is actually illustrated. Public labels may say `写实真人角色化人像摄影` when the styling visibly borrows anime/COS/doll language, but do not route it to `anime_illustration`.
- For close-up beauty, makeup, or styling portraits, describe the visible framing controls instead of only saying `近景`: aspect ratio, near-square / vertical / horizontal frame, bust or head-shoulder crop, camera height, whether it is straight-on or slightly low/high, approximate subject occupancy, head placement, arm/shoulder diagonal, and clean background negative space when supported.
- The `图像类型` line should combine visible aspect ratio, photographic subtype / subject class, and confidence, for example `2:3 竖幅写实人像摄影，真实人物近景肖像，置信度很高`. Do not state exact dimensions when only the ratio is visible.
- Approximate focal-length language such as `约 70–85mm 中长焦感` is allowed only when perspective compression, facial proportions, framing, and depth of field support it. Describe it as a visual impression, never as camera metadata.
- Preserve a visible sharpness hierarchy: identify what is sharpest, what has medium detail, and what progressively softens. Do not flatten local facial sharpness plus highlight bloom into either `全局锐利` or `整体朦胧`.
- When exposure, color temperature, beautification, highlight diffusion, grain, compression, or local softness forms a distinctive photographic signature, read `imaging-signature-taxonomy.md` before writing `风格/滤镜`, `肤色/肤调`, `光线/色彩`, `成像质感`, or `成像签名`.
- Keep `肤色/肤调` for inherent skin appearance, `光线/色彩` for illumination, `成像质感` for capture/render surface, and `风格/滤镜` plus `成像签名` for the selected compound imaging signature. Do not resolve apparent conflicts by deleting one layer.
- If a compound imaging term is selected, place the canonical term first in `风格/滤镜`, expand its visible mechanics in `成像签名`, and put both the term and its shortest executable expansion near the beginning of the final prompt.
- For gaze and expression, determine gaze only from iris/pupil placement inside the eyelid opening, not from face direction, mood, nearby objects, or an inferred narrative. Express horizontal gaze only as image-left / image-right in the viewer's canvas frame; do not introduce subject-left / subject-right. Use visible sclera distribution as a cross-check: when the iris shifts toward image-right, more sclera is usually exposed on its image-left side, and vice versa. Only after the canvas direction is established may a visible object in that direction be described as a possible gaze target.
- For lip micro-expressions, separate mouth opening, lip asymmetry, teeth, tongue, and mood labels. If a small tongue tip or tongue surface is visibly caught between slightly parted lips, describe it as `舌尖微露` / `tiny tongue peek` with a narrow lip gap, no teeth, and not an exaggerated tongue-out face. If the shape is uncertain, mark it as possible lip-gap shadow instead of asserting a tongue.
- When a generated return image loses expression vitality compared with the original, strengthen only observable expression mechanics: iris offset, catchlight size/placement, upper-eyelid pressure, lower-eyelid tension, brow softness or lift, cheek/nose blush intensity, mouth asymmetry, lip compression, and the hand/lip contact point. Avoid vague fixes such as `更有神`, `更灵动`, or `更丰富表情` unless they are immediately grounded in these visible controls.
- For hand-to-mouth, hand-to-face, or prop-near-face portraits, state the hand/lip/face relationship and visible jewelry or occlusion because generation easily drifts into a different gesture. If finger, nail, straw, cigarette, prop, or fabric visibly presses the lip or cheek, describe the exact contact point and micro-deformation: indentation, lip contour interruption, compressed lower/upper lip edge, narrowed mouth gap, shifted highlight, or skin/lip pressure. If there is no visible pressure, describe it as hovering or light touch instead.
- For hand-to-face portraits, specify which visible fingers are straight or bent, their destination relative to the eye, nose, lips, cheek, or jaw, whether the palm bears weight, and what the other hand does. `托脸` alone is not enough when the gesture is visually distinctive.
- For elaborate hair, headdress, jewelry, or layered costume, describe first the large silhouette and occupied frame region, then attachment paths and repeated element families, then small materials/colors. A list of accessory nouns without placement is insufficient.
- For full-body studio fashion portraits, describe only the visible subset: `竖幅 9:16`, `全身构图`, `低机位仰拍`, approximate `28-35mm 广角感`, top negative space, bottom foot crop, leg-lengthening perspective, or social story/Pin-image feeling. Do not include any of these just because the profile matched.
- For automotive fashion portraits, when a car/motorcycle/vehicle visibly co-dominates the frame with the model, keep the photographic portrait profile unless the product clearly dominates. Describe the vehicle as a co-main visual: body position on/near the vehicle, car front/side/wheel/headlight shapes, paint/metal reflections, leg/body diagonals against vehicle geometry, and fashion-advertising mood. Do not invent a vehicle brand or model.
- If clothing, hands, hair, or props hide the mouth or lower face, describe visible facial zones and occlusion explicitly instead of inventing a full expression.
- For soft-beauty social-media portraits, mention `柔焦美颜`, `手机压缩`, `背景压缩色块`, or `人物边缘略软` only when the current image shows those artifacts; avoid over-sharpening language unless the image is truly crisp commercial photography.
- For multi-person fashion portraits or editorial poses, describe each person by stable visual role before describing clothing, and preserve visible overlap, support points, foreground/background order, and face/hand/foot anchors in natural language.
- When the current image has fragile generation constraints, the final prompt may end with a compact `避免...` clause instead of a separate negative-prompt list. For real-person styling portraits, common evidence-triggered risks include anime/illustration drift, ordinary clean avatar drift, over-clean commercial studio retouch, lost side gaze, exaggerated smile, direct gaze, lost hand-to-mouth relationship, or lost accessory structure.
- For photographic portraits, prompt order is:

```text
成像签名 + photographic medium / realism
→ aspect ratio, crop, camera height, approximate lens impression, subject occupancy
→ face, skin tone, gaze and expression mechanics
→ exact gesture/contact/occlusion and body orientation
→ large hair/accessory silhouette, then accessory families and placement
→ garment structure, fit and material contrast
→ key-light direction, falloff, background separation and color system
→ sharpness hierarchy, skin/rendering texture
→ compact current-image failure guard
→ signature requirement when applicable
```

- When a portrait combines a fragile gesture with elaborate hair/accessories, generation priority is: face visibility and gaze, exact gesture/contact, framing and large head silhouette, garment silhouette, lighting, then small ornaments. Put the same priority into prompt order.

## Anime Illustration

Use for anime, manga, game character art, stylized 2D characters, semi-anime illustrations.

Preferred public sections:

```text
图像类型
风格参考线索
脸部风格锁定
脸型/面部线条
眼型/瞳孔设计
眉形/眼神压力
嘴唇/口红
脸部负面约束
身形轮廓
肤色/肤调
动作/姿态
微表情/情绪
服装贴合度
服装材质
皮肤/头发高光
色卡
成像质感
场景/世界观
服装/道具
色彩/光影
知名角色判断
角色设计
画风/线稿
分镜/构图
局部视觉焦点
清晰度/遮挡地图
图形元素功能
失败风险
生成时参考色卡
提示词
```

Rules:

- This is the only default profile that must expand all face-specific fields.
- For anime character poster / game character art, prefer illustration-native labels such as `场景/世界观`, `服装/道具`, `色彩/光影`, `角色设计`, `画风/线稿`, and `分镜/构图` instead of photographic labels such as `摄影/构图`, `主体人物`, `造型`, `场景/背景`, and `光线/色彩`, unless the current image is intentionally mimicking photography.
- For anime close-up face posters with guofeng / ink / seal / calligraphy / rice-paper evidence, explicitly preserve the hybrid medium identity: `现代国风动漫插画`, `半厚涂与水墨线描融合`, `宣纸底`, `黑色乱发线条`, `橙红印章点缀`. Do not collapse these into generic `日系暗黑角色海报`.
- If the anime image is also a poster/cover, keep the anime face fields and add only the poster-control fields supported by the image. For example, an extreme face close-up with hair crossing the eye needs `局部视觉焦点` and `清晰度/遮挡地图`; calligraphy, seals, frames, scan windows, or typography need `图形元素功能` and possibly `版式结构地图`.
- `脸部风格锁定` should define face archetype, maturity, stylization level, and whether it is non-moe / mature / sharp / soft.
- `眼型/瞳孔设计` should include eye shape, pupil size, highlights, upper eyelid, lower lash, eye-tail pressure.
- `脸部负面约束` is required when avoiding drift matters, especially to prevent unwanted moe, galgame, childlike, over-cute, web-influencer, or overly glossy eye styles.
- `皮肤/头发高光` should be used when anime skin lighting, hair specular highlights, rim light, or cel/high-paint highlights matter more than photographic skin texture.
- Use `场景/世界观` when the image depends on setting genre, fantasy motifs, night city, sci-fi, battle, school, concert, vehicle, or other world-building context.
- Use `服装/道具` to inventory visible outfit pieces, props, weapons, vehicles, wings, tails, accessories, or mechanical objects that shape the character design.
- Use `知名角色判断` only as a cautious visual judgment: if stable IP markers are visible, mention the likely source; if not, say it is not clearly identifiable and appears closer to original / fan character design. Do not invent an IP.
- Use `角色设计` for hair structure, silhouette motifs, fantasy traits, color blocks, outfit concept, and recurring design anchors.
- Use `画风/线稿` for line quality, cel-shading, semi-thick paint, brush/rendering mix, mechanical illustration precision, and detail density.
- Use `分镜/构图` for illustration framing, low/high angle, near-full-body crop, character-to-prop layout, diagonals, S-curves, perspective, and visual flow.
- For extreme face close-ups, do not invent a full body, outfit, or scene. State that clothing is mostly absent / unclear when only head, neck, hair, and graphic marks are visible.
- For anime images with motorcycles, cars, weapons, mecha, or large props, keep the anime illustration profile when the character remains the main visual. Describe the prop in `服装/道具`, `场景/世界观`, `画风/线稿`, and `分镜/构图`; do not switch to photographic automotive/profile rules unless the image is actually a real photo.
- For anime or stylized images with complex action, multiple characters, fight choreography, inverted bodies, large props, or extreme foreshortening, describe visible character count, foreground/background order, limb ownership, contact and occlusion directly in the structure words and final prompt.
- `风格/滤镜`, `摄影/构图`, `主体人物`, `造型`, `场景/背景`, and `光线/色彩` remain valid fallback labels for simpler anime outputs, but they should not replace the anime-native sections when those sections fit better.
- Prompt order should put face style before body and clothing.

## Poster Design

Use for posters, magazine covers, graphic layouts, title cards, social cards, editorial collages.

Preferred public sections:

```text
图像类型
风格参考线索
风格/滤镜
版式/构图
主体/主视觉
主体可见性
局部视觉焦点
清晰度/遮挡地图
版式结构地图
图形元素功能
生成优先级
失败风险
文字/信息层级
图形元素
材质/印刷质感
场景/背景
光线/色彩
色卡
成像质感
```

Rules:

- Focus on hierarchy, typography placement, margins, grid, title/subtitle relationship, stickers, frames, paper/print texture.
- Treat poster reverse as generation control, not inventory. Explain why each visual element exists: guide the eye, mask/occlude, create local clarity, carry text hierarchy, frame the subject, add texture, or prevent failure.
- `版式结构地图` should include aspect ratio, title/main/info/edge-note zones, approximate positions/ratios, alignment, whitespace, overlaps, layer order, and reading path when visible.
- `清晰度/遮挡地图` is required for frosted glass, scan layers, low-res compression, translucent masks, ghosted figures, local sharpening windows, or partial features.
- `失败风险` should name short generation guardrails only when visible risks exist, such as text becoming dominant, subject disappearing, wrong clear/blur zones, lost window/frame function, or broken face/hand relationship.
- If text exists, describe its layout and visual weight. Do not invent exact words unless the user asks to preserve text.
- Do not use portrait body/face sections unless the poster's main visual is a person and those details affect generation.

## Fashion Poster Portrait

Use for real-person fashion posters, magazine inside pages, lookbook layouts, social-media campaign posters, or brand/ambassador pages where a photographed person is the main visual and typography/layout remains important.

Use these stable Chinese public field names in this order. Never expose English internal keys, underscores, or bilingual headings:

```text
图像类型
风格参考线索
品牌气质
清晰度/遮挡地图
色彩系统
构图节奏
失败风险
视觉焦点
生成优先级
图形元素功能
主视觉
图层顺序
版式层级
版式结构地图
印刷/材质质感
人物表情/动作关系
主体可见性
字体/文字系统
视觉权重
可直接复制的完整提示词
```

Rules:

- Use this profile when typography is small but structurally meaningful, especially right-side title/info blocks, bottom logos, brand labels, or magazine-page white/negative space.
- Keep the person as the first-order visual if they dominate the image; describe typography as supporting layout unless it visually overwhelms the person.
- `品牌气质` defines the audience-facing cultural mood, era signal, editorial attitude, and emotional energy; do not invent a real brand.
- `清晰度/遮挡地图` states which facial zones, limbs, props, background, and typography are sharp, soft, grain-covered, or occluded. Distinguish print grain from global fog.
- `色彩系统` assigns background, skin, dark anchor, high-saturation control color, and lightening color by role rather than listing swatches.
- `构图节奏` explains stable axes, arm/body arcs, top-middle-bottom density, deliberate asymmetry, and the reading rhythm created by crop and overlap.
- `失败风险` lists only current fragile structures: expression direction, prop/hand relation, text occlusion, small-label scale, background identity, print texture, or other visible risks.
- `视觉焦点` ranks first through fourth visual focus when the hierarchy is visible.
- `生成优先级` separates level-one identity/action/layout constraints, level-two environment/style/crop constraints, and level-three replaceable low-weight editorial details.
- `图形元素功能` names each non-text or micro-information element and states its balancing, indexing, framing, or rhythm function.
- `主视觉` is a compact identity statement for the photographed person, framing, signature pose/prop relation, hair/skin anchor, and dominant position.
- `图层顺序` explicitly lists bottom-to-top layers. Separate environment, photographed subject, foreground limbs/props, solid typography, micro-editorial marks, and global print texture when present.
- `版式层级` states primary, secondary, and tertiary information groups and the grid logic.
- `版式结构地图` divides the canvas into approximate zones or percentages and gives the reading path. Use real image dimensions for the aspect ratio when available.
- `印刷/材质质感` describes grain, color noise, scan texture, compression, halftone, ink edge, bleed, or dark-area color penetration without turning them into global blur.
- `人物表情/动作关系` combines visible gaze mechanics, eyelid pressure, mouth opening/teeth, mood, and the relation of hands or props to the face.
- `主体可见性` records visible body zones, edge crops, prop/hand occlusion, and exactly where typography may overlap without hiding identity-critical features.
- `字体/文字系统` describes color, type class, weight, tracking, scale range, crop, offset, overlap, and function. Default to layout semantics instead of copying exact words; preserve exact text only when the user explicitly asks or the wording itself is the main subject.
- `视觉权重` estimates the share of the photographed subject, key prop/gesture, typography, environment, and micro-marks. Use a small set of percentages that total approximately 100%.
- Do not add a separate `参考色卡` or `成像签名` to this profile by default. `色彩系统` and `印刷/材质质感` carry those controls; add a separate palette only when requested.
- For a close portrait, use `近距离广角肖像` when nearby arms, hands, shoes, props, or edge geometry visibly expand relative to the face and increase spatial tension. Do not replace this with a standard/mid-telephoto focal estimate merely because the face is close.
- The final prompt should read like a generation control prompt for a fashion poster, not like a pure portrait prompt. It may include a compact negative or failure-avoidance sentence when the current image has a clear risk.
- Fashion poster prompt order:

```text
photographic key visual + era/editorial style + print material
→ subject identity, framing, visual weight, inherent skin and visible highlight treatment
→ poster expression and gaze mechanics
→ exact limb/hand/prop relation
→ hair, visible garment and fit
→ environment, clarity boundary and subject visibility
→ ranked visual weight and generation priority
→ top/middle/bottom layout map and typography behavior
→ bottom-to-top 图层顺序 and reading path
→ low-weight graphic elements
→ current 失败风险
→ signature requirement when applicable
```

## Commercial Product

Use for ads, product campaign imagery, product with model, packaging hero shots, branded commercial scenes.

Preferred public sections:

```text
图像类型
风格参考线索
风格/滤镜
摄影/构图
产品主体
产品形态/结构
材质/表面反应
使用场景/商业语境
道具/辅助元素
光线/色彩
色卡
成像质感
```

Rules:

- Prioritize product silhouette, material, reflection, packaging structure, label area, prop relation, commercial lighting.
- Avoid brand names and source marks unless the user explicitly asks to preserve them.
- If a person appears, describe them only as part of product context unless they dominate the frame.

## Product Still

Use for clean still life, catalog product photos, isolated objects, tabletop compositions.

Preferred public sections:

```text
图像类型
风格参考线索
风格/滤镜
摄影/构图
主体物件
形态/结构
材质/表面反应
摆放关系
场景/背景
光线/色彩
色卡
成像质感
```

Rules:

- Focus on object geometry, surface, shadow, reflection, table/background, lens angle, depth of field.
- Do not introduce people or narrative unless visible.

## Space Landscape

Use for landscapes, cityscapes, natural scenery, space scenes, abstract environmental vistas.

Preferred public sections:

```text
图像类型
风格参考线索
风格/滤镜
构图/空间层次
主体环境
尺度/景深
地貌/建筑/天体结构
氛围/天气/粒子
光线/色彩
色卡
成像质感
```

Rules:

- Focus on spatial depth, horizon, foreground/midground/background, atmosphere, weather, light direction, scale cues.
- Do not use portrait or product sections.

## UI Infographic

Use for UI screenshots, dashboards, diagrams, information graphics, charts, app/web layouts.

Preferred public sections:

```text
图像类型
风格参考线索
版式/信息结构
主界面/主体图表
组件层级
文字/标签系统
图标/图形元素
交互状态/数据表达
光线/色彩
色卡
成像质感
```

Rules:

- Prioritize layout, grid, information hierarchy, component style, chart type, label density, icon style.
- Do not invent readable copy; describe text blocks and hierarchy unless the user provides exact text.

## Mixed Other

Use when no single category dominates.

Preferred public sections:

```text
图像类型
风格参考线索
风格/滤镜
构图
主体
关键元素
材质/质感
场景/背景
光线/色彩
色卡
成像质感
```

Rules:

- Borrow only the sections needed from the closest primary profile.
- Keep the output concise and factual.
