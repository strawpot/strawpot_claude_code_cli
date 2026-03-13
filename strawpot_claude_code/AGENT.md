---
name: strawpot-claude-code
description: Claude Code agent
metadata:
  strawpot:
    bin:
      macos: strawpot_claude_code
      linux: strawpot_claude_code
    install:
      macos: curl -fsSL https://raw.githubusercontent.com/strawpot/strawpot_claude_code_cli/main/strawpot_claude_code/install.sh | sh
      linux: curl -fsSL https://raw.githubusercontent.com/strawpot/strawpot_claude_code_cli/main/strawpot_claude_code/install.sh | sh
    tools:
      npm:
        description: Node.js package manager (https://nodejs.org)
      claude:
        description: Claude Code CLI
        install:
          macos: npm install -g @anthropic-ai/claude-code
          linux: npm install -g @anthropic-ai/claude-code
    params:
      model:
        type: string
        description: Model override (omit to use claude CLI default)
      dangerously_skip_permissions:
        type: boolean
        default: true
        description: Skip permission prompts (enabled by default, set to false to require approval)
    env:
      ANTHROPIC_API_KEY:
        required: false
        description: Anthropic API key (optional if using Plus/Max plan)
---

# Claude Code Agent

Runs Claude Code as a subprocess. Supports interactive and non-interactive
modes, custom model selection, and skill-based prompt augmentation.
