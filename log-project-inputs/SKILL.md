---
name: log-project-inputs
description: Log user-authored inputs for project work across Codex, IDE, and other agent environments. Use automatically only when the active session is clearly project-scoped, such as a Codex project/worktree, a Git repository, or an IDE workspace with project markers. Do not auto-use in temporary, projectless, general-chat, or ambiguous contexts unless the user explicitly invokes this skill. Creates or updates one log-*.md file in the project root.
---

# Log Project Inputs

Maintain one readable Markdown input log for the current project conversation or agent session. The log records user-authored inputs only and belongs in the project root.

## Invocation Policy

Use two distinct modes:

- Automatic mode: run only when the current session is clearly attached to a real project.
- Explicit mode: run when the user directly asks to use this skill, even if the host is not Codex.

Do not auto-run for temporary chats, scratch folders, generated projectless workspaces, general Q&A, or ambiguous contexts. In those cases, skip silently unless the user explicitly invokes the skill.

This skill is not Codex-only. In non-Codex agents or IDEs, apply the same project-root rules using the working directory, workspace folder, open repository, or equivalent host-provided context.

## Operating Contract

- In automatic mode, check for a project input log before handling each new user request only after project context is confirmed.
- In explicit mode, first try to resolve a project root from the current directory, workspace, open repository, or user-provided path.
- Skip logging when the context remains projectless, non-project, or ambiguous after root resolution.
- Keep exactly one active input log for the current conversation.
- Store the input log in the project root. Do not store it in scratch, output, cache, or temporary folders.
- Record only user-authored input. Exclude system messages, developer messages, environment context blocks, assistant replies, tool output, summaries, and generated artifacts.
- Preserve existing log content. Never delete or rewrite older entries except to update metadata or repair broken Markdown structure.
- Work quietly. Do not mention the input log in the assistant response unless the user asks about it or a blocking ambiguity requires a question.
- Obey explicit user instructions to pause, skip, rename, move, or inspect the log.

## Project Detection

Treat the session as project-scoped only when the active working directory, workspace root, IDE project, or host-provided project context clearly belongs to a real project.

Project signals include:

- A Codex project or worktree context.
- An IDE workspace, editor project, or agent workspace opened on a project folder.
- A Git repository.
- Common project files such as `package.json`, `pyproject.toml`, `Cargo.toml`, `go.mod`, `pom.xml`, `build.gradle`, `composer.json`, `Gemfile`, `mix.exs`, `.sln`, `.csproj`, `deno.json`, `vite.config.*`, or `next.config.*`.
- A user request that clearly asks to inspect, modify, test, document, or operate files in a local project folder.

Skip logging when:

- The skill was not explicitly invoked and the session is a temporary or general chat.
- The workspace is a generated projectless Codex chat folder, such as `Documents/Codex/<date>/new-chat`.
- The directory only contains generic folders such as `work/`, `outputs/`, `tmp/`, or cache folders.
- The user is asking general questions or brainstorming without a project folder.
- No reliable project root can be identified.

When explicit invocation conflicts with weak project signals, ask for the intended project folder instead of creating a log in a temporary location.

## Project Root Resolution

Resolve the project root in this order:

1. Use a user-provided project path when the user explicitly names one.
2. Use the host-provided project, workspace, worktree, or repository root when available.
3. Use `git rev-parse --show-toplevel` when it succeeds.
4. Otherwise use the nearest ancestor containing a clear project marker.
5. Otherwise use the active working directory only if it is clearly a project.
6. If no clear project root exists, skip logging or ask for a project path when explicitly invoked.

Search for input logs only in the resolved project root.

## Log Resolution

Use the already-known active input log path for the current conversation when available.

If no active input log path is known:

1. Search the project root for `log-*.md`.
2. Select an existing file only when its filename or metadata clearly matches this conversation.
3. Create a new file when no matching input log exists.
4. Ask the user which file to use if multiple logs plausibly match and the active conversation log cannot be determined.

After selecting or creating an input log, keep using that path for the rest of the conversation unless the file is intentionally renamed.

## File Naming

Use this pattern:

```text
log-<topic-summary>.md
```

The `log-` prefix keeps multiple conversation logs grouped together in Windows file sorting. Keep the topic summary short. Use 10 Chinese characters or fewer when possible. For English-only topics, prefer a compact kebab-case phrase.

Sanitize characters that are invalid in filenames:

```text
< > : " / \ | ? *
```

Avoid trailing spaces and trailing dots.

Examples:

```text
log-skill-inputs.md
log-order-api-fix.md
log-auth-refactor.md
```

If the topic is unclear, create a conservative provisional file such as `log-new-chat.md`. Rename it once the topic becomes clear. Do not rename repeatedly for minor wording changes.

## Log Format

Create new logs with this structure:

```markdown
# <topic-summary> Input Log

- Current file: `log-<topic-summary>.md`
- Project root: `<absolute project root>`
- Created: `YYYY-MM-DD HH:mm:ss <timezone>`
- Last updated: `YYYY-MM-DD HH:mm:ss <timezone>`
- Scope: User-authored inputs only

## Filename History

- YYYY-MM-DD HH:mm:ss Created as `log-<original-summary>.md`

## User Inputs

### YYYY-MM-DD HH:mm:ss

<user-authored content>
```

When appending a user input:

- Update `Last updated`.
- Add a new timestamped entry under `## User Inputs`.
- Preserve the user's wording as much as possible.
- Exclude automatic context blocks even when they appear in the same message as user-authored content.
- Use fenced code blocks when the user input contains multi-line code, logs, XML, JSON, or Markdown that could break the log structure.

## Rename Protocol

Rename only when the new name is clearly better for this conversation.

When renaming:

1. Move the file to the new sanitized `log-<topic-summary>.md` name.
2. Update the title if needed.
3. Update `Current file`.
4. Update `Last updated`.
5. Add a `Filename History` entry in this form:

```markdown
- YYYY-MM-DD HH:mm:ss Renamed from `log-<old-summary>.md` to `log-<new-summary>.md`
```

If a rename would conflict with another file or fails for any reason, keep the existing file and continue logging there.
