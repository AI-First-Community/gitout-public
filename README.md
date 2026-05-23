# GitOut — Remote Control for Claude Code

**Live life. AI codes.**

GitOut is a free, open-source VS Code extension + Progressive Web App that lets you babysit Claude Code from your phone. Approve tool calls, answer questions, send follow-up instructions — all from anywhere.

[![VS Code Marketplace](https://img.shields.io/visual-studio-marketplace/v/innovate-with-sanjeev.gitout?label=VS%20Code%20Marketplace&color=ff5630)](https://marketplace.visualstudio.com/items?itemName=innovate-with-sanjeev.gitout)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Cost: Free](https://img.shields.io/badge/Cost-%240%20forever-2ea44f)](#cost-0-forever)

---

## ⚖️ Important: No central service

GitOut is **client-only software**. There is no GitOut server, no GitOut backend, no GitOut SaaS. All code runs on:

- **Your laptop** — the VS Code extension and local agent daemon
- **Your phone** — the Progressive Web App
- **Cloudflare's anonymous quick tunnel** (default) — or your own Cloudflare account if you opt to self-host

The maintainer of GitOut **operates no infrastructure**, **collects no data**, and **has no access** to your sessions, code, or Claude conversations.

---

## Install

1. Open VS Code → Extensions panel (`⇧⌘X`)
2. Search **"GitOut"**
3. Click **Install**

Or install from the [Marketplace page](https://marketplace.visualstudio.com/items?itemName=innovate-with-sanjeev.gitout).

## Quickstart (3 minutes)

Prerequisite: [Claude Code](https://docs.claude.com/en/docs/claude-code/getting-started) installed.

1. Open the Command Palette (`⇧⌘P`) → **GitOut: Start**
2. A side panel opens with a QR code
3. Scan the QR code with your phone → the GitOut PWA opens
4. On your phone, tap **Pair & enable notifications**
5. (Recommended) Add the PWA to your home screen: Safari → Share → Add to Home Screen
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

---

## Cost: $0 forever

GitOut is designed to **never cost you a cent** and **never cost the maintainer a cent**:

| Component | Hosted on | Who pays |
|---|---|---|
| VS Code extension | Your laptop | $0 — you |
| Agent daemon (Node) | Your laptop | $0 — you |
| Default tunnel | Cloudflare's free anonymous quick-tunnel pool | $0 — Cloudflare absorbs |
| Optional permanent URL | **Your own** Cloudflare Workers free tier | $0 — your free tier |
| Push notifications | FCM (Android) / APNS (iOS), free for low volume | $0 — Google/Apple |

The maintainer hosts **no shared infrastructure**. You will never be billed by GitOut, because there is nothing to bill for.

You may, optionally, self-host the relay Worker on your own Cloudflare account. If you choose to do so, you alone are responsible for your account, its usage, and any billing decisions you make on it. Cloudflare's free Workers plan does not require a credit card and cannot auto-upgrade you to a paid plan — but you should verify this on the Cloudflare dashboard before deploying anything.

## Privacy

- **No telemetry, no analytics, no account required.**
- The maintainer collects **zero data** — there is no server to collect it on.
- Your code, prompts, and Claude responses travel between your laptop and your phone via a Cloudflare tunnel — see [Cloudflare's privacy policy](https://www.cloudflare.com/privacypolicy/) for what they retain.
- The pairing code is a short-lived secret known only to your laptop and your phone.
- Source code for the agent and worker is **not** open-source at this time. The VS Code extension source ships inside the `.vsix` package (minified) and can be inspected by unzipping it.

## Requirements

- VS Code 1.80+ (any OS)
- [Claude Code](https://docs.claude.com/en/docs/claude-code/getting-started) installed
- A modern phone with a browser (iOS 16.4+ or any Chrome-based Android)
- For the default zero-setup mode: nothing else
- For the optional permanent URL mode: a free [Cloudflare](https://dash.cloudflare.com/sign-up) account

## AI tools supported

✅ **[Claude Code](https://docs.claude.com/en/docs/claude-code/getting-started)** — fully supported in the current release.

🛣️ **Planned** (community-driven): Cursor, GitHub Copilot Chat, OpenAI Codex CLI, Gemini Code Assist, Aider, and others.

**Want a different tool supported?** [Open an issue](https://github.com/AI-First-Community/gitout-public/issues/new?labels=tool-request&template=feature_request.md) describing which one — votes and demand are tracked publicly.

**Want to *build* support for a tool?** The source for the agent / PWA / worker is in a private repository for now. To get collaborator access, email **`sanjeev.azad@gmail.com`** with:

1. The AI tool you want to add (e.g., Cursor)
2. Your GitHub handle
3. A short note on what you'd build and your relevant experience

Priority goes to contributors who actively use the tool they want to integrate.

## Troubleshooting

Common issues seen during community testing, what causes them, and how to fix.

### 🌐 Tunnel & connectivity

<details>
<summary><b>Phone shows "Cloudflare Error 1033" when scanning the QR</b></summary>

**Cause:** The `cloudflared` client connected to Cloudflare's edge, but Cloudflare hasn't finished routing the quick-tunnel URL yet. Their own message warns *"it may take some time to be reachable."*

**Fix:** Wait 30–60 seconds after the URL appears, then retry the scan. If it persists, run **GitOut: Stop** → **GitOut: Start** for a fresh URL.

</details>

<details>
<summary><b>VS Code panel hangs on "Warming up the tunnel"</b></summary>

**Cause:** If you're on v0.1.9 or older, `cloudflared` wasn't installed and the tunnel never came up. Fixed in **v0.1.10+** which auto-downloads the binary.

**Fix:** Update the extension to the latest version. If still stuck on v0.1.10+, check the GitOut output channel (View → Output → "GitOut") for the actual error.

</details>

<details>
<summary><b>Quick tunnels keep failing / corporate VPN blocks <code>*.trycloudflare.com</code></b></summary>

**Cause:** Cloudflare's quick-tunnel pool is anonymous, best-effort infrastructure with no SLA. Many corporate networks also block outbound QUIC (port 443/UDP) which cloudflared uses by default.

**Fix:** Deploy your own free Cloudflare Worker as a relay. Set `gitout.relayUrl` in VS Code settings to `wss://your-worker.workers.dev/agent`. Bypasses cloudflared entirely.

</details>

### 📳 Push notifications

<details>
<summary><b>Phone doesn't buzz when the PWA is open in the foreground</b></summary>

**Cause:** iOS Safari and most Android browsers suppress Web Push banners when the app is already visible — they assume you're already looking at it.

**Fix:** Test with the screen locked or the PWA backgrounded. Approval prompts (`PreToolUse`) use `requireInteraction: true` and are more likely to surface even in foreground.

</details>

<details>
<summary><b>No notifications arrive at all, even with the screen locked</b></summary>

**Cause:** Stale subscription. The agent has an old push endpoint that FCM/APNS still accepts but no longer delivers to your current device (common after clearing browser data, OS reset, or testing across multiple devices).

**Fix:** On the phone PWA, tap the Unpair icon (top-right of Console) → re-enter the pairing code from the VS Code panel. A fresh subscription gets registered.

</details>

<details>
<summary><b>iOS: no "Allow Notifications" prompt on Pair</b></summary>

**Cause:** iOS only supports Web Push for PWAs **added to the Home Screen** (Apple's requirement, not ours). From a regular Safari tab, Pair will silently fail.

**Fix:** In Safari with the PWA open → Share button → **Add to Home Screen** → Add. Close Safari. Reopen GitOut from the home-screen icon. Tap Pair again — notification prompt now appears.

</details>

### ✅ Approval flow

<details>
<summary><b>Claude does Write/Edit/Bash without my phone getting an approval prompt</b></summary>

**Cause:** Missing the `PreToolUse` hook in `~/.claude/settings.json`. Common if you installed hooks via an older version of GitOut before that event existed.

**Fix:** Run **GitOut: Install Claude Code Hooks** from the Command Palette. The command is idempotent — safe to re-run. Verify:
```bash
python3 -c "import json; print(list(json.load(open('$HOME/.claude/settings.json')).get('hooks',{}).keys()))"
```
Expected: `['Stop', 'Notification', 'PreToolUse']`.

</details>

<details>
<summary><b>Tapped Approve, button stuck on "Approving…" forever</b></summary>

**Cause:** You tapped a push that FCM/APNS had queued — by the time you saw it, the agent's 5-minute decision timer had expired and Claude Code already prompted locally instead. The phone's late decision can't resolve the dead `requestId`.

**Fix:** Open Settings → Maintenance → **Clear** to wipe the stale cards. Retry with a fresh action that fires a new push.

</details>

### 📦 Installation

<details>
<summary><b>"Could not locate packages/agent" error popup</b></summary>

**Cause:** You're on GitOut v0.1.7 or older — those versions only shipped the extension UI, not the agent code. Since the source repo is private, there was no recovery path.

**Fix:** Update to **v0.1.8 or newer** from the Marketplace. The agent is bundled inside the .vsix now.

</details>

<details>
<summary><b>After auto-updating, the extension still behaves like the old version</b></summary>

**Cause:** VS Code caches loaded extension code in the extension-host process. A normal "Reload Window" doesn't always pick up the new bytes.

**Fix:** Fully quit VS Code (`⌘Q` on macOS, `File → Exit` elsewhere) and reopen. Then verify the version in the Extensions panel.

</details>

### 🔍 Where to look first

Before filing an issue, check the **GitOut output channel** in VS Code:

1. `View → Output`
2. In the dropdown on the right, select **GitOut**
3. Scroll to the bottom — the agent logs every hook, push, tunnel event, and error here

90% of issues show their root cause in this log.

## Issues & feedback

Still stuck after Troubleshooting? File an [issue](https://github.com/AI-First-Community/gitout-public/issues/new/choose). See [CONTRIBUTING.md](CONTRIBUTING.md) for what info to include — and please paste the last 20 lines of the GitOut output channel.

---

## ⚖️ Disclaimer

GitOut is provided **"as is"** under the [MIT license](LICENSE), without warranty of any kind, express or implied. By installing or using GitOut, you acknowledge and agree that:

1. **No infrastructure is operated by the maintainer.** GitOut runs entirely on your own hardware and on third-party services you choose (Cloudflare, FCM, APNS). The maintainer has no ability to monitor, control, or recover your sessions.

2. **You are solely responsible** for any third-party accounts you use with GitOut (Cloudflare, Apple developer push services, Google FCM) — including all billing, terms of service, and account decisions made on those platforms.

3. **No data is collected, transmitted to, or stored by the maintainer.** All data flow happens between devices you own and third-party services you have agreed to use.

4. **The maintainer is not liable** for any data loss, downtime, billing surprises, security incidents, or damages arising from the use of, or inability to use, this software. See the [MIT license](LICENSE) for the full warranty disclaimer.

5. **GitOut is not affiliated with, endorsed by, or sponsored by** Anthropic, Cloudflare, Apple, Google, Microsoft, or any other organization. "Claude" and "Claude Code" are trademarks of Anthropic; "VS Code" is a trademark of Microsoft. GitOut interoperates with these products as an independent third-party tool.

6. **Use at your own risk.** AI-generated code can be wrong, unsafe, or incomplete. Always review tool calls before approving them, especially destructive ones (file deletion, force pushes, database mutations). One-tap convenience does not replace one-tap review.

If any of these terms are unacceptable to you, do not install or use GitOut.

---

## License

[MIT](LICENSE) — free to use, modify, and redistribute. See [LICENSE](LICENSE) for the full text.

Built with [Claude Code](https://docs.claude.com/en/docs/claude-code/) and `@anthropic-ai/claude-agent-sdk`.
