# 🦞 Moltbot — 个人 AI 助手

<p align="center">
  <img src="https://raw.githubusercontent.com/moltbot/moltbot/main/docs/whatsapp-clawd.jpg" alt="Clawdbot" width="400">
</p>

<p align="center">
  <strong>蜕变！蜕变！</strong>
</p>

<p align="center">
  <a href="https://github.com/moltbot/moltbot/actions/workflows/ci.yml?branch=main"><img src="https://img.shields.io/github/actions/workflow/status/moltbot/moltbot/ci.yml?branch=main&style=for-the-badge" alt="CI 状态"></a>
  <a href="https://github.com/moltbot/moltbot/releases"><img src="https://img.shields.io/github/v/release/moltbot/moltbot?include_prereleases&style=for-the-badge" alt="GitHub 发布版本"></a>
  <a href="https://deepwiki.com/moltbot/moltbot"><img src="https://img.shields.io/badge/DeepWiki-moltbot-111111?style=for-the-badge" alt="DeepWiki"></a>
  <a href="https://discord.gg/clawd"><img src="https://img.shields.io/discord/1456350064065904867?label=Discord&logo=discord&logoColor=white&color=5865F2&style=for-the-badge" alt="Discord"></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-MIT-blue.svg?style=for-the-badge" alt="MIT 许可证"></a>
</p>

**Moltbot** 是一款运行在您自己设备上的 *个人 AI 助手*。
它可以在您已有的渠道上回答您（WhatsApp、Telegram、Slack、Discord、Google Chat、Signal、iMessage、Microsoft Teams、WebChat），以及扩展渠道如 BlueBubbles、Matrix、Zalo 和 Zalo Personal。它可以在 macOS/iOS/Android 上进行语音交流，并能渲染您控制的实时画布（Canvas）。网关（Gateway）只是控制平面 —— 产品核心是助手本身。

如果您想要一个感觉像本地运行、响应迅速且始终在线的个人单用户助手，这就是您的选择。

