# Slack Clapp

Slack integration manager for OpenClaw. Configure accounts, channels, settings, and monitor connection status.

**Repo:** https://github.com/robin-blocks/clapp-slack  
**Parent monorepo:** https://github.com/robin-blocks/clapps

## Installation

```bash
git clone https://github.com/robin-blocks/clapp-slack.git ~/.openclaw/clapps/slack
```

## Features

### Connections (Accounts)
- Add/edit/delete Slack accounts
- Support for Socket Mode and HTTP Events API
- Token management (botToken, appToken, signingSecret)
- Connection testing

### Channels (Access Control)
- DM policy (pairing/allowlist/open/disabled)
- Channel policy (open/allowlist/disabled)
- Per-channel settings:
  - Require mention
  - User allowlist
  - Custom skills

### Settings
- Threading mode (replyToMode)
- Streaming mode (off/partial/block/progress)
- Slash command configuration
- Action toggles (reactions, pins, emoji, etc.)

### Status
- Live connection monitoring
- Active channels
- Pending pairing requests (approve/reject)

## Structure

```
slack/
├── clapp.json
├── views/
│   ├── slack.app.md
│   ├── default.slack-connections.view.md
│   ├── default.slack-channels.view.md
│   ├── default.slack-settings.view.md
│   └── default.slack-status.view.md
├── components/
│   ├── AccountCard.tsx
│   ├── AccountEditor.tsx
│   ├── ChannelList.tsx
│   ├── ChannelEditor.tsx
│   ├── PolicySelector.tsx
│   ├── FeatureToggles.tsx
│   ├── SlashCommandConfig.tsx
│   └── ConnectionStatus.tsx
├── handlers/
│   └── slack-handler.ts
└── README.md
```

## Intents

### Connections
- `slack.init` — Load accounts
- `slack.addAccount` — Add new account
- `slack.editAccount` — Edit existing account
- `slack.deleteAccount` — Remove account
- `slack.testAccount` — Test connection
- `slack.saveAccount` — Save account config

### Channels
- `slack.setDmPolicy` — Set DM access policy
- `slack.setGroupPolicy` — Set channel access policy
- `slack.addChannel` — Add channel to allowlist
- `slack.editChannel` — Edit channel settings
- `slack.removeChannel` — Remove channel
- `slack.saveChannel` — Save channel config

### Settings
- `slack.setReplyMode` — Set threading mode
- `slack.setStreaming` — Set streaming mode
- `slack.toggleAction` — Enable/disable actions
- `slack.setSlashCommand` — Configure slash commands

### Status
- `slack.refreshStatus` — Refresh connection status
- `slack.approvePairing` — Approve pairing request
- `slack.rejectPairing` — Reject pairing request

## Development

This clapp is a git submodule of the main clapps monorepo.

**To customize locally:**
1. Edit files in `~/.openclaw/clapps/slack/`
2. Restart the connect server to see changes

**To contribute:**
```bash
cd ~/.openclaw/clapps/slack
git checkout -b my-feature
# Make changes
git commit -am "Add my feature"
git push origin my-feature
# Open PR at https://github.com/robin-blocks/clapp-slack
```

**In the parent monorepo:**
```bash
# Clone with submodules
git clone --recurse-submodules https://github.com/robin-blocks/clapps.git

# Sync clapp files into packages for build
pnpm sync:clapps

# Build and run
pnpm build
cd packages/connect && node dist/index.js
```

## Configuration

This clapp reads and writes to `~/.openclaw/openclaw.json` under `channels.slack.*`.

Uses OpenClaw commands:
- `openclaw config set channels.slack.*`
- `openclaw config delete channels.slack.*`
- `openclaw pairing approve slack <code>`
- `openclaw pairing reject slack <code>`
- `openclaw channels status --json`
