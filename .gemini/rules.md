# Antigravity Token Optimization Directives for HTML Resume Workspace

## 1. Response Output Rules (Prevent Output Token Drain)
- DO NOT dump or print full HTML, CSS, or file contents into chat responses.
- After making edits, report ONLY:
  - The specific file modified.
  - A 2–4 bullet high-level summary of changes (e.g., keywords replaced, sections tailored).
  - The exact line range affected.
- Never show raw terminal diffs or full code blocks unless explicitly requested with: "show full code" or "print in terminal".
- Never show Summary of Changes unless explicitly requested

## 2. File Reading & Editing Rules (Prevent Context Inflation)
- NEVER read entire HTML files if only inspecting specific sections. Always use targeted line ranges (`StartLine` and `EndLine`) with `view_file`.
- NEVER rewrite entire files with `write_to_file` for minor edits; always use surgical edits (`replace_file_content`) to minimize input/output payload.
- Do not re-read files that are already present in recent context unless changes were made externally.

## 3. Command Execution Rules (Prevent Command Output Bloat)
- Never run unconstrained directory listings, recursive scans, or commands that output full file streams (e.g., avoid unbounded `git log`, `Get-Content`, `type`, or `cat`).
- Use minimal flags for git operations:
  - Use `git status --porcelain` instead of full status.
  - Use `git log -n 3 --oneline` instead of full log.
- Do not run unsolicited inspection commands (such as `git diff`) that consume tokens with large diff outputs.

## 4. Workflow & Agent Execution Rules
- Do NOT spawn subagents for single-file tasks, resume tailoring, or simple edits within this workspace.
- Keep all explanations concise, technical, and directly focused on the requested action.
- When performing resume tailoring from a job description:
  1. Read only `jobDesc.md` and the targeted sections of the resume.
  2. Apply edits surgically.
  3. Confirm completion in under 5 lines of text.
