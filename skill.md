# doU — Agent Skill Definition

## Metadata

- **Name:** doU
- **Version:** 1.0.0
- **Trigger:** `>doU`
- **Type:** iterative-execution
- **Iterations:** 6 (0 through 5)

## Expansion

When the agent encounters `>doU`, expand to:

```
RUN `date` and append the date to a goal-{date}.md with a `# ITERATION 0` header; THEN complete the following prompt and iterate +1 upon completion until `ITERATION 5` -> """{PROMPT}"""
```

Where:
- `{date}` = output of `date` command, formatted for filenames (e.g., `May 26, 2026`)
- `{PROMPT}` = the user or orchestrator input, replacing the `"""_"""` placeholder

## Execution Protocol

### Step 1: Initialize

```bash
DATE=$(date +"%b %d, %Y")
TIMESTAMP=$(date)
GOAL_FILE="goal-${DATE}.md"
```

Create or append to `$GOAL_FILE`:

```markdown
# ITERATION 0
{TIMESTAMP}

```

### Step 2: Execute Iteration N (0 → 5)

For each iteration:

1. **Execute** the prompt fully
2. **Append** the output under the current iteration header
3. **Reflect** on the output:
   - What was accomplished?
   - What gaps remain?
   - What should the next iteration focus on?
4. **If N < 5:**
   - Append the next iteration header:

   ```markdown
   # ITERATION {N+1}
   {new_timestamp}

   ```

   - Execute the prompt again, incorporating all learning from iterations 0 through N
5. **If N = 5:**
   - Produce the final, production-grade output
   - Append completion marker:

   ```markdown
   <!-- doU complete: 6 iterations -->
   ```

### Step 3: Report

After ITERATION 5 completes, output a summary:

```
doU complete. 6 iterations executed.
Goal file: goal-{date}.md
```

## Input Contract

The `"""_"""` placeholder accepts any prompt string. Examples:

```
>doU """Write a Python module for SHA3-256 file hashing with chunked reading"""
>doU """Analyze this codebase for security vulnerabilities"""
>doU """Design the database schema for a multitenant SaaS platform"""
```

## Output Contract

- **File:** `goal-{date}.md` in the current working directory
- **Structure:** 6 iteration sections, each with timestamp and output
- **Quality gradient:** Each iteration must demonstrate measurable improvement over the previous

## Iteration Focus Guidelines

| Iteration | Focus |
|-----------|-------|
| 0 | Initial execution — produce working output |
| 1 | Correction — fix errors, fill gaps identified in pass 0 |
| 2 | Refinement — improve structure, naming, completeness |
| 3 | Optimization — performance, edge cases, error handling |
| 4 | Hardening — security, validation, constraints, compliance |
| 5 | Final — production-ready, reviewed, documented |

## Constraints

- Do not skip iterations. All 6 must execute.
- Do not repeat previous output verbatim. Each pass must add value.
- Do not modify previous iterations in the file. Append only.
- If the prompt is empty (`>doU """"""`), ask for a prompt before starting.
- Timestamp each iteration with `date` output.

## Compatibility

Designed for:
- Standalone agent sessions
- Orchestrator-to-agent delegation
- MCP tool chains
- Any agent that can execute shell commands and write files
