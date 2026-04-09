# TrenchClaw

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Built With: Go](https://img.shields.io/badge/Built%20With-Go-00ADD8?logo=go&logoColor=white)](https://go.dev/)
[![Interface: CLI Agent](https://img.shields.io/badge/Interface-CLI%20Agent-F97316)](#quick-start)
[![Channel: Telegram](https://img.shields.io/badge/Channel-Telegram-26A5E4?logo=telegram&logoColor=white)](./trenchclaw/docs/channels/telegram/README.md)
[![Gateway: Enabled](https://img.shields.io/badge/Gateway-Multi--Channel-111827)](#channel-integrations)

<p align="center">
  <img src="./trenchclaw/assets/agent-avatar.png" alt="TrenchClaw cyborg avatar" width="260" />
</p>

TrenchClaw is a lightweight AI agent focused on practical work: direct chat in the terminal, configurable model providers, workspace memory, skills, scheduled jobs, and message-based integrations such as Telegram and Discord.

This repository contains the TrenchClaw project workspace and the agent core in [`trenchclaw/`](./trenchclaw).

## What The Agent Can Do

- Chat directly in the terminal with a configurable default model
- Run in multiple interfaces: terminal agent, web console, and TUI dashboard
- Connect to external channels such as Telegram, Discord, Slack, Matrix, LINE, QQ, Weixin, DingTalk, Feishu, and more
- Use multiple model providers through a model-centric configuration
- Manage reusable skills for specialized workflows
- Keep workspace context with files such as `AGENT.md`, `USER.md`, `SOUL.md`, and `MEMORY.md`
- Schedule recurring work with built-in cron commands
- Expose a gateway process for always-on or multi-channel agent operation

## Repository Layout

- [`README.md`](./README.md): GitHub landing page and quick start
- [`trenchclaw/`](./trenchclaw): Agent source code, docs, workspace scaffold, and packaging
- [`trenchclaw/docs/`](./trenchclaw/docs): Provider, channel, and architecture docs
- [`trenchclaw/workspace/`](./trenchclaw/workspace): Default workspace identity, memory, and tool instructions

## Quick Start

The shortest path is: build once, run onboarding once, set a default model, then use `trenchclaw`.

### 1. Build the CLI

From the repository root:

```bash
cd trenchclaw
go build -o trenchclaw ./cmd/trenchlaw
```

### 2. Run onboarding

```bash
./trenchclaw onboard
```

This creates the local config and workspace files. `install` is an alias:

```bash
./trenchclaw install
```

### 3. Set a default model

You can do this during onboarding or later with the CLI:

```bash
./trenchclaw auth login
./trenchclaw auth status
./trenchclaw model
./trenchclaw model gpt-5.4
```

If you prefer editing config directly, add a model entry such as:

```json
{
  "model_name": "gpt-5.4",
  "model": "openai/gpt-5.4",
  "api_key": "sk-..."
}
```

Provider setup details are in [`trenchclaw/docs/providers.md`](./trenchclaw/docs/providers.md).

### 4. Start the agent

For normal use:

```bash
./trenchclaw
```

If onboarding is complete, the interactive launcher lets you choose:

- Terminal Agent
- Web Console
- TUI Dashboard

If you want the terminal agent directly:

```bash
./trenchclaw agent
./trenchclaw agent -m "Summarize the repository and suggest next steps"
```

Useful checks:

```bash
./trenchclaw status
./trenchclaw version
```

## Most Used Commands

Use these first before exploring the rest of the CLI:

```bash
./trenchclaw onboard      # first-time setup
./trenchclaw              # launcher: agent, web, or tui
./trenchclaw agent        # terminal agent directly
./trenchclaw auth login   # connect a provider
./trenchclaw model        # list or set the default model
./trenchclaw status       # confirm config and runtime state
./trenchclaw gateway      # run integrations and long-lived channels
./trenchclaw skills list  # inspect installed skills
./trenchclaw cron list    # inspect scheduled jobs
```

## Interfaces

`trenchclaw` is the default entry point.

- `trenchclaw`: opens the startup selector in an interactive terminal
- `trenchclaw agent`: skips the selector and starts terminal chat
- `trenchclaw gateway`: runs the always-on gateway for channels and automations

If setup is incomplete, `trenchclaw` sends you to onboarding first. If no default model is configured, `trenchclaw agent` tells you to finish setup or choose a model.

## Channel Integrations

TrenchClaw can operate across external messaging platforms through the gateway.

Documented channel:

- Telegram

Start the gateway with:

```bash
./trenchclaw gateway
```

Channel setup docs:

- [`trenchclaw/docs/channels/telegram/README.md`](./trenchclaw/docs/channels/telegram/README.md)
- [`trenchclaw/docs/channels/discord/README.md`](./trenchclaw/docs/channels/discord/README.md)
- [`trenchclaw/docs/channels/slack/README.md`](./trenchclaw/docs/channels/slack/README.md)

## Skills, Memory, And Workspace Customization

The workspace is part of the agent design. TrenchClaw ships with editable workspace files that define identity, memory, tools, and user-specific context.

Important files:

- [`trenchclaw/workspace/AGENT.md`](./trenchclaw/workspace/AGENT.md)
- [`trenchclaw/workspace/USER.md`](./trenchclaw/workspace/USER.md)
- [`trenchclaw/workspace/SOUL.md`](./trenchclaw/workspace/SOUL.md)
- [`trenchclaw/workspace/TOOLS.md`](./trenchclaw/workspace/TOOLS.md)
- [`trenchclaw/workspace/memory/MEMORY.md`](./trenchclaw/workspace/memory/MEMORY.md)

Skill management commands:

```bash
./trenchclaw skills list
./trenchclaw skills search git
./trenchclaw skills install <github-repo>
./trenchclaw skills remove <skill-name>
```

## Scheduling And Automation

TrenchClaw includes built-in cron support for recurring work.

Examples:

```bash
./trenchclaw cron list
./trenchclaw cron add
./trenchclaw cron enable <job-id>
./trenchclaw cron disable <job-id>
./trenchclaw cron remove <job-id>
```

## Documentation

- Provider setup: [`trenchclaw/docs/providers.md`](./trenchclaw/docs/providers.md)
- Hooks: [`trenchclaw/docs/hooks/README.md`](./trenchclaw/docs/hooks/README.md)
- Agent refactor notes: [`trenchclaw/docs/agent-refactor/README.md`](./trenchclaw/docs/agent-refactor/README.md)
- Chat app docs: [`trenchclaw/docs/chat-apps.md`](./trenchclaw/docs/chat-apps.md)

## Notes

- The package metadata inside `trenchclaw/` still references `trenchlaw` in several places. The current repo name and top-level project presentation use `TrenchClaw`.
- `.DS_Store` files are currently modified in the repository and were not changed by this README update.
