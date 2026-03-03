---
name: claude-code
description: Claude Code agent
metadata:
  version: "0.1.0"
  strawpot:
    bin:
      macos: strawpot_claude_code
      linux: strawpot_claude_code
    install:
      macos: curl -fsSL https://raw.githubusercontent.com/strawpot/strawpot_claude_code_cli/main/strawpot_claude_code/install.sh | sh
      linux: curl -fsSL https://raw.githubusercontent.com/strawpot/strawpot_claude_code_cli/main/strawpot_claude_code/install.sh | sh
    tools:
      claude:
        description: Claude Code CLI
        install:
          macos: npm install -g @anthropic-ai/claude-code
          linux: npm install -g @anthropic-ai/claude-code
    params:
      model:
        type: string
        default: claude-sonnet-4-6
        description: Model to use for Claude Code
    env:
      ANTHROPIC_API_KEY:
        required: false
        description: Anthropic API key (optional if using Plus/Max plan)
---

# Claude Code Agent

Runs Claude Code as a subprocess. Supports interactive and non-interactive
modes, custom model selection, and skill-based prompt augmentation.
