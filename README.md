# Agent 全局配置

跨工具共享的 AI Agent 行为规则，核心文件仅 [`AGENTS.md`](./AGENTS.md)。

将本仓库放在 `~/.agents`，然后通过软链接挂到各 Agent 的全局配置位置（源一律用绝对路径 `/Users/mj/.agents/AGENTS.md`）：

| Agent | 全局配置路径 | 状态 |
|-------|-------------|------|
| Claude Code | `~/.claude/CLAUDE.md` | ✅ 已链接 |
| ZCode | `~/.zcode/AGENTS.md` | ✅ 已链接 |
| Codex | `~/.codex/AGENTS.md` | ✅ 已链接 |
| Kimi Code | `~/.kimi-code/AGENTS.md` | ✅ 已链接 |
| OpenCode | `~/.config/opencode/AGENTS.md` | ⬜ 未链接（2026-09-10 决定仅链 4 个工具，待用到时再建） |

```bash
# 已完成（2026-09-10）
ln -s /Users/mj/.agents/AGENTS.md /Users/mj/.claude/CLAUDE.md
ln -s /Users/mj/.agents/AGENTS.md /Users/mj/.zcode/AGENTS.md
ln -s /Users/mj/.agents/AGENTS.md /Users/mj/.codex/AGENTS.md
ln -s /Users/mj/.agents/AGENTS.md /Users/mj/.kimi-code/AGENTS.md

# 待用（需先创建 ~/.config/opencode 目录）
# ln -s /Users/mj/.agents/AGENTS.md /Users/mj/.config/opencode/AGENTS.md
```

修改 `~/.agents/AGENTS.md` 后，所有已链接的 Agent 在下次会话中自动生效。
