# Remo Code Channel Plugin

A [Claude Code channel plugin](https://code.claude.com/docs/en/channels) that bridges your local Claude Code session to the [Remo Code](https://remo-code.com) hub for remote chat access via any browser or phone.

## How It Works

This plugin runs as an MCP server inside your Claude Code session. It connects outbound to your Remo Code hub via WebSocket and:

- Receives messages from the web UI as `<channel source="remo-code">` events
- Lets Claude reply back through the `reply` tool
- Reports session status (online/thinking/offline) in real-time
- Supports message editing and emoji reactions

## Install

```
/plugin install remo-code@claude-plugins-official
```

If not found, first add the marketplace:
```
/plugin marketplace add anthropics/claude-plugins-official
```

## Configure

### Option A: Use the configure skill

```
/remo-code:configure https://remo-code.com remo_YOUR_TOKEN
```

### Option B: Manual setup

Create `~/.claude/channels/remo-code/.env`:

```
HUB_URL=https://remo-code.com
HUB_TOKEN=remo_YOUR_TOKEN
SESSION_ID=my-project
```

## Run

Restart Claude Code with the channel enabled:

```bash
claude --channels plugin:remo-code@claude-plugins-official
```

During development (before official approval):

```bash
claude --dangerously-load-development-channels plugin:remo-code@claude-plugins-official
```

## Getting a Token

1. Sign in at [remo-code.com](https://remo-code.com) (or your self-hosted hub)
2. Click **+ New Session** in the sidebar
3. Copy the token from the connect modal

## Requirements

- [Bun](https://bun.sh) runtime
- [Claude Code](https://claude.ai/code) v2.1.80+
- A Remo Code hub account ([remo-code.com](https://remo-code.com) or self-hosted)

## License

Apache-2.0
