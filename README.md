# StrawPot Claude Code CLI

A Go wrapper that translates [StrawPot](https://github.com/strawpot) protocol arguments into [Claude Code](https://docs.anthropic.com/en/docs/claude-code) CLI flags. It acts as a pure translation layer — process management, sessions, and infrastructure are handled by StrawPot core.

## Prerequisites

- [Claude Code CLI](https://www.npmjs.com/package/@anthropic-ai/claude-code) (`npm install -g @anthropic-ai/claude-code`)
- An Anthropic API key (or a Claude Pro/Max plan)

## Installation

```sh
curl -fsSL https://raw.githubusercontent.com/strawpot/strawpot_claude_code_cli/main/strawpot_claude_code/install.sh | sh
```

This downloads a pre-built binary for your platform (macOS/Linux, amd64/arm64) to `/usr/local/bin`. Override the install directory with `INSTALL_DIR`:

```sh
INSTALL_DIR=~/.local/bin curl -fsSL ... | sh
```

## Usage

The wrapper exposes two subcommands:

### `setup`

Runs `claude /login` to authenticate with Anthropic.

```sh
strawpot_claude_code setup
```

### `build`

Translates StrawPot protocol flags into a Claude Code command and outputs it as JSON.

```sh
strawpot_claude_code build \
  --agent-workspace-dir /path/to/workspace \
  --working-dir /path/to/project \
  --task "fix the bug" \
  --config '{"model":"claude-opus-4-6"}'
```

Output:

```json
{
  "cmd": ["claude", "-p", "fix the bug", "--system-prompt", "/path/to/workspace/prompt.md", "--model", "claude-opus-4-6", "--dangerously-skip-permissions", "--add-dir", "/path/to/workspace"],
  "cwd": "/path/to/project"
}
```

#### Build flags

| Flag | Required | Description |
|---|---|---|
| `--agent-workspace-dir` | Yes | Workspace directory (used as `--add-dir`) |
| `--working-dir` | No | Working directory for the command (`cwd` in output) |
| `--task` | No | Task prompt (passed as `claude -p`) |
| `--config` | No | JSON config object (default: `{}`) |
| `--role-prompt` | No | Role prompt text (written to `prompt.md`) |
| `--memory-prompt` | No | Memory/context prompt (appended to `prompt.md`) |
| `--skills-dir` | No | Directory with skill subdirectories (symlinked to `.claude/skills/`) |
| `--roles-dir` | No | Directory with role subdirectories (repeatable, symlinked to `roles/`) |
| `--agent-id` | No | Agent identifier |

## Configuration

### Config JSON

Pass via `--config`:

| Key | Type | Default | Description |
|---|---|---|---|
| `model` | string | `claude-sonnet-4-6` | Model to use |
| `dangerously_skip_permissions` | boolean | `true` | Skip permission prompts. Set to `false` to require approval for each action. |

### Environment variables

| Variable | Description |
|---|---|
| `ANTHROPIC_API_KEY` | Anthropic API key (optional if using Plus/Max plan) |
| `PERMISSION_MODE` | Permission mode passed to `--permission-mode` (e.g. `auto`) |

## Development

```sh
cd claude_code/wrapper
go test -v ./...
```

Releases are built with [GoReleaser](https://goreleaser.com/) and published automatically via GitHub Actions.

## License

See [LICENSE](LICENSE) for details.