[网站](https://molt.bot) · [文档](https://docs.molt.bot) · [入门指南](https://docs.molt.bot/start/getting-started) · [更新指南](https://docs.molt.bot/install/updating) · [案例展示](https://docs.molt.bot/start/showcase) · [常见问题](https://docs.molt.bot/start/faq) · [向导](https://docs.molt.bot/start/wizard) · [Nix](https://github.com/moltbot/nix-clawdbot) · [Docker](https://docs.molt.bot/install/docker) · [Discord](https://discord.gg/clawd)

推荐设置：运行入门向导 (`moltbot onboard`)。它将引导您完成网关、工作区、渠道和技能的设置。CLI 向导是推荐路径，适用于 **macOS、Linux 和 Windows (通过 WSL2；强烈推荐)**。
支持 npm、pnpm 或 bun。
新安装？从这里开始：[入门指南](https://docs.molt.bot/start/getting-started)

**订阅 (OAuth):**
- **[Anthropic](https://www.anthropic.com/)** (Claude Pro/Max)
- **[OpenAI](https://openai.com/)** (ChatGPT/Codex)

模型说明：虽然支持任何模型，但我强烈建议使用 **Anthropic Pro/Max (100/200) + Opus 4.5**，因为它具有强大的长上下文能力和更好的提示词注入防御。参见 [入门设置](https://docs.molt.bot/start/onboarding)。

## 模型 (选择 + 认证)

- 模型配置 + CLI: [模型](https://docs.molt.bot/concepts/models)
- 认证配置文件轮换 (OAuth vs API 密钥) + 备用方案: [模型故障转移](https://docs.molt.bot/concepts/model-failover)

## 安装 (推荐)

运行环境: **Node ≥22**。

```bash
npm install -g moltbot@latest
# 或者: pnpm add -g moltbot@latest

moltbot onboard --install-daemon
```

向导会安装网关守护进程（launchd/systemd 用户服务），使其保持运行。
历史说明：`clawdbot` 仍可作为兼容别名使用。

## 快速开始 (TL;DR)

运行环境: **Node ≥22**。

完整新手指南（认证、配对、渠道）：[入门指南](https://docs.molt.bot/start/getting-started)

```bash
moltbot onboard --install-daemon

moltbot gateway --port 18789 --verbose

# 发送消息
moltbot message send --to +1234567890 --message "来自 Moltbot 的问候"

# 与助手交谈（可选择发送回任何已连接的渠道：WhatsApp/Telegram/Slack/Discord/Google Chat/Signal/iMessage/BlueBubbles/Microsoft Teams/Matrix/Zalo/Zalo Personal/WebChat）
moltbot agent --message "发货清单" --thinking high
```

升级？[更新指南](https://docs.molt.bot/install/updating)（并运行 `moltbot doctor`）。

## 开发渠道

- **stable**: 标记的发布版本 (`vYYYY.M.D` 或 `vYYYY.M.D-<patch>`)，npm 标签为 `latest`。
- **beta**: 预发布版本标签 (`vYYYY.M.D-beta.N`)，npm 标签为 `beta`（可能缺少 macOS 应用）。
- **dev**: `main` 分支的最新进度，npm 标签为 `dev`（发布时）。

切换渠道 (git + npm): `moltbot update --channel stable|beta|dev`。
详情: [开发渠道](https://docs.molt.bot/install/development-channels)。

## 从源码构建 (开发)

从源码构建建议使用 `pnpm`。Bun 可选，用于直接运行 TypeScript。

```bash
git clone https://github.com/moltbot/moltbot.git
cd moltbot

pnpm install
pnpm ui:build # 首次运行时自动安装 UI 依赖
pnpm build

pnpm moltbot onboard --install-daemon

# 开发循环 (TS 更改时自动重新加载)
pnpm gateway:watch
```

注意：`pnpm moltbot ...` 直接运行 TypeScript（通过 `tsx`）。`pnpm build` 生成 `dist/` 目录，用于通过 Node 或打包好的 `moltbot` 二进制文件运行。

## 安全默认设置 (私聊访问)

Moltbot 连接到真实的即时通讯平台。请将收到的私聊消息视为 **不可信输入**。

完整安全指南: [安全](https://docs.molt.bot/gateway/security)

在 Telegram/WhatsApp/Signal/iMessage/Microsoft Teams/Discord/Google Chat/Slack 上的默认行为：
- **私聊配对** (`dmPolicy="pairing"` / `channels.discord.dm.policy="pairing"` / `channels.slack.dm.policy="pairing"`): 未知发送者会收到一个简短的配对码，机器人不会处理他们的消息。
- 批准方式: `moltbot pairing approve <channel> <code>`（随后发送者将被添加到本地允许列表存储中）。
- 公开接收私聊消息需要显式开启：设置 `dmPolicy="open"` 并在渠道允许列表中包含 `"*"` (`allowFrom` / `channels.discord.dm.allowFrom` / `channels.slack.dm.allowFrom`)。

运行 `moltbot doctor` 以检查风险或配置错误的私聊策略。

## 亮点

- **[本地优先网关](https://docs.molt.bot/gateway)** — 用于会话、渠道、工具和事件的单一控制平面。
- **[多渠道收件箱](https://docs.molt.bot/channels)** — WhatsApp, Telegram, Slack, Discord, Google Chat, Signal, iMessage, BlueBubbles, Microsoft Teams, Matrix, Zalo, Zalo Personal, WebChat, macOS, iOS/Android。
- **[多智能体路由](https://docs.molt.bot/gateway/configuration)** — 将入站渠道/账户/联系人路由到隔离的智能体（工作区 + 每个智能体独立的会话）。
- **[语音唤醒](https://docs.molt.bot/nodes/voicewake) + [通话模式](https://docs.molt.bot/nodes/talk)** — 配合 ElevenLabs 为 macOS/iOS/Android 提供始终在线的语音功能。
- **[实时画布 (Live Canvas)](https://docs.molt.bot/platforms/mac/canvas)** — 由智能体驱动的视觉工作区，采用 [A2UI](https://docs.molt.bot/platforms/mac/canvas#canvas-a2ui)。
- **[一流的工具支持](https://docs.molt.bot/tools)** — 浏览器、画布、节点、定时任务、会话以及 Discord/Slack 动作。
- **[伴侣应用](https://docs.molt.bot/platforms/macos)** — macOS 菜单栏应用 + iOS/Android [节点](https://docs.molt.bot/nodes)。
- **[入门向导](https://docs.molt.bot/start/wizard) + [技能](https://docs.molt.bot/tools/skills)** — 向导驱动的设置，包含内置、托管和工作区技能。

## 星标历史

[![星标历史图表](https://api.star-history.com/svg?repos=moltbot/moltbot&type=date&legend=top-left)](https://www.star-history.com/#moltbot/moltbot&type=date&legend=top-left)

## 核心平台

- [网关 WS 控制平面](https://docs.molt.bot/gateway): 包含会话、在线状态、配置、定时任务、Webhook、[控制 UI](https://docs.molt.bot/web) 和 [画布宿主](https://docs.molt.bot/platforms/mac/canvas#canvas-a2ui)。
- [CLI 界面](https://docs.molt.bot/tools/agent-send): gateway, agent, send, [向导](https://docs.molt.bot/start/wizard) 和 [诊断工具](https://docs.molt.bot/gateway/doctor)。
- [Pi 智能体运行时](https://docs.molt.bot/concepts/agent): RPC 模式，支持工具流和块流。
- [会话模型](https://docs.molt.bot/concepts/session): `main` 用于直接聊天，支持群组隔离、激活模式、队列模式、自动回复。群组规则: [群组](https://docs.molt.bot/concepts/groups)。
- [媒体流水线](https://docs.molt.bot/nodes/images): 图像/音频/视频，转录钩子，大小限制，临时文件生命周期。音频详情: [音频](https://docs.molt.bot/nodes/audio)。

### 渠道

- [渠道](https://docs.molt.bot/channels): [WhatsApp](https://docs.molt.bot/channels/whatsapp) (Baileys), [Telegram](https://docs.molt.bot/channels/telegram) (grammY), [Slack](https://docs.molt.bot/channels/slack) (Bolt), [Discord](https://docs.molt.bot/channels/discord) (discord.js), [Google Chat](https://docs.molt.bot/channels/googlechat) (Chat API), [Signal](https://docs.molt.bot/channels/signal) (signal-cli), [iMessage](https://docs.molt.bot/channels/imessage) (imsg), [BlueBubbles](https://docs.molt.bot/channels/bluebubbles) (扩展), [Microsoft Teams](https://docs.molt.bot/channels/msteams) (扩展), [Matrix](https://docs.molt.bot/channels/matrix) (扩展), [Zalo](https://docs.molt.bot/channels/zalo) (扩展), [Zalo Personal](https://docs.molt.bot/channels/zalouser) (扩展), [WebChat](https://docs.molt.bot/web/webchat)。
- [群组路由](https://docs.molt.bot/concepts/group-messages): 提及过滤、回复标签、按渠道分块和路由。渠道规则: [渠道](https://docs.molt.bot/channels)。

### 应用 + 节点

- [macOS 应用](https://docs.molt.bot/platforms/macos): 菜单栏控制平面，[语音唤醒](https://docs.molt.bot/nodes/voicewake)/PTT，[通话模式](https://docs.molt.bot/nodes/talk) 叠加层，[WebChat](https://docs.molt.bot/web/webchat)，调试工具，[远程网关](https://docs.molt.bot/gateway/remote) 控制。
- [iOS 节点](https://docs.molt.bot/platforms/ios): [画布](https://docs.molt.bot/platforms/mac/canvas)，[语音唤醒](https://docs.molt.bot/nodes/voicewake)，[通话模式](https://docs.molt.bot/nodes/talk)，摄像头，屏幕录制，Bonjour 配对。
- [Android 节点](https://docs.molt.bot/platforms/android): [画布](https://docs.molt.bot/platforms/mac/canvas)，[通话模式](https://docs.molt.bot/nodes/talk)，摄像头，屏幕录制，可选短信。
- [macOS 节点模式](https://docs.molt.bot/nodes): system.run/notify + 画布/摄像头暴露。

### 工具 + 自动化

- [浏览器控制](https://docs.molt.bot/tools/browser): 专用的 moltbot Chrome/Chromium，快照，动作，上传，配置文件。
- [画布](https://docs.molt.bot/platforms/mac/canvas): [A2UI](https://docs.molt.bot/platforms/mac/canvas#canvas-a2ui) 推送/重置，评估，快照。
- [节点](https://docs.molt.bot/nodes): 摄像头拍照/剪辑，屏幕录制，[位置获取](https://docs.molt.bot/nodes/location-command)，通知。
- [定时任务 + 唤醒](https://docs.molt.bot/automation/cron-jobs); [Webhook](https://docs.molt.bot/automation/webhook); [Gmail Pub/Sub](https://docs.molt.bot/automation/gmail-pubsub)。
- [技能平台](https://docs.molt.bot/tools/skills): 内置、托管和工作区技能，带有安装门控 + UI。
