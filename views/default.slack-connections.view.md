---
name: slack-connections
domain: default
version: 0.1.0
---

## State Bindings
- `slack.accounts` -> array
- `slack.loading` -> boolean
- `slack.error` -> string

## Layout
```clapp-layout
Column(gap=5):
  Card(title=Slack Accounts):
    Column(gap=4):
      Conditional(when=slack.loading):
        Skeleton():
      Conditional(when=!slack.loading):
        Conditional(when=slack.accounts.length):
          List(data=slack.accounts):
            AccountCard():
        Conditional(when=!slack.accounts.length):
          Heading(level=4): "No Slack accounts configured"
      IntentButton(intent=slack.addAccount, label="Add Account", variant=primary):
  Conditional(when=slack.error):
    Card(variant=destructive):
      Heading(level=4): "Error"
      MarkdownContent(content=slack.error):
```

## Intents
| Name | Payload | Description |
|------|---------|-------------|
| slack.init | `{}` | Load Slack accounts |
| slack.addAccount | `{}` | Open account creation modal |
| slack.editAccount | `{ accountId: string }` | Edit existing account |
| slack.deleteAccount | `{ accountId: string }` | Remove account |
| slack.testAccount | `{ accountId: string }` | Test connection |
| slack.saveAccount | `{ accountId: string, mode: string, botToken: string, appToken?: string, signingSecret?: string, webhookPath?: string }` | Save account config |
