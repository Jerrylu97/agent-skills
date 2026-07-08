# Log Project Inputs Skill

English | [中文](#中文)

A small Codex skill that keeps one Markdown input log for each project conversation.

The skill is intentionally instruction-only. It has no scripts, assets, or external dependencies. When invoked in a real project, it creates or updates a single `log-*.md` file in the project root and records only user-authored inputs with timestamps. It skips projectless and non-project conversations.

## Features

- Maintains exactly one active input log per project conversation.
- Stores the log in the resolved project root.
- Records user-authored inputs only.
- Excludes assistant replies, system/developer messages, environment context, and tool output.
- Skips generated projectless Codex chat folders.
- Uses `log-<summary>.md` filenames so multiple logs sort together in Windows.
- Supports short topic-based filenames and controlled renaming.

## Repository Layout

```text
log-project-inputs/
  SKILL.md
  agents/
    openai.yaml
```

Only `log-project-inputs/` is the installable skill folder. The root `README.md`, `LICENSE`, `.gitattributes`, and `.gitignore` files are repository metadata.

## Installation

Clone or download this repository, then copy the `log-project-inputs` folder into your Codex skills directory:

```text
~/.codex/skills/log-project-inputs
```

On Windows, the equivalent path is commonly:

```text
C:\Users\<you>\.codex\skills\log-project-inputs
```

Restart Codex or refresh skill discovery after installation.

## Privacy Notes

This skill writes local Markdown logs inside project folders. Those logs may contain the user's own prompts, including sensitive project details if the user typed them. Review generated `log-*.md` files before committing or sharing a project repository.

The repository `.gitignore` ignores `log-*.md` to reduce accidental commits when testing this skill.

## License

MIT

---

## 中文

一个用于 Codex 的轻量 skill：为每个项目对话维护一个 Markdown 格式的用户输入日志。

这个 skill 只包含指令，不包含脚本、素材或外部依赖。当它在真实项目中被触发时，会在项目根目录创建或更新一个 `log-*.md` 文件，并只记录用户主动输入的内容和时间戳。非项目对话和 projectless 对话会被跳过。

## 功能

- 每个项目对话只维护一个活跃输入日志。
- 日志保存在识别到的项目根目录。
- 只记录用户主动输入。
- 不记录 assistant 回复、system/developer 消息、环境上下文和工具输出。
- 跳过 Codex 自动生成的 projectless 对话目录。
- 使用 `log-<概述>.md` 文件名，让多个日志在 Windows 排序中聚在一起。
- 支持短主题文件名和受控重命名。

## 仓库结构

```text
log-project-inputs/
  SKILL.md
  agents/
    openai.yaml
```

只有 `log-project-inputs/` 是可安装的 skill 文件夹。根目录的 `README.md`、`LICENSE`、`.gitattributes` 和 `.gitignore` 是开源仓库元数据。

## 安装

克隆或下载本仓库，然后把 `log-project-inputs` 文件夹复制到 Codex 的 skills 目录：

```text
~/.codex/skills/log-project-inputs
```

Windows 上通常是：

```text
C:\Users\<you>\.codex\skills\log-project-inputs
```

安装后重启 Codex，或刷新 skill discovery。

## 隐私说明

这个 skill 会在项目文件夹中写入本地 Markdown 日志。日志可能包含用户自己输入的项目细节，甚至敏感内容。提交或分享项目仓库前，请检查生成的 `log-*.md` 文件。

本仓库的 `.gitignore` 已忽略 `log-*.md`，用于降低测试时误提交日志的风险。

## 许可证

MIT
