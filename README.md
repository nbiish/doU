# doU

**Date-stamped iterative goal execution. 6 passes. Zero config.**

```
RUN `date` → goal-{date}.md → # ITERATION 0 → complete prompt → ITERATION +1 → repeat until ITERATION 5
```

## What It Does

`doU` is an agent skill standardization that forces iterative refinement through exactly 6 passes (ITERATION 0 through ITERATION 5). Each iteration:

1. Stamps the current date
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

### Multiple goals in one session

Each `>doU` invocation creates or appends to its own date-stamped file. Running two `doU` calls on the same day appends to the same file with distinct iteration chains.

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
```

## Skill Definition

See [`skill.md`](skill.md) for the agent-consumable skill definition.

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

## License

See [LICENSE](LICENSE).
