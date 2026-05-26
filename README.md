# doU

**Date-stamped iterative goal execution. 6 passes. Zero dependencies.**

[![install with skills](https://skills.sh/b/nbiish/doU)](https://skills.sh/nbiish/doU)

```
RUN `date` → goal-{date}.md → # ITERATION 0 → complete prompt → ITERATION +1 → repeat until ITERATION 5
```

## What It Does

`doU` is an [Agent Skills](https://agentskills.io) standard skill that forces iterative refinement through exactly 6 passes (ITERATION 0 through ITERATION 5). Each iteration:

1. Stamps the current date via `date`
2. Appends to a date-named goal file (`goal-May 26, 2026.md`)
3. Completes the user/orchestrator prompt
4. Advances the iteration counter

This produces a visible, auditable trail of progressive refinement — each pass building on the last.

## The Snippet

```
>doU
```

When an agent encounters `>doU`, it expands to:

```
RUN `date` and append the date to a goal-May 26, 2026.md with a `# ITERATION 0` header; THEN complete the following prompt and iterate +1 upon completion until `ITERATION 5` -> """{USER_PROMPT}"""
```

## Installation

### One-command install (50+ agents)

The [skills CLI](https://github.com/vercel-labs/skills) (`npx skills`) auto-detects your installed agents and installs to all of them:

```bash
npx skills add nbiish/doU
```

Install to a specific agent:

```bash
npx skills add nbiish/doU -a claude-code
npx skills add nbiish/doU -a codex
npx skills add nbiish/doU -a cursor
npx skills add nbiish/doU -a pi
npx skills add nbiish/doU -a github-copilot
npx skills add nbiish/doU -a windsurf
npx skills add nbiish/doU -a gemini-cli
```

Install globally:

```bash
npx skills add nbiish/doU -g
```

### Manual install (any agent)

Copy or symlink the skill directory to your agent's discovery path:

| Agent | Project path | Global path |
|-------|-------------|-------------|
| **Pi** | `.pi/skills/` | `~/.pi/agent/skills/` |
| **Claude Code** | `.claude/skills/` | `~/.claude/skills/` |
| **OpenAI Codex** | `.agents/skills/` | `~/.codex/skills/` |
| **Cursor** | `.agents/skills/` | `~/.cursor/skills/` |
| **GitHub Copilot** | `.agents/skills/` | `~/.copilot/skills/` |
| **Windsurf** | `.windsurf/skills/` | `~/.codeium/windsurf/skills/` |
| **Gemini CLI** | `.agents/skills/` | `~/.gemini/skills/` |
| **Cline** | `.agents/skills/` | `~/.agents/skills/` |
| **Goose** | `.goose/skills/` | `~/.config/goose/skills/` |
| **Roo Code** | `.roo/skills/` | `~/.roo/skills/` |
| **Warp** | `.agents/skills/` | `~/.agents/skills/` |
| **Augment** | `.augment/skills/` | `~/.augment/skills/` |
| **OpenCode** | `.agents/skills/` | `~/.config/opencode/skills/` |
| **AiderDesk** | `.aider-desk/skills/` | `~/.aider-desk/skills/` |
| **Devin** | `.devin/skills/` | `~/.config/devin/skills/` |
| **Kiro** | `.kiro/skills/` | `~/.kiro/skills/` |
| **Continue** | `.continue/skills/` | `~/.continue/skills/` |
| **Junie** | `.junie/skills/` | `~/.junie/skills/` |
| **Trae** | `.trae/skills/` | `~/.trae/skills/` |
| **Any (universal)** | `.agents/skills/` | `~/.agents/skills/` |

```bash
# Example: manual install to Pi
cp -r .agents/skills/doU ~/.pi/agent/skills/doU

# Example: project-level (Pi auto-discovers from cwd)
cp -r .agents/skills/doU .agents/skills/doU
```

### Via Pi settings

```json
{
  "skills": ["path/to/doU/.agents/skills/doU"]
}
```

### Via Pi CLI

```bash
pi --skill path/to/doU/.agents/skills/doU
```

### Via package managers

```bash
# npm (agent-skills wrapper)
npm install agent-skills

# npm (Vercel skills CLI — 50+ agent support)
npx skills add nbiish/doU

# npm (rosie-skills — cross-platform skill package manager)
npx rosie-skills add nbiish/doU
```

### Via Git clone

```bash
git clone https://github.com/nbiish/doU.git
cp -r doU/.agents/skills/doU ~/.agents/skills/doU
```

## Usage

### As a standalone skill

```
>doU """Design a REST API for task management"""
```

The agent will:

1. Create `goal-May 26, 2026.md` with `# ITERATION 0`
2. Execute the prompt — first pass (initial design)
3. Append `# ITERATION 1` — refine the design
4. Append `# ITERATION 2` — add error handling, edge cases
5. Append `# ITERATION 3` — optimize, validate constraints
6. Append `# ITERATION 4` — harden, add security/compliance
7. Append `# ITERATION 5` — final review, production-ready output

### As an orchestrator input

An orchestrator agent injects the target prompt into the `"""_"""` placeholder:

```
>doU """{orchestrator_task}"""
```

### Inline (no triple quotes)

```
>doU analyze this codebase for security vulnerabilities
```

### Pi skill command

```
/skill:doU """your prompt here"""
```

## File Format

A completed `goal-May 26, 2026.md` looks like:

```markdown
# ITERATION 0
Mon May 26 14:32:01 EDT 2026

{first-pass output}

# ITERATION 1
Mon May 26 14:35:22 EDT 2026

{refined output building on iteration 0}

# ITERATION 2
Mon May 26 14:38:44 EDT 2026

{further refinement}

# ITERATION 3
Mon May 26 14:41:03 EDT 2026

{optimization pass}

# ITERATION 4
Mon May 26 14:43:55 EDT 2026

{hardening pass}

# ITERATION 5
Mon May 26 14:46:10 EDT 2026

{final production-grade output}

<!-- doU complete: 6 iterations -->
```

## Why 6 Iterations

| Pass | Purpose |
|------|---------|
| 0 | Initial execution — raw output |
| 1 | Correct errors, fill gaps |
| 2 | Refine structure and completeness |
| 3 | Optimize performance and edge cases |
| 4 | Harden security, validate constraints |
| 5 | Final review — production-ready |

6 passes is enough to go from rough draft to production-grade without diminishing returns. Fewer passes leave gaps. More passes waste cycles.

## Supported Agents

This skill works with any tool that implements the [Agent Skills](https://agentskills.io) specification. Full list of compatible agents (50+):

AiderDesk · Amp · Antigravity · Augment · Bob · Claude Code · Cline · CodeArts Agent · CodeBuddy · Codemaker · Code Studio · Codex · Command Code · Continue · Cortex Code · Crush · Cursor · Deep Agents · Devin · Dexto · Droid · Firebender · ForgeCode · Gemini CLI · GitHub Copilot · Goose · Hermes Agent · iFlow CLI · Junie · Kilo Code · Kiro CLI · Kode · MCPJam · Mistral Vibe · Mux · OpenClaw · OpenCode · OpenHands · Pi · Pochi · Qoder · Qwen Code · Replit · Rovo Dev · Roo Code · Tabnine CLI · Trae · Universal · Warp · Windsurf · Zencoder · AdaL · Neovate

## Skill Structure

```
.agents/skills/doU/
└── SKILL.md          # Agent Skills standard (agentskills.io)
```

Compliant with the [Agent Skills specification](https://agentskills.io/specification).

## Distribution Channels

| Channel | Install |
|---------|---------|
| **GitHub** | `git clone https://github.com/nbiish/doU` |
| **skills CLI** | `npx skills add nbiish/doU` |
| **skills.sh** | [![install with skills](https://skills.sh/b/nbiish/doU)](https://skills.sh/nbiish/doU) |
| **rosie-skills** | `npx rosie-skills add nbiish/doU` |
| **agent-skills (npm)** | `npm install agent-skills` |
| **Manual** | Copy `.agents/skills/doU/` to any agent's skills directory |

## License

MIT — see [LICENSE](LICENSE).
