---
name: project-chatlog
description: Maintain one Markdown chatlog for each Codex project conversation. Use at the start of every project-scoped conversation and before handling each user turn to create, select, and update a single *-chatlog.md file in the project root, recording only user-authored inputs with timestamps. Skip projectless and non-project chats.
---

# Project Chatlog

Maintain one readable Markdown log for the current project conversation. The log records user-authored inputs only and belongs in the project root.

## Operating Contract

- Check for a project chatlog before handling each new user request.
- Skip logging when the conversation is projectless, non-project, or ambiguous.
- Keep exactly one active chatlog for the current conversation.
- Store the chatlog in the project root. Do not store it in scratch, output, cache, or temporary folders.
- Record only user-authored input. Exclude system messages, developer messages, environment context blocks, assistant replies, tool output, summaries, and generated artifacts.
- Preserve existing log content. Never delete or rewrite older entries except to update metadata or repair broken Markdown structure.
- Work quietly. Do not mention the chatlog in the assistant response unless the user asks about it or a blocking ambiguity requires a question.
- Obey explicit user instructions to pause, skip, rename, move, or inspect the log.

## Project Detection

Treat the conversation as project-scoped only when the active working directory or workspace root clearly belongs to a real project.

Project signals include:

- A Git repository.
- Common project files such as `package.json`, `pyproject.toml`, `Cargo.toml`, `go.mod`, `pom.xml`, `build.gradle`, `composer.json`, `Gemfile`, `mix.exs`, `.sln`, `.csproj`, `deno.json`, `vite.config.*`, or `next.config.*`.
- A user request that clearly asks to inspect, modify, test, document, or operate files in a local project folder.

Skip logging when:

- The workspace is a generated projectless Codex chat folder, such as `Documents/Codex/<date>/new-chat`.
- The directory only contains generic folders such as `work/` and `outputs/`.
- The user is asking general questions or brainstorming without a project folder.
- No reliable project root can be identified.

## Project Root Resolution

Resolve the project root in this order:

1. Use `git rev-parse --show-toplevel` when it succeeds.
2. Otherwise use the nearest ancestor containing a clear project marker.
3. Otherwise use the active workspace root only if it is clearly a project.
4. If no clear project root exists, skip logging.

Search for chatlogs only in the resolved project root.

## Chatlog Resolution

Use the already-known active chatlog path for the current conversation when available.

If no active chatlog path is known:

1. Search the project root for `*-chatlog.md`.
2. Select an existing file only when its filename or metadata clearly matches this conversation.
3. Create a new file when no matching chatlog exists.
4. Ask the user which file to use if multiple chatlogs plausibly match and the active conversation log cannot be determined.

After selecting or creating a chatlog, keep using that path for the rest of the conversation unless the file is intentionally renamed.

## File Naming

Use this pattern:

```text
<topic-summary>-chatlog.md
```

Keep the topic summary short. Use 10 Chinese characters or fewer when possible. For English-only topics, prefer a compact kebab-case phrase.

Sanitize characters that are invalid in filenames:

```text
< > : " / \ | ? *
```

Avoid trailing spaces and trailing dots.

Examples:

```text
skill-log-chatlog.md
order-api-fix-chatlog.md
auth-refactor-chatlog.md
```

If the topic is unclear, create a conservative provisional file such as `new-chat-chatlog.md`. Rename it once the topic becomes clear. Do not rename repeatedly for minor wording changes.

## Log Format

Create new logs with this structure:

```markdown
# <topic-summary> Chatlog

- Current file: `<topic-summary>-chatlog.md`
- Project root: `<absolute project root>`
- Created: `YYYY-MM-DD HH:mm:ss <timezone>`
- Last updated: `YYYY-MM-DD HH:mm:ss <timezone>`
- Scope: User-authored inputs only

## Filename History

- YYYY-MM-DD HH:mm:ss Created as `<original-name>-chatlog.md`

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

1. Move the file to the new sanitized name.
2. Update the title if needed.
3. Update `Current file`.
4. Update `Last updated`.
5. Add a `Filename History` entry in this form:

```markdown
- YYYY-MM-DD HH:mm:ss Renamed from `<old-name>-chatlog.md` to `<new-name>-chatlog.md`
```

If a rename would conflict with another file or fails for any reason, keep the existing file and continue logging there.
