# ⬡ VAULT v4 — Private AI Security Command Center

> **A single-file, zero-server, AI-powered mobile security dashboard.**
> Built for Android. Runs entirely in your browser. Nothing stored in the cloud.

---

## What is VAULT?

VAULT is a personal security command center that runs as a single HTML file — no installation, no server, no backend. It combines a private AI assistant (powered by Anthropic's Claude) with a suite of real browser-based security tools: permission auditing, network analysis, dark web breach scanning, location spoofing, threat intelligence, and more.

Everything runs locally on your device. The only external calls made are to Anthropic's API (for AI responses), HaveIBeenPwned (for breach scanning), and standard geolocation/IP lookup services — all of which you control explicitly.

---

## Features

### 💬 AI Chat — Private Security Assistant
A full streaming chat interface connected to Claude (claude-sonnet-4). The AI is context-aware — it knows your current location mode, VPN status, watchdog event counts, and installed modules, so every response is relevant to your actual security posture. Quick-command shortcuts cover common security questions instantly.

### 🐕 Watchdog
Real-time permission scanner using the browser Permissions API. Checks camera, microphone, geolocation, clipboard, accelerometer, and more. Monitors clipboard events, battery drain, tab visibility changes, and network state. Logs every event with timestamps and severity classification.

### 🚨 Threat Intelligence Feed
A curated CVE database covering recent Android and DNG SDK vulnerabilities with CVSS scores, affected versions, and patch dates. Tap any CVE to get an immediate AI breakdown of whether it affects your device and what to do.

### 📡 Network Analysis
- Real-time connection type, downlink speed, and latency from the Network Information API
- VPN detection via latency heuristics
- DNS leak testing across multiple resolvers
- WebRTC IP leak detection — catches real IP exposure even behind a VPN

### 🕵️ Dark Web Scanner
- Email breach lookup via the HaveIBeenPwned API v3
- Password breach check using k-anonymity (only the first 5 characters of the SHA-1 hash are transmitted — your password never leaves your device)
- Scan history with masked email display

### 📍 Location Control
Three modes: fully disabled, spoofed (choose from 10 global cities), or live GPS. Includes an emergency kill switch that instantly resets all location state with a single tap. All location access attempts are logged.

### 🔎 Intel Engine *(New in v4)*
On-demand threat lookup for IP addresses, domains, and Android app package names. IP addresses are resolved to live geolocation data. All entities can be sent directly to the AI for threat analysis. Maintains a session tracker registry for flagged known-bad domains.

### ⬆ Upgrade System *(New in v4)*
VAULT can request additional browser capabilities to unlock new modules. Six upgrade modules are available, each declaring exactly which browser APIs and permissions it requires. Every permission appears in a **Tool Request Queue** where you review and grant each one individually before installation proceeds. The AI can explain every requested permission before you approve it.

Available modules: Fingerprint Shield, Deep Network Scanner, Malware Heuristics Engine, Crypto Vault, Live Threat Feed, AI Self-Patching.

### ⚙ System Panel *(New in v4)*
Deep device audit covering browser fingerprint vectors (user agent, platform, hardware concurrency, device memory, language settings), capability exposure (WebRTC, geolocation, Bluetooth, notifications), WebCrypto status, entropy metrics, storage usage, and session security details.

### 🔒 Encrypted Notes
Local-only note storage. Notes are saved to `localStorage` and never transmitted anywhere. Create, edit, and delete notes with a full in-panel editor.

### 🛡 Privacy Score
A composite 0–100 score calculated from your live settings — location mode, VPN status, permission grants, and encryption state — displayed as an animated ring gauge with a full checklist breakdown.

### 🍞 Toast Notifications *(New in v4)*
Real-time security alerts surface regardless of which panel you're viewing — VPN detection failures, breach discoveries, WebRTC leaks, permission grants, and more.

---

## Getting Started

### Option 1: GitHub Pages (Recommended)
1. Fork or clone this repository
2. Go to **Settings → Pages** in your repo
3. Under *Branch*, select `main` and click Save
4. VAULT will be live at `https://yourusername.github.io/your-repo-name/`

### Option 2: Run Locally
Download `index.html` and open it directly in any modern mobile or desktop browser. No web server required.

---

## API Key Setup

VAULT uses Anthropic's Claude API for all AI features. To enable full AI mode:

1. Get an API key from [console.anthropic.com](https://console.anthropic.com)
2. When VAULT loads, enter your key in the initialization screen
3. The key is stored in **session memory only** — it is never written to disk, localStorage, or any server

VAULT works in limited mode without an API key — all non-AI tools (breach scanner, network tests, watchdog, location) remain fully functional.

---

## Privacy & Security Model

| Concern | Answer |
|---|---|
| Is my API key stored? | Session memory only. Cleared when you close the tab. |
| Is my chat history stored? | No. All messages exist only in the current session. |
| Does VAULT phone home? | No. There is no VAULT server. |
| What external calls are made? | Anthropic API (AI), HaveIBeenPwned (breach scan), ipapi.co (IP lookup), pwnedpasswords.com (password check). All are opt-in actions you trigger manually. |
| Is my password sent during breach check? | No. Only the first 5 characters of a SHA-1 hash are transmitted, using k-anonymity. |
| Where are notes stored? | `localStorage` on your device only. |

---

## Compatibility

Designed and tested on **Samsung S24 FE running Android 16 with Chrome**. Works on any modern Chromium-based mobile or desktop browser. Some features (Permissions API, Network Information API, WebRTC) may behave differently on Firefox or Safari due to browser API availability.

---

## Version History

| Version | Notes |
|---|---|
| v4.0 | Intel Engine, Upgrade System, System Panel, toast notifications, bug fixes (note editing, VPN timing, stream stability, privacy score updates) |
| v3.0 | Initial public release — AI chat, Watchdog, Threats, Network, Dark Web, Location, Notes, Privacy Score |

---

## Bug Fixes in v4

The following issues present in v3 were resolved in v4:

- **Note editing** — saving an open note always created a new entry instead of updating the existing one; editing now correctly tracks which note is being modified.
- **Privacy score location check** — the DOM selector was targeting the wrong element class, silently failing to update the location row when mode changed.
- **VPN latency detection** — `performance.now()` was being called before the fetch resolved, giving near-zero readings; timing now correctly wraps only the awaited network call.
- **Stream error cleanup** — a crashed or interrupted AI stream left a dangling element ID that broke subsequent messages; this is now cleaned up on any error path.
- **Busy AI queue** — calling a quick command while the AI was streaming silently dropped the message; it now queues in the input field instead.
- **Visibility monitoring** — the tab visibility watchdog was wired but never actually registered its event listener; fixed in v4.

---

## Disclaimer

VAULT is a personal security awareness tool. It does not replace professional security software, a real VPN client, or expert security advice. CVE data is curated manually and may not reflect the latest published vulnerabilities. Location spoofing affects only data readable by the browser — it does not modify your device's system-level GPS.

---

*Built with the Anthropic Claude API · Runs entirely client-side · No tracking · No ads*
