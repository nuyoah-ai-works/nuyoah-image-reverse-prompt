# 南鸢图片反推

<!-- yarkr:badges:start -->
[![Indexed on Yarkr](https://api.yarkr.com/functions/v1/api/api/v1/badges/repos/nuyoah-ai-works/nuyoah-image-reverse-prompt/version.svg)](https://yarkr.com/arks/nuyoah-ai-works/nuyoah-image-reverse-prompt)
<!-- yarkr:badges:end -->

把参考图转译成可理解、可复用、可直接生成的中文视觉语言。

它会按图片类型逐项拆解画幅、构图、主体、动作、空间、光线、色彩、材质与成像签名，再把有画面证据的控制信息重组为连续、可复制的中文 Prompt。它不会声称恢复原作者的原始 Prompt，也不会在普通反推中自动生图。

## 安装

```bash
npx skills add nuyoah-ai-works/nuyoah-image-reverse-prompt -g -y
```

安装后直接对支持 Agent Skills 的 Agent 说：

```text
使用南鸢图片反推拆解这张参考图，给我参考色卡和可直接生图的完整中文提示词。
```

## 更新

直接对 Agent 说：

```text
更新南鸢图片反推 Skill 到最新版。
```

也可以执行：

```bash
npx skills update nuyoah-image-reverse-prompt -g -y
```

更新完成后，新建任务或重新加载 Agent，让新版指令进入上下文。

## 文件

- `SKILL.md`：触发边界、普通反推、校准和更新流程。
- `references/`：图片类型、成像签名和输出合同。
- `agents/`：Agent 展示与兼容接口。
- `evals/`：触发、空间关系、成像签名和海报回归案例。

## 许可

[MIT License](LICENSE)

<!-- yarkr:install:start -->
## Install with Yarkr

This repo is indexed on [Yarkr](https://yarkr.com/arks/nuyoah-ai-works/nuyoah-image-reverse-prompt) as the ark [nuyoah-ai-works/nuyoah-image-reverse-prompt](https://yarkr.com/arks/nuyoah-ai-works/nuyoah-image-reverse-prompt), so its skills install into Claude Code, Codex, Cursor and other agent harnesses with one command.

### CLI

Install the whole ark, which Yarkr keeps equal to this repo:

```bash
npx yarkr-cli sync nuyoah-ai-works/nuyoah-image-reverse-prompt
```

Or add individual skills:

```bash
npx yarkr-cli add skill:nuyoah-ai-works/nuyoah-image-reverse-prompt/nuyoah-image-reverse-prompt
```

No Node.js? `curl -fsSL https://yarkr.com/install.sh | sh` (macOS, Linux) or `irm https://yarkr.com/install.ps1 | iex` (Windows PowerShell) installs `yarkr` as a standalone binary; then type `yarkr` in place of `npx yarkr-cli`.

### MCP

Connect your agent to the ark over MCP:

```bash
npx yarkr-cli mcp add nuyoah-ai-works/nuyoah-image-reverse-prompt
```

Or point any MCP client at `https://api.yarkr.com/functions/v1/api/mcp/o/nuyoah-ai-works/nuyoah-image-reverse-prompt`.
<!-- yarkr:install:end -->
