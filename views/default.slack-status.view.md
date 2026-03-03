---
name: slack-status
domain: default
version: 0.1.0
---

## State Bindings
- `slack.status` -> object
- `slack.pairings` -> array
- `slack.loading` -> boolean

## Layout
```clapp-layout
Column(gap=5):
  Card(title=Connection Status):
    Conditional(when=slack.loading):
      Skeleton():
    Conditional(when=!slack.loading):
      ConnectionStatus(status=slack.status):
  
  Card(title=Pending Pairings):
    Conditional(when=slack.pairings.length):
      List(data=slack.pairings):
        Row(gap=3):
          Column(flex=1):
            Heading(level=4): "{item.code}"
            MarkdownContent(content="{item.user}"):
          IntentButton(intent=slack.approvePairing, payload={code: item.code}, label="Approve", variant=primary):
          IntentButton(intent=slack.rejectPairing, payload={code: item.code}, label="Reject", variant=destructive):
    Conditional(when=!slack.pairings.length):
      Heading(level=4): "No pending pairings"
```

## Intents
| Name | Payload | Description |
|------|---------|-------------|
| slack.init | `{}` | Load status and pairings |
| slack.approvePairing | `{ code: string }` | Approve pairing request |
| slack.rejectPairing | `{ code: string }` | Reject pairing request |
| slack.refreshStatus | `{}` | Refresh connection status |
