# Hocket

Hocket is a desktop app for Mac and Windows for running Claude Code and Codex side by side: your projects, conversations, agents, worktrees and pages in one place.

This repository only holds releases. There's no source code here.

## Install

Copy the prompt for your computer and paste it into Claude Code or Codex. It checks your machine, sets up the agents you use, installs Hocket, verifies the download and opens it.

### Mac

You need an Apple silicon Mac on macOS 13 or later (your agent's app may require a newer macOS).

```text
Set up this Mac for Hocket. Perform and verify these steps, not just explain them.

Ask once: “Which subscriptions do you have: Claude, ChatGPT, or both?” Set up the chosen agents; mark the other NOT SELECTED. One missing agent must not block using the other.

Check before changing anything. Fix what you safely can; otherwise give me the exact command or GUI step, wait for me, then recheck. Sign-ins are mine. Never read, print, copy or request credentials, tokens, passwords or Keychain items. Use official sign-in status commands, reporting only pass/fail and authentication mode. Never use sudo or change shell profiles without asking. Leave agent settings, projects and Hocket data alone. Do not bypass Gatekeeper, remove quarantine or start agent conversations to test. Use a fresh temporary folder and clean up only your files. If your sandbox blocks network access or a write outside that folder, ask me to approve that command; don't work around it.

1. Check sw_vers -productVersion and sysctl -n hw.optional.arm64. Hocket requires macOS 13+ and Apple silicon (arm64 must be 1, including under Rosetta). Stop if either fails, explaining the needed Mac or OS upgrade. Check selected apps' own minimum OS too; report any higher requirement.

2. Check xcode-select -p, xcrun --find git and /usr/bin/git --version. Git is required for worktrees. If tools are missing, run xcode-select --install; I complete Apple's installer. If git stops at the Xcode license, have me run sudo xcodebuild -license myself. Repeat all three checks. A full Xcode installation also supplies them. Do not create or change a repository to test.

3. If I chose Claude: Hocket searches the interactive login shell's PATH for an executable named claude, not an alias. Read that PATH with env -i HOME="$HOME" USER="$USER" LOGNAME="$LOGNAME" SHELL="${SHELL:-/bin/zsh}" TMPDIR="$TMPDIR" "${SHELL:-/bin/zsh}" -ilc 'printf "%s\n" "$PATH"' and use the first executable claude in it. Inspect executable paths only; never dump the environment. Check the actual binary's --version and claude auth status --json, reporting only loggedIn, authMethod and subscriptionType (it also prints the account's email and organization). If missing, download https://claude.ai/install.sh over HTTPS to your temporary folder and run it with bash, without sudo. The native launcher is ~/.local/bin/claude. If needed, ask before adding only ~/.local/bin to the appropriate shell profile; recheck in a fresh login shell. Ask me before updating, then run claude update and --version; for a package-manager installation use its official update command instead. If loggedIn isn't true or authMethod isn't claude.ai (an API key or Console login bills the API, not my subscription), have me run claude auth login in my terminal and complete its browser sign-in; then recheck. Official setup: https://code.claude.com/docs/en/setup

4. If I chose ChatGPT: check /Applications/ChatGPT.app and its Info.plist minimum OS. Install or update from https://learn.chatgpt.com/docs/app using the official Mac download and app update control; ask before replacing an existing app. Have me open it and sign in myself. Hocket uses the first executable at these paths, in order:
   /Applications/ChatGPT.app/Contents/Resources/codex-cli/CodexCLI.app/Contents/MacOS/codex
   /Applications/ChatGPT.app/Contents/Resources/codex
   Check that binary's --version and "<binary>" login status (never plain login, which starts a sign-in); it must say Logged in using ChatGPT. Capture status output locally and report only the authentication mode and pass/fail, never a key value. On failure, have me finish signing in to the ChatGPT app and recheck. If neither binary exists, install the current official app and repeat. Do not install a separate codex CLI.

5. gh is optional, needed only for New project's GitHub repository and Open pull request, including their GitHub branch/PR operations. Local projects and updates need no GitHub login. Check gh --version on the login PATH. Offer installation only for these features: brew install gh if Homebrew already exists; otherwise the official macOS package at https://cli.github.com. Do not install Homebrew just for this. Run gh auth status --hostname github.com with its output captured locally (it lists a masked token and scopes) and report only pass/fail and the account name. If needed, have me run gh auth login --hostname github.com myself, then recheck. Never read tokens or switch accounts. Mark skipped features NOT SELECTED.

6. Fetch https://github.com/GudUtenTruser/hocket-releases/releases/latest/download/latest.json with curl --fail --location --proto '=https' --proto-redir '=https', --max-time 30 and --max-filesize 262144. Parse JSON with available tools (Command Line Tools provide Python 3); never eval it. Require schemaVersion 1, a stable three-part numeric version, ISO pubDate, plain-text notes, and arm64 with a url starting https://github.com/GudUtenTruser/hocket-releases/releases/download/ (no port, credentials or #fragment), lowercase 128-digit hexadecimal sha512 and integer size 1–1073741824. Download that zip with the same HTTPS-only options, --max-time 600 and --max-filesize set to its declared size. Check actual byte size and shasum -a 512 against the manifest. Stop on a mismatch.

7. Stage the zip with ditto -x -k into your temporary folder. Require Hocket.app as its only top-level item. Run codesign --verify --deep --strict and spctl -a -vv -t execute on it: both must succeed; spctl must report accepted, source=Notarized Developer ID and origin=Developer ID Application: Thomas Dale (364NX5D6N5). Stop on failure. Before replacing /Applications/Hocket.app, ask and have me quit it normally; do not kill it or merge bundles. With approval, move the old app into your temporary folder as Hocket-<old version>.app (a copy left in /Applications would show in Spotlight and could take hocket:// links); move it back if any later step fails, and delete it only after Hocket opened. If /Applications needs elevation, ask before sudo or give the exact Finder step. Unpack the checked zip with ditto -x -k into /Applications. Repeat both signature/notarization checks there and confirm CFBundleShortVersionString equals the feed version. Run open /Applications/Hocket.app. Verify its window appears, or ask me to confirm if you cannot see it. Do not send an agent message.

End with PASS, FAIL (exact next step), or NOT SELECTED for: Mac/OS; Git/tools; Claude path/version/subscription sign-in; ChatGPT app/bundled Codex version/ChatGPT sign-in; optional gh/GitHub sign-in; Hocket version/size/SHA-512; installed signature/notarization; Hocket opened. Claim no unverified success.
```

### Windows

You need Windows 11, x64 or ARM64. Windows builds aren't code-signed yet: the prompt checks the installer's SHA-512 against the release feed instead, and if you download it yourself, SmartScreen asks once (More info → Run anyway). Hocket installs for your user only, with no administrator prompt.

```text
Set up this Windows PC for Hocket. Perform and verify these steps in PowerShell, not just explain them.

Ask once: "Which subscriptions do you have: Claude, ChatGPT, or both?" Set up the chosen agents; mark the other NOT SELECTED. One missing agent must not block using the other.

Check before changing anything. Fix what you safely can; otherwise give me the exact command or GUI step, wait for me, then recheck. Sign-ins are mine. Never read, print, copy or request credentials, tokens, passwords or Credential Manager items. Use official sign-in status commands, reporting only pass/fail and authentication mode. Never run anything as administrator, change the execution policy machine-wide, or edit my PATH or profile without asking. Leave agent settings, projects and Hocket data alone. Do not disable SmartScreen or Defender, and do not start agent conversations to test. Use a fresh folder under $env:TEMP and clean up only your files. If your sandbox blocks network access or a write outside that folder, ask me to approve that command; don't work around it.

1. Check Windows 11: (Get-CimInstance Win32_OperatingSystem).Caption and [Environment]::OSVersion.Version.Build must be 22000 or later. Find the CPU: $env:PROCESSOR_ARCHITEW6432, else $env:PROCESSOR_ARCHITECTURE; AMD64 means x64, ARM64 means arm64. Stop on anything else, explaining what's needed.

2. Git for Windows is required: Claude Code runs its commands in Git Bash, and Hocket's worktrees and changes use Git. Check git --version. If it's missing, ask, then install it for this user only with Git for Windows' official installer: from https://github.com/git-for-windows/git/releases/latest take the installer for my CPU (Git-<version>-64-bit.exe for x64, Git-<version>-arm64.exe for arm64; its URL must be on github.com/git-for-windows/git/releases/download/), download it into your folder and run it with /CURRENTUSER /VERYSILENT /NORESTART. Open a new PowerShell and recheck. Do not create or change a repository to test.

3. If I chose Claude: check claude --version on PATH. If missing, install Anthropic's official per-user build with irm https://claude.ai/install.ps1 | iex (never as administrator), then recheck in a new PowerShell; the launcher is %USERPROFILE%\.local\bin\claude.exe, so if PATH lacks that folder, ask before adding only it to my user PATH. Check claude auth status --json, reporting only loggedIn, authMethod and subscriptionType (it also prints the account's email and organization). If loggedIn isn't true or authMethod isn't claude.ai (an API key or Console login bills the API, not my subscription), have me run claude auth login and complete its browser sign-in; then recheck. Official setup: https://code.claude.com/docs/en/setup

4. If I chose ChatGPT: Hocket uses the ChatGPT app's Codex when the app is installed, otherwise a standalone Codex. Check codex --version on PATH. If there's no Codex, install OpenAI's official per-user Codex with irm https://chatgpt.com/codex/install.ps1 | iex, then recheck in a new PowerShell. Check codex login status (never plain codex login, which starts a sign-in); it must say Logged in using ChatGPT. Capture its output locally and report only the authentication mode and pass/fail. If not, have me run codex login and finish the browser sign-in; recheck. Codex's Windows sandbox needs a one-time setup that Hocket's own Set up Claude and Codex page offers; leave it to that page.

5. gh is optional, needed only for New project's GitHub repository and Open pull request. Local projects and updates need no GitHub login. Check gh --version. Offer installation only for these features, with winget install --id GitHub.cli -e. Run gh auth status --hostname github.com with its output captured locally and report only pass/fail and the account name. If needed, have me run gh auth login --hostname github.com myself, then recheck. Never read tokens or switch accounts.

6. Fetch https://github.com/GudUtenTruser/hocket-releases/releases/latest/download/latest.json with Invoke-RestMethod over HTTPS only (-MaximumRedirection 5, -TimeoutSec 30). Treat it as data; never execute it. Require schemaVersion 1, a stable three-part numeric version, and windows.<x64 or arm64, my CPU> with a url starting https://github.com/GudUtenTruser/hocket-releases/releases/download/ (no port, credentials or #fragment), a lowercase 128-digit hexadecimal sha512 and an integer size 1–1073741824. Download that installer with Invoke-WebRequest -UseBasicParsing (-TimeoutSec 600) into your folder. Check its byte size and (Get-FileHash -Algorithm SHA512).Hash, lowercased, against the manifest. Stop on a mismatch. Windows builds are not code-signed yet, so the HTTPS feed and this SHA-512 are the integrity check; say so in your report.

7. If Hocket is running (Get-Process Hocket), ask me to quit it normally; do not kill it. Install for this user only, silently: Start-Process -FilePath <installer> -ArgumentList '/S' -Wait. No administrator prompt should appear; stop if one does. Check that %LOCALAPPDATA%\Programs\claude-codex-hub\Hocket.exe exists and its (Get-Item).VersionInfo.ProductVersion starts with the feed version. Start it with Start-Process. Verify its window appears, or ask me to confirm if you cannot see it. Do not send an agent message. Hocket updates itself from the same feed afterwards.

End with PASS, FAIL (exact next step), or NOT SELECTED for: Windows 11/CPU; Git for Windows; Claude path/version/subscription sign-in; Codex version/ChatGPT sign-in; optional gh/GitHub sign-in; Hocket version/size/SHA-512; Hocket installed for this user; Hocket opened. Claim no unverified success.
```

### Without an agent

Download from [Releases](../../releases/latest):
- **Mac:** the `.dmg`. Drag Hocket to Applications and open it.
- **Windows:** `Hocket-<version>-win-x64-Setup.exe` or `Hocket-<version>-win-arm64-Setup.exe` for your CPU, and run it.

On first launch, Hocket's **Set up Claude and Codex** page installs and signs in the agents you choose.

## Agents

Hocket runs the agents you choose:
- **Claude:** Claude Code, signed in with your Claude account;
- **Codex:** on Mac the ChatGPT app, on Windows the ChatGPT app's Codex or OpenAI's standalone Codex, signed in with ChatGPT.

## Updates

Hocket updates itself from this public feed on both Mac and Windows. Updates need no GitHub login.
