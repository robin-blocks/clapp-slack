---
name: slack-channels
domain: default
version: 0.1.0
---

## State Bindings
- `slack.dmPolicy` -> string
- `slack.groupPolicy` -> string
- `slack.channels` -> array
- `slack.loading` -> boolean

## Layout
```clapp-layout
Column(gap=5):
  Card(title=Access Control):
    Column(gap=4):
      Heading(level=4): "DM Policy"
      PolicySelector(value=slack.dmPolicy, type=dm):
      Heading(level=4): "Channel Policy"
      PolicySelector(value=slack.groupPolicy, type=group):
  
  Card(title=Allowed Channels):
    Column(gap=4):
      Conditional(when=slack.loading):
        Skeleton():
      Conditional(when=!slack.loading):
        Conditional(when=slack.channels.length):
          ChannelList(channels=slack.channels):
        Conditional(when=!slack.channels.length):
          Heading(level=4): "No channels configured"
      IntentButton(intent=slack.addChannel, label="Add Channel", variant=primary):
```

## Intents
| Name | Payload | Description |
|------|---------|-------------|
| slack.init | `{}` | Load channel config |
| slack.setDmPolicy | `{ policy: string }` | Set DM access policy |
| slack.setGroupPolicy | `{ policy: string }` | Set channel access policy |
| slack.addChannel | `{}` | Add channel to allowlist |
| slack.editChannel | `{ channelId: string }` | Edit channel settings |
| slack.removeChannel | `{ channelId: string }` | Remove channel from allowlist |
| slack.saveChannel | `{ channelId: string, requireMention?: boolean, users?: string[], skills?: string[] }` | Save channel config |
