---
title: "OpenClaw — Personal AI Assistant"
summary: "OpenClaw is a personal AI assistant you run on your own devices, supporting multiple messaging channels and AI models."
---

# {{ page.title }}

**OpenClaw** is a _personal AI assistant_ you run on your own devices.
It answers you on the channels you already use (WhatsApp, Telegram, Slack, Discord, Google Chat, Signal, iMessage, Microsoft Teams, WebChat), plus extension channels like BlueBubbles, Matrix, Zalo, and Zalo Personal. It can speak and listen on macOS/iOS/Android, and can render a live Canvas you control.

Source: [https://github.com/openclaw/openclaw](https://github.com/openclaw/openclaw)

## Install

Runtime: **Node ≥22**.

{% highlight bash %}
npm install -g openclaw@latest
# or: pnpm add -g openclaw@latest

openclaw onboard --install-daemon
{% endhighlight %}

## Quick Start

{% highlight bash %}
openclaw onboard --install-daemon

openclaw gateway --port 18789 --verbose

# Send a message
openclaw message send --to +1234567890 --message "Hello from OpenClaw"

# Talk to the assistant
openclaw agent --message "Ship checklist" --thinking high
{% endhighlight %}

## Highlights

- **Local-first Gateway** — single control plane for sessions, channels, tools, and events.
- **Multi-channel inbox** — WhatsApp, Telegram, Slack, Discord, Google Chat, Signal, iMessage, Microsoft Teams, Matrix, WebChat, and more.
- **Multi-agent routing** — route inbound channels/accounts/peers to isolated agents.
- **Voice Wake + Talk Mode** — always-on speech for macOS/iOS/Android.
- **Live Canvas** — agent-driven visual workspace.
- **First-class tools** — browser, canvas, nodes, cron, sessions, and channel actions.
- **Companion apps** — macOS menu bar app + iOS/Android nodes.
- **Onboarding wizard** — guided setup with bundled/managed/workspace skills.

## Models

Any model is supported. Recommended: **Anthropic Pro/Max + Opus 4.6** for long-context strength and better prompt-injection resistance.

- [Models documentation](https://docs.openclaw.ai/concepts/models)
- [Model failover](https://docs.openclaw.ai/concepts/model-failover)

## Security

OpenClaw connects to real messaging surfaces. Treat inbound DMs as **untrusted input**.

Default behavior: unknown senders receive a pairing code and the bot does not process their message until approved.

- Approve with: `openclaw pairing approve <channel> <code>`
- Run `openclaw doctor` to surface risky/misconfigured DM policies.

## Resources

- [Website](https://openclaw.ai)
- [Documentation](https://docs.openclaw.ai)
- [Getting Started](https://docs.openclaw.ai/start/getting-started)
- [GitHub Repository](https://github.com/openclaw/openclaw)
- [Discord Community](https://discord.gg/clawd)
