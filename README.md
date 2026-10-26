# Agent 全局配置

跨工具共享的 AI Agent 行为规则与 Claude Code subagent 定义。全局行为规则见 [`AGENTS.md`](./AGENTS.md)，subagent 源文件见 [`agents/`](./agents/)。

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

## Claude Code subagents

`agents/` 是源目录，`~/.claude/agents/` 使用逐文件软链接。模型 alias 的实际映射以 `~/.claude/settings.json` 为准。

| Agent | model / effort | 用途 |
|-------|----------------|------|
| `Explore` | `haiku` / `max` | 只读搜索代码、配置和文档 |
| `spec-reviewer` | `opus` / `max` | 审核 spec 和 tickets |
| `implementer` | `haiku` / `max` | 实现单个 ticket，或修复 review findings |
| `code-reviewer` | `opus` / `max` | 按 spec 和指定范围审核代码及复审 |

`Explore.md` 是内置 Explore 的同名覆盖：模型、effort、工具和提示词都使用本仓库的定义，不只是修改模型。

### 调用

这些定义只提供角色，不自动串成开发流水线。现有 skills（包括 `/complete-tickets`）保持原样；需要这里的分工时，在主会话中点名：

```text
用 spec-reviewer 审核 <spec> 和 <tickets>
用 implementer 按 <spec> 完成 <ticket>
用 code-reviewer 按 <spec> 和 <tickets> 审核 <改动范围>
```

代码 findings 交给 `implementer` 修复，再由 `code-reviewer` 复审；spec/tickets findings 交回主会话和用户修改。同一阶段最多两轮修复，仍有阻塞问题就暂停。

### 链接记录（2026-10-26）

```bash
ln -s /Users/mj/.agents/agents/Explore.md /Users/mj/.claude/agents/Explore.md
ln -s /Users/mj/.agents/agents/spec-reviewer.md /Users/mj/.claude/agents/spec-reviewer.md
ln -s /Users/mj/.agents/agents/implementer.md /Users/mj/.claude/agents/implementer.md
ln -s /Users/mj/.agents/agents/code-reviewer.md /Users/mj/.claude/agents/code-reviewer.md
```

首次新建 `~/.claude/agents` 目录后需要重启 Claude Code；目录已被监视后，新增或修改定义会自动加载。
