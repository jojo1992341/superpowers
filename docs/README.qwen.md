# Superpowers for Qwen Code

Guide for using Superpowers with [Qwen Code](https://github.com/QwenLM/qwen-code).

## Quick Install

Tell Qwen Code:
```
Fetch and follow instructions from https://raw.githubusercontent.com/obra/superpowers/refs/heads/main/docs/README.qwen.md
```

## Manual Installation

### Prerequisites

- Qwen Code CLI installed
- Git

### Steps

1. Clone the repository into your project or home config:
```bash
git clone https://github.com/obra/superpowers.git ~/.qwen/superpowers
```

2. Copy or link `QWEN.md` to your project root:
```bash
# Option A — symlink (updates automatically with git pull)
ln -s ~/.qwen/superpowers/QWEN.md ./QWEN.md

# Option B — copy (static snapshot)
cp ~/.qwen/superpowers/QWEN.md ./QWEN.md
```

Qwen Code automatically reads `QWEN.md` at session start and injects its contents into the system context.

3. Verify by starting a new session — you should see Qwen Code acknowledge superpowers skills.

### Global installation (all projects)

If Qwen Code supports a global context file, place `QWEN.md` in the config directory:
```bash
mkdir -p ~/.config/qwen-code
cp ~/.qwen/superpowers/QWEN.md ~/.config/qwen-code/QWEN.md
```

## How It Works

`QWEN.md` uses Qwen Code's `@file` import syntax to load two files at session start:

1. `skills/using-superpowers/SKILL.md` — the core skill discovery and usage instructions
2. `skills/using-superpowers/references/qwen-tools.md` — tool name mapping for Qwen Code

This mirrors the same pattern used for Gemini CLI (`GEMINI.md`).

## Usage

### Finding skills
```bash
find ~/.qwen/superpowers/skills -name "SKILL.md" | sort
```

Or ask Qwen Code:
```
List the available superpowers skills.
```

### Loading a skill

Tell Qwen Code to read a skill file:
```
Read and follow skills/brainstorming/SKILL.md
```

Or instruct it directly:
```
Use the superpowers brainstorming skill to help me design this feature.
```

### Tool mapping

Qwen Code uses different tool names than Claude Code. The mapping is loaded automatically from `qwen-tools.md`. Key differences:

- `Skill` tool → `read_file` on the skill's `SKILL.md`
- `Task` (subagents) → not supported; use `executing-plans` instead
- `TodoWrite` → maintain a checklist in your chat context
- `Bash` → `execute_command`

## Limitations

- **No subagent support** — `subagent-driven-development` and `dispatching-parallel-agents` fall back to `executing-plans`
- **No native skill tool** — skills are loaded by reading files directly
- **No automatic skill discovery** — skills must be referenced by path

## Updating
```bash
cd ~/.qwen/superpowers && git pull
```

If you used a symlink in step 2, `QWEN.md` updates automatically. If you copied it, re-copy after updates.

## Uninstalling
```bash
rm ~/.qwen/superpowers
rm ./QWEN.md  # or ~/.config/qwen-code/QWEN.md
```

## Getting Help

- Report issues: https://github.com/obra/superpowers/issues
- Qwen Code docs: https://github.com/QwenLM/qwen-code
