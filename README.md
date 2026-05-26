# doU

**Date-stamped iterative goal execution. 6 passes. Zero dependencies.**

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

### Pi / Claude Code / Codex / Any Agent Skills-compatible tool

Copy or symlink the skill directory to any agent's skill discovery path:

```bash
# Cross-platform standard location (Pi, and others)
cp -r .agents/skills/doU ~/.agents/skills/doU

# Pi-specific
cp -r .agents/skills/doU ~/.pi/agent/skills/doU

# Claude Code
cp -r .agents/skills/doU ~/.claude/skills/doU

# OpenAI Codex
cp -r .agents/skills/doU ~/.codex/skills/doU

# Project-level (Pi discovers from cwd ancestors)
cp -r .agents/skills/doU .agents/skills/doU
```

### Via Pi settings

Add to `~/.pi/settings.json` or `.pi/settings.json`:

```json
{
  "skills": ["path/to/doU/.agents/skills/doU"]
}
```

### Via Pi CLI

```bash
pi --skill path/to/doU/.agents/skills/doU
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

## Skill Structure

```
.agents/skills/doU/
└── SKILL.md          # Agent Skills standard (agentskills.io)
```

Compliant with the [Agent Skills specification](https://agentskills.io/specification). Loads in Pi, Claude Code, OpenAI Codex, and any tool that implements the standard.

## License

MIT — see [LICENSE](LICENSE).
