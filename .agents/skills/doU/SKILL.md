---
name: dou
description: Date-stamped iterative goal execution across 6 passes (ITERATION 0 through 5). Use when the user says ">doU" or "run doU", asks for iterative refinement with tracking, wants to execute a prompt through multiple progressive passes, or needs a goal file with iteration history. Triggers on any request involving iterative execution with date-stamped goal files.
license: MIT
compatibility: No dependencies. Works with any agent that can execute shell commands and write files.
metadata:
  author: nbiish
  version: "1.0.0"
  trigger: ">doU"
  iterations: "6"
  spec: agentskills.io
---

# doU — Date-Stamped Iterative Goal Execution

Execute a prompt through 6 progressive refinement passes, stamping each into a date-named goal file.

## The Expansion

When you encounter `>doU`, the user's prompt goes into the placeholder:

```
>doU """{PROMPT}"""
```

If the user provides the prompt inline without triple quotes, treat their entire message after `>doU` as `{PROMPT}`.

## Execution Protocol

### Step 1: Initialize the goal file

```bash
DATE=$(date +"%b %d, %Y")
TIMESTAMP=$(date)
GOAL_FILE="goal-${DATE}.md"
```

Create or append to `goal-{date}.md` in the current working directory:

```markdown
# ITERATION 0
{TIMESTAMP}

```

### Step 2: Execute iterations 0 through 5

For each iteration N (starting at 0):

1. **Execute** the prompt fully, producing complete output
2. **Append** the output under the current `# ITERATION N` header in the goal file
3. **Reflect** on the output — what was done, what gaps remain, what the next pass should improve
4. **If N < 5:** Stamp the next iteration header and re-execute with accumulated learning:

   ```markdown
   # ITERATION {N+1}
   {new timestamp from `date`}

   ```

   Re-execute the same prompt, but incorporate all improvements and corrections identified through iterations 0–N.

5. **If N = 5:** Produce the final production-grade output, then append:

   ```markdown
   <!-- doU complete: 6 iterations -->
   ```

### Step 3: Report completion

After ITERATION 5:

```
doU complete. 6 iterations executed.
Goal file: goal-{date}.md
```

## Iteration Focus

Each pass has a specific purpose. The agent should lean into the appropriate focus for each iteration:

| Pass | Focus | What to emphasize |
|------|-------|-------------------|
| 0 | Initial execution | Produce working, complete output. Raw but functional. |
| 1 | Correction | Fix errors, fill gaps, address anything broken or missing from pass 0. |
| 2 | Refinement | Improve structure, naming, completeness, readability. Tighten the work. |
| 3 | Optimization | Performance, edge cases, error handling, robustness. |
| 4 | Hardening | Security, validation, constraints, compliance, production readiness. |
| 5 | Final review | Production-grade. Polished, documented, no loose ends. |

## Output Contract

- **File:** `goal-{date}.md` in the current working directory
- **Format:** 6 iteration sections, each with a `# ITERATION N` header, timestamp from `date`, and the output
- **Quality gradient:** Each iteration must demonstrate measurable improvement over the previous one
- **Append-only:** Never modify previous iterations. Each pass appends only.

## Constraints

- **All 6 iterations must execute.** Do not skip any.
- **Each pass must add value.** Do not repeat previous output verbatim.
- **Each pass must be timestamped** with the output of `date`.
- **If the prompt is empty**, ask the user for a prompt before starting.
- **Multiple doU calls on the same date** append to the same goal file with distinct iteration chains.

## Examples

**Basic usage:**
```
>doU """Design a REST API for task management"""
```

**Inline (no triple quotes):**
```
>doU analyze this codebase for security vulnerabilities
```

**Orchestrator delegation:**
```
>doU """{subagent_task}"""
```

## Multiple Invocations

Running `>doU` twice in one session creates two iteration chains in the same date file:

```markdown
# ITERATION 0
Mon May 26 14:32:01 EDT 2026
{first task output}

# ITERATION 1
...
<!-- doU complete: 6 iterations -->

# ITERATION 0
Mon May 26 15:01:22 EDT 2026
{second task output}

...
```

Each chain runs 0→5 independently.
