---
name: moongate-auth
description: MoonGate token provisioning and local credential management for msh.team internal apps (outsight, monitor Grafana, riskcontrol console, etc.). Use when a skill or script needs a MoonGate token, when setting up MOONGATE_ACCESS_TOKEN, or when choosing between a personal and a service token.
---

# MoonGate Auth

## Overview

MoonGate protects internal web apps. Skills authenticate with a personal MoonGate access token. The token itself must never be stored in a skill, committed to a repository, pasted into chat, or printed in logs.

## Token Types

- **Personal token** — default choice. Its permissions are exactly your own: any app you can open in a browser, the token can call. Create at <https://moongate.msh.work/tokens/create?type=personal>. Protect it like a password.
- **Service token** — for service-to-service calls. Request at <https://moongate.msh.work/tokens/create?type=service> (requires the target app's domain; approval by that app's admin). A service token for app A does not work on app B.

Some apps additionally require an in-app role (e.g. riskcontrol console-api requires the ADMIN role) — the token authenticates you, the role authorizes you.

## Credential Sources

Prefer these sources in order:

1. `MOONGATE_ACCESS_TOKEN` env var
2. macOS Keychain item with service `codex-moongate-access-token` and account `$USER`

## Setup

Ask the user to create or provide a token outside of chat. Do not ask them to paste the token into the conversation.

Recommended storage on macOS:

```bash
read -rsp "MoonGate token: " MOONGATE_ACCESS_TOKEN
printf '\n'
security add-generic-password -U -a "$USER" -s codex-moongate-access-token -w "$MOONGATE_ACCESS_TOKEN"
unset MOONGATE_ACCESS_TOKEN
```

To remove it later:

```bash
security delete-generic-password -a "$USER" -s codex-moongate-access-token
```

## For Skill Authors

Read the token through the bundled helper instead of re-implementing env/Keychain lookup:

```bash
TOKEN="$(~/.agents/skills/moongate-auth/scripts/moongate-token)"
# prints the token to stdout; exits 1 with setup instructions on stderr if missing
```

Skills should reference this skill for credential setup instead of documenting their own MoonGate token instructions.

## Safety Rules

- Do not print token values.
- Do not store token values in files, repo config, shell history, or skill files.
- Do not use `set -x` around token commands.
- If a token may have leaked, tell the user to revoke or rotate it (recreate at the token page) before continuing.
