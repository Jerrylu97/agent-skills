# Agent Skills

English | [中文](#中文)

A public collection of small, practical skills for AI coding agents and assistant workflows.

This repository is intentionally organized as a dedicated skill collection. Each skill lives in its own top-level folder and keeps only the files required for that skill to work. Repository-level files document the collection, licensing, and contribution shape.

## Skills

| Skill | Summary |
| --- | --- |
| [`log-project-inputs`](log-project-inputs) | Logs user-authored inputs for project sessions into one `log-*.md` file in the project root. |
| [`reason-across-languages`](reason-across-languages) | Improves reasoning and output-language routing for Chinese, English, and mixed-language requests. |

## Repository Layout

```text
log-project-inputs/
  SKILL.md
  agents/
    openai.yaml
reason-across-languages/
  SKILL.md
  agents/
    openai.yaml
```

Each top-level skill directory is intended to be independently installable when the target agent supports that skill format.

## Installing A Skill

Clone or download this repository, then copy the skill folder you want into the relevant agent's skills directory.

For Codex, install `log-project-inputs` like this:

```text
~/.codex/skills/log-project-inputs
```

On Windows, the equivalent path is commonly:

```text
C:\Users\<you>\.codex\skills\log-project-inputs
```

Restart the agent or refresh skill discovery after installation.

## Privacy Notes

Some skills may write local files or process project content. Review each skill's `SKILL.md` before use, and review generated files before committing or sharing a project repository.

The repository `.gitignore` currently ignores `log-*.md` to reduce accidental commits when testing `log-project-inputs`.

## License

MIT

---

## 中文

一个公开的 AI agent skills 集合，收录小而实用的 agent 技能和工作流增强。

这个仓库刻意设计成一个专门的 skill 集合，而不是单个 skill 项目。每个 skill 都直接放在仓库根目录下自己的文件夹中，并且只保留运行该 skill 所需的文件。仓库根目录负责说明集合定位、许可证和后续扩展方式。

## Skill 清单

| Skill | 简介 |
| --- | --- |
| [`log-project-inputs`](log-project-inputs) | 将项目会话中的用户主动输入记录到项目根目录的一个 `log-*.md` 文件中。 |
| [`reason-across-languages`](reason-across-languages) | 为中文、英文和混合语言请求增强推理质量，并按用户意图控制输出语言。 |

## 仓库结构

```text
log-project-inputs/
  SKILL.md
  agents/
    openai.yaml
reason-across-languages/
  SKILL.md
  agents/
    openai.yaml
```

每个顶层 skill 目录都应当能在对应 agent 支持该 skill 格式时独立安装。

## 安装某个 Skill

克隆或下载本仓库，然后把需要的 skill 文件夹复制到对应 agent 的 skills 目录。

对于 Codex，可以这样安装 `log-project-inputs`：

```text
~/.codex/skills/log-project-inputs
```

Windows 上通常是：

```text
C:\Users\<you>\.codex\skills\log-project-inputs
```

安装后重启对应 agent，或刷新 skill discovery。

## 隐私说明

部分 skill 可能会写入本地文件，或处理项目内容。使用前请阅读对应 skill 的 `SKILL.md`，提交或分享项目仓库前也请检查生成文件。

本仓库的 `.gitignore` 当前已忽略 `log-*.md`，用于降低测试 `log-project-inputs` 时误提交日志的风险。

## 许可证

MIT
