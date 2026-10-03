# Hocket

Hocket is a desktop app for Mac and Windows for running Claude Code and Codex side by side: your projects, conversations, agents, worktrees and pages in one place.

This repository only holds releases. There's no source code here.

## Install

Copy the prompt for your computer and paste it into Claude Code or Codex. It installs Hocket, checks the download and opens it. Hocket then sets up Claude Code and Codex itself, on its **Set up Claude and Codex** page.

### Mac

Apple silicon, macOS 13 or later.

```text
Install Hocket on this Mac. Perform and verify these steps, not just explain them.

Only install Hocket. Do not install, update, configure or sign in to Claude Code, Codex, the ChatGPT app, Git or gh, and don't tell me to: Hocket's own setup page does all of that once it opens. Don't ask me which agents I use.

Check before changing anything. Never read, print or copy credentials, tokens, passwords or Keychain items. Never use sudo without asking. Leave agent settings, projects and Hocket data alone. Do not bypass Gatekeeper or remove quarantine. Use a fresh temporary folder and clean up only your files. If your sandbox blocks network access or a write outside that folder, ask me to approve that command; don't work around it.

1. Check sw_vers -productVersion and sysctl -n hw.optional.arm64. Hocket needs macOS 13 or later on Apple silicon (arm64 must be 1, including under Rosetta). Stop if either fails, saying what's needed.

2. Fetch https://github.com/GudUtenTruser/hocket-releases/releases/latest/download/latest.json with curl --fail --location --proto '=https' --proto-redir '=https' --max-time 30 --max-filesize 262144. Read it as data with plutil -extract or osascript -l JavaScript (JSON.parse); never eval it. Require schemaVersion 1, a stable three-part numeric version, and arm64 with a url starting https://github.com/GudUtenTruser/hocket-releases/releases/download/ (no port, credentials or #fragment), a lowercase 128-digit hexadecimal sha512 and an integer size 1–1073741824. Download that zip with the same HTTPS-only options, --max-time 600 and --max-filesize set to its declared size. Check its byte size and shasum -a 512 against the feed. Stop on a mismatch.

3. Unpack the zip with ditto -x -k into your temporary folder; Hocket.app must be its only top-level item. Run codesign --verify --deep --strict and spctl -a -vv -t execute on it: both must succeed, and spctl must report accepted, source=Notarized Developer ID and origin=Developer ID Application: Thomas Dale (364NX5D6N5). Stop on failure.

4. If /Applications/Hocket.app exists, ask me to quit Hocket normally (never kill it), then move the old app into your temporary folder, so no second copy stays in /Applications; move it back if a later step fails, and delete it only after the new one opened. If /Applications needs elevation, ask before sudo or give me the Finder step. Copy the checked app with ditto into /Applications. Repeat both signature checks there and confirm CFBundleShortVersionString equals the feed version.

5. Run open /Applications/Hocket.app and confirm its window appears (ask me if you can't see it). Tell me: "Hocket's Set up Claude and Codex page takes it from here." Do not start conversations or send agent messages.

End with PASS or FAIL (with the exact next step) for: Mac and macOS; Hocket version, size and SHA-512; signature and notarization; installed in /Applications; Hocket opened. Claim no unverified success.
```

### Windows

Windows 11, x64 or ARM64. Windows builds aren't code-signed yet: the prompt checks the installer against the release feed's SHA-512 instead. Hocket installs for your user only, with no administrator prompt.

```text
Install Hocket on this Windows PC. Perform and verify these steps in PowerShell, not just explain them.

Only install Hocket. Do not install, update, configure or sign in to Claude Code, Codex, the ChatGPT app, Git or gh, and don't tell me to: Hocket's own setup page does all of that once it opens. Don't ask me which agents I use.

Check before changing anything. Never read, print or copy credentials, tokens, passwords or Credential Manager items. Never run anything as administrator. Leave agent settings, projects and Hocket data alone. Do not disable SmartScreen or Defender. Use a fresh folder under $env:TEMP and clean up only your files. If your sandbox blocks network access or a write outside that folder, ask me to approve that command; don't work around it.

1. Check Windows 11: [Environment]::OSVersion.Version.Build must be 22000 or later. Find the CPU: $env:PROCESSOR_ARCHITEW6432, else $env:PROCESSOR_ARCHITECTURE; AMD64 means x64, ARM64 means arm64. Stop on anything else, saying what's needed.

2. Fetch https://github.com/GudUtenTruser/hocket-releases/releases/latest/download/latest.json with Invoke-RestMethod (-TimeoutSec 30). Treat it as data; never execute it. Require schemaVersion 1, a stable three-part numeric version, and windows.<x64 or arm64, my CPU> with a url starting https://github.com/GudUtenTruser/hocket-releases/releases/download/ (no port, credentials or #fragment), a lowercase 128-digit hexadecimal sha512 and an integer size 1–1073741824. Download that installer with Invoke-WebRequest -UseBasicParsing (-TimeoutSec 600) into your folder. Check its byte size and (Get-FileHash -Algorithm SHA512).Hash, lowercased, against the feed. Stop on a mismatch. Windows builds aren't code-signed yet, so this HTTPS feed and SHA-512 are the integrity check; say so in your report.

3. If Hocket is running (Get-Process Hocket), ask me to quit it normally; never kill it. Install for this user only, silently: Start-Process -FilePath <installer> -ArgumentList '/S' -Wait. No administrator prompt should appear; stop if one does. Check that %LOCALAPPDATA%\Programs\claude-codex-hub\Hocket.exe exists and its (Get-Item).VersionInfo.ProductVersion starts with the feed version.

4. Start it with Start-Process and confirm its window appears (ask me if you can't see it). Tell me: "Hocket's Set up Claude and Codex page takes it from here." Do not start conversations or send agent messages. Hocket updates itself from the same feed afterwards.

End with PASS or FAIL (with the exact next step) for: Windows 11 and CPU; Hocket version, size and SHA-512; installed for this user; Hocket opened. Claim no unverified success.
```

### Without an agent

Download from [Releases](../../releases/latest):
- **Mac:** the `.dmg`. Drag Hocket to Applications and open it.
- **Windows:** `Hocket-<version>-win-x64-Setup.exe` or `Hocket-<version>-win-arm64-Setup.exe` for your CPU, and run it. SmartScreen asks once: More info → Run anyway.

## Agents

On first launch, Hocket's **Set up Claude and Codex** page installs and signs in the agents you want:
- **Claude:** Claude Code, signed in with your Claude account;
- **Codex:** signed in with your ChatGPT account.

## Updates

Hocket updates itself from this public feed on Mac and Windows. Updates need no GitHub login.
