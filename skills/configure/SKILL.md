---
name: remo-code:configure
description: Configure the Remo Code hub connection with your API key
arguments:
  - name: api_key
    description: "Your API key (starts with remokey_). Generate one at Settings > API Key in your Remo Code web UI."
    required: true
  - name: hub_url
    description: "Your Remo Code hub URL (default: https://app.remo-code.com)"
    required: false
---

# /remo-code:configure

Save the API key so the channel plugin can auto-register sessions. Each project directory gets its own session automatically.

## Steps

1. Create the config directory at `~/.claude/channels/remo-code/` if it doesn't exist
2. Load existing `state.json` or create a new one
3. Set `api_key` to `$ARGUMENTS` (the first argument — the remokey_ value)
4. Set `hub_url` to the second argument if provided, otherwise default to `https://app.remo-code.com`
5. Verify the key works by calling `GET {hub_url}/api/plugin/verify` with header `Authorization: Bearer {api_key}`
6. If verification succeeds (200), save `state.json` with permissions 600
7. If verification fails (401), tell the user the key is invalid

## state.json format

Write this to `~/.claude/channels/remo-code/state.json`:

```json
{
  "hub_url": "{hub_url}",
  "api_key": "{api_key}",
  "sessions": {}
}
```

After writing, set permissions:
```bash
chmod 600 ~/.claude/channels/remo-code/state.json
```

## On success

Tell the user:
> Configuration saved and verified. Restart Claude Code with the channel enabled:
> ```
> claude --dangerously-load-development-channels plugin:remo-code@remo-code-channel
> ```
> Sessions will be auto-created for each project directory — no manual token setup needed.
