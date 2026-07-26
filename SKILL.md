---
name: nuyoah-image-reverse-prompt
description: Use when the user provides a reference image and asks to 图片反推、画面解构、提取结构词、分析构图色彩材质、反推可直接生图的中文提示词，明确要求通过生成返图来校准本 Skill，或明确要求检查、更新“南鸢图片反推 Skill”本身。普通调用只交付结构拆解、参考色卡和可复制 prompt；不用于跳过分析直接生图、普通图片编辑或无参考图的通用提示词写作。
license: MIT
metadata:
  author: "南鸢 nuyoah"
  version: "0.1.0"
  homepage: "https://knowledge.nuyoahonline.com/skills/nuyoah-image-reverse-prompt"
  source: "https://github.com/nuyoah-ai-works/nuyoah-image-reverse-prompt"
---

# 南鸢图片反推

把参考图转译成可理解、可复用、可直接生成的视觉语言。普通用户不需要选择模式。

## 普通调用

1. 只使用当前图片、当前请求和本 Skill 的参考文件。当前图片是可访问本地文件时，先读取真实宽高并计算最简画幅比例；无法取得尺寸时才视觉估算。不要从旧对话、记忆、Eagle 历史或其他图片补全细节。
2. 先判断主导图片类型，再读取 [图片类型拆解规则](references/image-type-profiles.md)。混合图片选择一个主类型，只借用必要的次级字段。
3. 只写可见或由光线、材质、透视明确支持的事实；不确定的内容省略或标成不确定。
4. 图片存在明显曝光、色温、美颜、颗粒、柔焦、压缩或渲染签名时，读取 [成像签名与复合术语](references/imaging-signature-taxonomy.md)：先分离固有属性、光线、曝光、后期/渲染，再由证据归纳受控复合术语。
5. 按 [输出与提示词合同](references/reverse-output-contract.md) 逐项展示类型规则中有画面证据的字段和完整中文提示词；只有对应类型需要独立色卡时才输出 4–6 个参考色。不得把多个字段压缩成一个笼统的“画面结构拆解”列表。
6. 默认用中文人类可读区块展示，所有公开字段名和区块标题必须是中文，不得展示英文键、拼音、下划线字段或中英并列标题。只有用户明确要求机器记录时才输出结构化数据。
7. 按输出合同中的“画面结构到提示词的映射”重组完整提示词，不把字段原文机械拼接；再执行字段覆盖与层级冲突审计：每个会改变生成结果的已展示字段和已选复合术语都必须进入完整提示词，完整提示词不得新增无证据事实，也不得把固有属性、光线、曝光和后期处理混为一层。

## 默认交付

```text
图像类型
...

[按图片类型选择的公开字段逐项展开]
风格参考线索
...

摄影/构图
...

主体人物
...

动作/姿态
...

光线/色彩
...

成像质感
...

成像签名（仅在对应类型需要且独立渲染特征确实影响复现时）
...

参考色卡（仅在 profile 需要时）
- #HEX｜作用｜大致占比

可直接复制的完整提示词
...
```

默认采用高信息密度：每个有证据的字段独立成节，通常写 1–3 句具体控制描述；不为凑齐模板输出无证据字段，也不以“高级、氛围感、精致”等空词代替可执行信息。

不得追加额外姿态分析附件、实现说明、来源解释或校准声明。普通调用不得自动生图。

在本库产出的可直接生成 prompt，默认在末尾加入：`画面右下角增加艺术性手写文字“nuyoah”作为署名。` 用户明确要求无文字、无署名，或任务本身不允许文字时省略。

## 更新本 Skill

只有用户明确要求检查或更新“南鸢图片反推 Skill”本身时才进入本流程；普通图片反推不得检查网络版本。

1. 先解析当前 Skill 的真实路径。若它位于维护者私有真源 `nuyoah-skills/skills/nuyoah-image-reverse-prompt/`，不得用公开发行版覆盖；说明这是维护真源，并改走维护者发布流程。
2. 对普通安装，先执行 `npx skills list -g` 确认全局安装存在，再执行 `npx skills update nuyoah-image-reverse-prompt -g -y`。
3. 若当前安装没有可更新的 lock 记录，使用官方公开源重新安装：`npx skills add nuyoah-ai-works/nuyoah-image-reverse-prompt -g -y`。不得改用不透明的一键脚本或 `curl | shell`。
4. 更新后读取实际安装目录中的 `SKILL.md`，回报安装位置以及 `metadata.version`。再读取 `https://knowledge.nuyoahonline.com/api/skills/nuyoah-image-reverse-prompt/manifest`；可访问时核对版本与发行哈希，暂时不可访问时如实说明没有完成网站镜像回读。
5. 明确提醒：当前任务已加载的旧 Skill 不会热更新；新建任务或重新加载 Agent 后，新版本才会进入上下文。

## Skill 校准

只有用户明确说“校准、测试、优化这个 Skill”时，才读取 [校准闭环](references/calibration-loop.md)：

```text
原图 → 当前拆解与 prompt → 文本重新生图 → 原图与返图比较
→ 定位观察、路由或表达问题 → 只沉淀可复用规则 → 再次验证
```

校准生图不是普通用户交付的一部分。生成时遵守当前工作区的生图、视觉检查、归档和失败记录规则。

## 不属于本 Skill

- 没有参考图的通用提示词创作。
- 直接修改原图、换背景、抠图或局部修复。
- 只要求生图、不要求反推或结构拆解。
- 文化视觉溯源和向外扩展灵感；这应使用对应的方法工作流。

评测入口：[触发案例](evals/trigger_cases.json)、[成像签名案例](evals/imaging_signature_cases.json)、[真人摄影时尚海报案例](evals/fashion_poster_cases.json)。
