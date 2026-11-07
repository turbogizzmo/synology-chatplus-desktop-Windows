# ChatPlus Desktop for Windows

<img src="public/chatplus.png" alt="ChatPlus Desktop Windows app icon" width="64" />

An unofficial, open-source **Windows** desktop client for Synology ChatPlus and
Synology Chat. It puts the chat on your Synology NAS in a lightweight Tauri app
with native notifications, unread badges and a tray icon.

This repository is a fork of
[ChatPlus Desktop by Swiph3l](https://github.com/Swiph3l/synology-chatplus-desktop),
maintained by **turbogizzmo**. It focuses the app on Synology ChatPlus and makes
signing in simpler, matching the
[macOS port](https://github.com/turbogizzmo/synology-chatplus-desktop-OSX).

[![CI](https://github.com/turbogizzmo/synology-chatplus-desktop-Windows/actions/workflows/ci.yml/badge.svg)](https://github.com/turbogizzmo/synology-chatplus-desktop-Windows/actions/workflows/ci.yml)
[![Windows x64](https://img.shields.io/badge/Windows-x64-0078D4)](#build-from-source)
[![GPLv3](https://img.shields.io/badge/license-GPLv3-blue)](LICENSE)
[![Tauri 2](https://img.shields.io/badge/Tauri-2-24C8DB)](https://v2.tauri.app/)

## What's different in this fork

- **Synology first.** First launch goes straight to connecting your NAS, with
  Synology ChatPlus as the main choice and classic Synology Chat as a secondary
  link. Slack, Discord, WhatsApp, Messenger and Mattermost are hidden until you turn
  on **Settings > Services > Show other chat services**, so it's clear which app
  "ChatPlus" is. Profiles that already use one of those services keep seeing them.
- **Simpler sign-in.** You no longer need a DSM Login Portal alias such as
  `https://nas.example.com/chat/`. Enter either:
  - your NAS address, for example `https://nas.example.com:5001`. ChatPlus opens
    through DSM's own launcher.
  - just your **QuickConnect ID**, for example `mynas` (or the `quickconnect.to/mynas`
    link). The app finds your NAS the way Synology's apps do and only connects to an
    address that proves it is that NAS. It follows you between networks: it rechecks
    every minute, and Ctrl+R forces a recheck.

An existing `/chat/` alias URL keeps working exactly as before.

## Supported services

| Service           | Status                                                                         |
| ----------------- | ------------------------------------------------------------------------------ |
| Synology ChatPlus | Primary; dedicated theme, unread and notification integration                  |
| Synology Chat     | Dedicated unread/notification integration                                      |
| Discord           | Optional (hidden by default); unread/notification integration                  |
| WhatsApp          | Optional, experimental; native notifications, no read actions or unread totals |
| Messenger         | Optional, experimental; native notifications, no read actions or unread totals |
| Mattermost        | Optional, experimental; notifications from browser events                      |
| Slack             | Optional, experimental web session; no desktop unread/notifications            |

Provider login/SSO, calls and other features depend on each web app and its
policies. See [provider details](docs/PROVIDERS.md). This is an independent client
with no Synology, Meta, Slack or Discord affiliation.

## Features

- Persistent per-service sessions, each in its own WebView2 profile.
- Native Windows notifications with Full, Sender/chat or Generic previews and sound.
- Per-service unread dots plus tray, title and taskbar unread presentation.
- PDF and attachment downloads through the provider's session, with a Save As dialog.
- External links show their destination before opening your default browser.
- Light, Dark and System themes; English, Polish, Spanish, German, French,
  Japanese, Traditional Chinese, Brazilian Portuguese and Italian interface.
- Native menus, zoom/fullscreen, saved window geometry and optional start with Windows.

## Status and downloads

**[Download ChatPlus Desktop for Windows](https://turbogizzmo.github.io/synology-chatplus-desktop-Windows/)**
(version `0.11.0`, based on upstream `0.9.1` with fixes from upstream `1.0.2`). All versions are on the
[Releases page](https://github.com/turbogizzmo/synology-chatplus-desktop-Windows/releases).
Every pull request also builds a test installer you can download from its CI run
(GitHub sign-in required).

Installed apps check this repository for updates and only install ones signed with
this fork's update key. The fork uses its own app identifier, so it keeps its own
settings and can sit next to the upstream app.

Windows x64 is the supported target. Builds aren't Authenticode-signed, so Windows
SmartScreen may ask once before setup runs. See [update details](docs/UPDATER.md).

## Getting started

1. Install the app. Microsoft WebView2 is required, and setup can install it.
2. Choose **Set up Synology ChatPlus** and enter your NAS address or QuickConnect ID.
3. Sign in through Synology's own sign-in page.
4. Optional: in **Settings > Services**, add more accounts, or turn on
   **Show other chat services** to add Discord, Slack and others.

Provider notification preferences and Windows permissions also apply. Sessions are
managed locally by WebView2. Finish drafts and calls before changing a service's URL.

## Build from source

Requirements: Windows 10/11 x64, a stable Rust MSVC toolchain with rustfmt, the
Microsoft Edge WebView2 Runtime, and Node.js 22.12+ or 24.

```sh
npm ci
npm run tauri -- build
```

`npm run tauri -- dev` runs a development build. `npm test`, `npm run typecheck` and
`cargo test` (in `src-tauri`) run the checks that CI runs. See
[development](docs/DEVELOPMENT.md), [architecture](docs/ARCHITECTURE.md),
[notifications](docs/NOTIFICATIONS.md), [testing](docs/TESTING.md) and
[CONTRIBUTING.md](CONTRIBUTING.md).

## Privacy

No advertising, and conversation content is never monetized. Providers load from their
own services, and the app never sees your sign-in password. QuickConnect lookups go to
Synology's QuickConnect directory and then directly to your NAS. Optional update checks
contact GitHub. Diagnostics leave out message content, credentials, cookies/tokens and
private URLs. See [security reporting](SECURITY.md).

## Reporting bugs

[Open an issue](https://github.com/turbogizzmo/synology-chatplus-desktop-Windows/issues/new/choose)
in this repository with the app, Windows and WebView2 versions, provider version and
safe reproduction steps. About > **Copy diagnostics** supplies bounded, privacy-safe
state. Never include private messages, credentials/tokens, server/attachment URLs or
profiles.

## License and credits

GNU GPLv3 (GPL-3.0-only). See [LICENSE](LICENSE), [NOTICE](NOTICE) and
[licensing notes](docs/LICENSING.md). This is a modified version of ChatPlus Desktop,
originally written by Swiph3l and distributed under the same license. The copyright
notices in NOTICE apply, and dependencies retain their own licenses.

Not affiliated with or endorsed by Synology or any other supported provider. Product
names and trademarks identify compatibility and belong to their respective owners.
No proprietary Synology server application bundles are redistributed.
