<div align="center">
  <img src="https://raw.githubusercontent.com/vastsa/PI-Desktop/main/docs/public/readme/logo.png" alt="PI-Desktop logo" width="96" />
  <h1>PI-Desktop</h1>
  <p><strong>A local-first desktop workspace for AI coding agents</strong></p>
  <p>
    <a href="https://github.com/vastsa/PI-Desktop/releases/latest">Download</a> ·
    <a href="https://docs.aiuo.net/">User guide</a> ·
    <a href="https://github.com/vastsa/PI-Desktop/blob/main/docs/guide/screenshots.md">Screenshots</a> ·
    <a href="README.zh-CN.md">简体中文</a>
  </p>
</div>

[![Release](https://img.shields.io/github/v/release/vastsa/PI-Desktop)](https://github.com/vastsa/PI-Desktop/releases)
[![Downloads](https://img.shields.io/github/downloads/vastsa/PI-Desktop/total)](https://github.com/vastsa/PI-Desktop/releases)
[![Stars](https://img.shields.io/github/stars/vastsa/PI-Desktop)](https://github.com/vastsa/PI-Desktop/stargazers)
[![CI](https://github.com/vastsa/PI-Desktop/actions/workflows/ci.yml/badge.svg)](https://github.com/vastsa/PI-Desktop/actions/workflows/ci.yml)
[![License](https://img.shields.io/github/license/vastsa/PI-Desktop)](https://github.com/vastsa/PI-Desktop/blob/main/LICENSE)

PI-Desktop brings project folders, persistent agent sessions, code review, and model settings into one application for macOS, Windows, and Linux. Open a repository, choose a model, and follow the agent's work from the first tool call to the final diff. Reopen the session later to continue from its saved history.

This repository contains the English and Simplified Chinese project overviews. The application source, releases, and issue tracker are in the [PI-Desktop project repository](https://github.com/vastsa/PI-Desktop).

![PI-Desktop home screen](https://raw.githubusercontent.com/vastsa/PI-Desktop/main/docs/public/readme/home.webp)

## Get started

1. [Download the latest stable release](https://github.com/vastsa/PI-Desktop/releases/latest) for your platform. Preview builds are listed on the [releases page](https://github.com/vastsa/PI-Desktop/releases). The current release line is **0.24.x**.
2. In **Settings → Models**, add a provider and select a model. Use a cloud provider, a compatible API or gateway, or a local server such as Ollama or LM Studio.
3. Open a local project folder and start a session. Choose **Agent** for implementation, **Plan** to review an approach before execution, or **Goal** to give the agent an outcome and acceptance criteria.

| Platform | Architecture | Release packages |
| --- | --- | --- |
| macOS | Apple Silicon and Intel | DMG, ZIP |
| Windows | x64 | Installer, ZIP |
| Linux | x64 and ARM64 | AppImage, DEB, RPM |

macOS packages are signed and notarized. Linux packages require glibc 2.35 or later.

## Work across sessions

- **Keep project context.** Organize sessions by project, search or branch past conversations, reference files with `@`, and queue prompts while a turn is running. Import local sessions from Claude Code, Codex, OpenCode, or Pi.
- **Review changes as they happen.** Follow streaming responses, inspect command output and code diffs, and open files and previews in the Work Panel.
- **Delegate parallel work.** Subagents handle scoped tasks with independent context and report back to the parent. The Session Orchestrator can coordinate full Worker Sessions with their own histories for work you want to inspect or continue separately.
- **Choose the model per session.** Switch between configured models for planning, implementation, and review while keeping the same project workflow.

Project and session data, settings, and logs are stored locally by default. When you use a remote model, the context needed for the request is sent directly to your configured provider. Privileged tool calls are evaluated against the session's permission policy and can be allowed, denied, or sent for your approval.

## Extend the workspace

Install plugins from the in-app marketplace or from a `.piplug` package. Plugins can add agent tools, Skills, MCP servers, panels, floating widgets, themes, and background services. The Plugin SDK and CLI provide templates and commands for validation, packaging, and publishing. [Plugin development guide](https://github.com/vastsa/PI-Desktop/blob/main/docs/plugin-development.md) · [Examples](https://github.com/vastsa/PI-Desktop/blob/main/examples/plugins/README.md)

## Architecture

| Layer | Responsibility |
| --- | --- |
| React and TypeScript renderer | Project, session, streaming transcript, review, and settings UI |
| Electron main and preload | Window lifecycle, typed IPC, and process supervision |
| Rust Host Core and SQLite | Local persistence, permission checks, and host services |
| Node.js Agent Runtime | Model streaming and agent execution using `pi-ai`, `pi-agent-core`, and `pi-coding-agent` |

[Architecture documentation](https://github.com/vastsa/PI-Desktop/blob/main/docs/spec/02-architecture/01-architecture.md) · [Pi](https://github.com/badlogic/pi-mono)

## Run from source

Use Node.js 22.19 or later, the pnpm version pinned in [package.json](https://github.com/vastsa/PI-Desktop/blob/main/package.json), and a stable Rust toolchain.

```bash
git clone https://github.com/vastsa/PI-Desktop.git
cd PI-Desktop
pnpm install --frozen-lockfile
cargo build --locked -p host-core
pnpm build:js
pnpm dev
```

Run `pnpm typecheck`, `pnpm lint`, or `pnpm test` as appropriate for your change. Read the [contributing guide](https://github.com/vastsa/PI-Desktop/blob/main/CONTRIBUTING.md) for repository conventions and the [specifications](https://github.com/vastsa/PI-Desktop/blob/main/docs/spec/README.md) for product contracts.

## Community and license

Share feedback on [GitHub Issues](https://github.com/vastsa/PI-Desktop/issues) or join the discussion on [Reddit](https://www.reddit.com/r/AIUO/), [QQ](https://qm.qq.com/q/iWP8i0XxIc), or [Linux.Do](https://linux.do/). Report vulnerabilities through the [security policy](https://github.com/vastsa/PI-Desktop/blob/main/SECURITY.md).

PI-Desktop is licensed under the [GNU Lesser General Public License v3.0](https://github.com/vastsa/PI-Desktop/blob/main/LICENSE). Thank you to the Pi project, the contributors, and the model providers whose tools helped build and review PI-Desktop.
