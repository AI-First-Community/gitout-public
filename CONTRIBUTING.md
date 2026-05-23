# Contributing to GitOut

The source code for the agent/PWA/worker is in a private repository. This public repo is for the **VS Code extension distribution + community feedback**.

You can contribute by:

1. **Reporting bugs** — see below
2. **Suggesting features** — open an issue with the `enhancement` label
3. **Testing edge cases** — try GitOut in unusual setups (corporate VPN, iOS 18 PWA standalone, slow networks) and file what you find

## Reporting a bug

[Open a new issue](https://github.com/AI-First-Community/gitout-public/issues/new?template=bug_report.md) using the **Bug report** template, or include the following manually:

### Required info

- **Extension version** — `code --list-extensions --show-versions | grep gitout`
- **VS Code version** — Help → About
- **OS** — macOS / Windows / Linux + version
- **Phone OS + browser** — iOS 17.4 Safari, Android 14 Chrome, etc.
- **Mode** — Remote (📱) or Desk (💻)
- **What you did** — step-by-step to reproduce
- **What you expected**
- **What happened instead**

### Helpful extras

- **VS Code output channel** — View → Output → "GitOut" — paste the last 20 lines
- **Agent log** — `~/.gitout/agent.log` (last 50 lines)
- **Network trace** — if push notifications aren't arriving, your phone's DevTools console screenshot

## The 5 categories of bugs we most expect

1. **Push notification delivery** — corporate VPN, iOS Low Power Mode, Android battery optimization
2. **Multi-device pairing** — same agent, two phones — never actually tested
3. **Long-running sessions** — >50k tokens and the context-too-long auto-fallback path
4. **iOS PWA quirks** — Apple keeps shifting Web Push standalone-mode behavior across 16.4 / 17 / 18
5. **Notification action buttons** — Approve/Reject from lockscreen on Android Chrome

If you hit any of these, please include as much network/log detail as you can — these are the hardest to reproduce.

## Privacy

When filing an issue, please **redact** any code, prompts, or Claude responses that contain sensitive information. Replace with `<REDACTED>` placeholders. Logs are usually safe but double-check.

## License

By contributing (issues, suggestions, PRs against this docs repo), you agree your contributions are licensed under [MIT](LICENSE).
