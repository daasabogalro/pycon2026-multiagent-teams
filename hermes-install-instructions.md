# Installation Instructions: Hermes Agent

Resources used:
- [Hermes Agent docs](https://hermes-agent.nousresearch.com/docs/)
- [Installation guide](https://hermes-agent.nousresearch.com/docs/getting-started/installation)
- [Slash commands reference](https://hermes-agent.nousresearch.com/docs/reference/slash-commands)

## Install

Go to the [Hermes website](https://hermes-agent.nousresearch.com/) and download the installer,
or install it via terminal:

```bash
curl -fsSL https://hermes-agent.nousresearch.com/install.sh | bash
```

## Setup wizard

After installation you'll be prompted to select a model provider or introduce an API key.
If installing via terminal, select the **Full Setup** option.

Then select the **"Anthropic API Key"** option and paste your Anthropic API key (use the key
provided to you for this workshop, or your own):

```bash
<ANTHROPIC_API_KEY>
```

After pasting the key, select **Sonnet 5** as the default model — it has introductory pricing
of $2/M tokens through August 31, 2026. Then select **Keep current (local)** as the terminal
backend.

## First run

If you're using the CLI, reload your shell so the `hermes` command is available:

```bash
source ~/.bashrc
```

or

```bash
source ~/.zshrc
```

Then run `hermes` to start the agent.

Run `hermes doctor` to confirm everything's healthy before the workshop starts.

## Frequent-use CLI commands

| Command | Description |
| --- | --- |
| `hermes` | Start the chat TUI |
| `hermes -c` | Continue last session |
| `hermes model` | Switch provider / model |
| `hermes status` | Gateway + cron + provider health |
| `hermes insights` | Tokens, costs, activity |
| `hermes sessions browse` | Pick a session to resume |
| `hermes skills browse` | Discover + install skills |
| `hermes config show` | See your current settings |
| `hermes doctor` | Health check + fix hints |
| `hermes update` | Pull latest version of Hermes |

## Handy slash commands (inside the TUI)

| Command | Description |
| --- | --- |
| `/kanban <action>` | Drive the collaboration board from chat — this is the shared board multi-agent runs coordinate through |
| `/agents` / `/tasks` | Show active agents and tasks — useful for watching a team work in real time |
| `/status` | Session info and recap |
| `/model [name]` | Show or switch the current model |
| `/usage` | Token usage and cost breakdown for the session |
| `/tools [action]` | List, disable, or enable tools |
| `/skills` | Search, install, inspect, or manage skills |
| `/debug` | Upload a debug report if something goes wrong |
| `/help` | Display help |
| `/quit` | Exit the CLI |

Full reference: [Slash Commands Reference](https://hermes-agent.nousresearch.com/docs/reference/slash-commands).
