# Qwen Code Tool Mapping

Skills use Claude Code tool names. When you encounter these in a skill, use your platform equivalent:

| Skill references | Qwen Code equivalent |
|-----------------|----------------------|
| `Read` (file reading) | `read_file` |
| `Write` (file creation) | `write_file` |
| `Edit` (file editing) | `edit_file` / `str_replace` |
| `Bash` (run commands) | `execute_command` |
| `Grep` (search file content) | `search_files` |
| `Glob` (search files by name) | `list_files` |
| `TodoWrite` (task tracking) | Internal state — maintain your own checklist in chat |
| `Skill` tool (invoke a skill) | Read the skill file directly with `read_file` |
| `WebSearch` | `browser_action` or no equivalent — rely on provided context |
| `WebFetch` | `browser_action` or no equivalent |
| `Task` tool (dispatch subagent) | No equivalent — Qwen Code does not support subagents |

## No subagent support

Qwen Code has no equivalent to Claude Code's `Task` tool. Skills that rely on subagent dispatch (`subagent-driven-development`, `dispatching-parallel-agents`) will fall back to single-session execution via `executing-plans`.

When a skill says to use `subagent-driven-development`, use `superpowers:executing-plans` instead.

## Reading skills

Qwen Code does not have a native `Skill` tool. To invoke a skill:

1. Use `read_file` on the skill path (e.g. `skills/brainstorming/SKILL.md`)
2. Follow the skill's instructions directly

Browse available skills:
```bash
find skills/ -name "SKILL.md" | sort
```

Search by keyword:
```bash
grep -r "keyword" skills/ --include="SKILL.md" -l
```

## Additional Qwen Code tools

These tools are available in Qwen Code but have no Claude Code equivalent:

| Tool | Purpose |
|------|---------|
| `list_files` | List files and directories recursively |
| `browser_action` | Open URLs and interact with web pages |
| `attempt_completion` | Signal task completion with a result |
