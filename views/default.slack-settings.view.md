---
name: slack-settings
domain: default
version: 0.1.0
---

## State Bindings
- `slack.streaming` -> string
- `slack.replyToMode` -> string
- `slack.actions` -> object
- `slack.slashCommand` -> object
- `slack.loading` -> boolean

## Layout
```clapp-layout
Column(gap=5):
  Card(title=Threading & Streaming):
    Column(gap=4):
      Heading(level=4): "Reply Mode"
      TextInput(value=slack.replyToMode, placeholder="off"):
      Heading(level=4): "Streaming Mode"
      TextInput(value=slack.streaming, placeholder="partial"):
  
  Card(title=Slash Commands):
    SlashCommandConfig(config=slack.slashCommand):
  
  Card(title=Actions):
    FeatureToggles(actions=slack.actions):
```

## Intents
| Name | Payload | Description |
|------|---------|-------------|
| slack.init | `{}` | Load settings |
| slack.setReplyMode | `{ mode: string }` | Set reply threading mode |
| slack.setStreaming | `{ mode: string }` | Set streaming mode |
| slack.toggleAction | `{ group: string, enabled: boolean }` | Enable/disable action group |
| slack.setSlashCommand | `{ enabled: boolean, name?: string }` | Configure slash command |
