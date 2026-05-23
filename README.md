# GitOut — phone control for Claude Code

**Live your life. Claude codes.**

GitOut is a free VS Code extension + Progressive Web App that lets you babysit Claude Code from your phone. Approve tool calls, answer questions, send follow-up instructions — all from anywhere.

[![VS Code Marketplace](https://img.shields.io/visual-studio-marketplace/v/sanjeev-azad.gitout?label=VS%20Code%20Marketplace&color=ff5630)](https://marketplace.visualstudio.com/items?itemName=sanjeev-azad.gitout)
[![Installs](https://img.shields.io/visual-studio-marketplace/i/sanjeev-azad.gitout?color=8a93a0)](https://marketplace.visualstudio.com/items?itemName=sanjeev-azad.gitout)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

---

## Install

1. Open VS Code → Extensions panel (`⇧⌘X`)
2. Search **"GitOut"**
3. Click **Install**

Or install from the [Marketplace page](https://marketplace.visualstudio.com/items?itemName=sanjeev-azad.gitout).

## Quickstart (3 minutes)

You need Claude Code installed first: https://docs.claude.com/en/docs/claude-code/getting-started

1. Open the Command Palette (`⇧⌘P`) → **GitOut: Start**
2. A side panel opens with a QR code and pairing instructions
3. Scan the QR code with your phone → the GitOut PWA opens in your browser
4. On your phone, tap **Pair & enable notifications**
5. Add the PWA to your home screen (Safari → Share → Add to Home Screen)
6. You're paired. When Claude needs you, your phone buzzes.

## What it does

| From your phone, you can: | How |
|---|---|
| **Approve tool calls** | Bash / Edit / Write tool calls show the actual diff or command. One-tap approve or reject. |
| **Answer Claude's questions** | When Claude uses `AskUserQuestion`, the options render as tappable buttons. |
| **Send follow-up instructions** | Type a nudge; Claude runs it and streams the response back to your phone. |
| **Configure per-tool policy** | Safe / Autopilot / Paranoid / Custom — set once, forget. |

## Screenshots

|  |  |
|---|---|
| ![Landing screen](docs/screenshots/landing-idle.png) | ![Console view](docs/screenshots/console-mixed.png) |
| ![Approval pending](docs/screenshots/landing-pending.png) | ![AskUserQuestion](docs/screenshots/console-askuserquestion.png) |

## Modes

| Mode | What happens |
|---|---|
| 📱 **Remote** | Claude SDK runs your reply, response streams back to your phone. Use when you're away from the desk. |
| 💻 **Desk** | Your reply lands in VS Code's Claude chat input. Use when you're back at the laptop. |

Toggle in Settings on the phone.

## How it works (in one paragraph)

A small Node daemon runs on your machine alongside Claude Code, hooked into Claude's `Stop` / `Notification` / `PreToolUse` events. When Claude needs you, the daemon sends a Web Push notification to your phone via a free Cloudflare Worker relay. Your phone is the front-end; the daemon executes anything you decide. No cloud database, no tracking, no account.

## Requirements

- VS Code 1.80+ (any OS)
- [Claude Code](https://docs.claude.com/en/docs/claude-code/getting-started) installed
- Any modern phone with a browser (iOS 16.4+ or any Chrome-based Android)
- Free [Cloudflare account](https://dash.cloudflare.com/sign-up) (optional — only if you want a permanent URL instead of the quick tunnel)

## Cost

**$0.** Everything runs on free tiers:
- Cloudflare Workers free plan
- Cloudflare Quick Tunnel (no account needed for testing)
- Web Push (free, no service)

## Privacy

- No telemetry, no analytics, no account.
- Your code and Claude's responses pass through a Cloudflare Worker you control. You can self-host the worker.
- The pairing code is a short-lived secret known only to your laptop and your phone.

## Issues & feature requests

Found a bug? Want a feature? File an [issue](https://github.com/AI-First-Community/gitout-public/issues/new/choose). See [CONTRIBUTING.md](CONTRIBUTING.md) for what info to include.

## License

[MIT](LICENSE) — free to use, modify, and redistribute.

---

Built with [Claude Code](https://docs.claude.com/en/docs/claude-code/) and `@anthropic-ai/claude-agent-sdk`.
