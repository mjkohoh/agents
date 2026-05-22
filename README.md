# Agent 全局配置

跨工具共享的 AI Agent 行为规则，核心文件仅 [`AGENTS.md`](./AGENTS.md)。

将本仓库放在 `~/.agents`，然后通过软链接挂到各 Agent 的全局配置位置：

| Agent | 全局配置路径 |
|-------|-------------|
| OpenCode | `~/.config/opencode/AGENTS.md` |
| Claude Code | `~/.claude/CLAUDE.md` |
| Codex | `~/.codex/AGENTS.md` |

```bash
ln -s ~/.agents/AGENTS.md ~/.config/opencode/AGENTS.md
ln -s ~/.agents/AGENTS.md ~/.claude/CLAUDE.md
ln -s ~/.agents/AGENTS.md ~/.codex/AGENTS.md
```

修改 `~/.agents/AGENTS.md` 后，所有已链接的 Agent 在下次会话中自动生效。
