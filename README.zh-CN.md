<div align="center">
  <img src="https://raw.githubusercontent.com/vastsa/PI-Desktop/main/docs/public/readme/logo.png" alt="PI-Desktop 标志" width="96" />
  <h1>PI-Desktop</h1>
  <p><strong>本地优先的 AI 编程桌面工作台</strong></p>
  <p>
    <a href="https://github.com/vastsa/PI-Desktop/releases/latest">立即下载</a> ·
    <a href="https://docs.aiuo.net/zh-CN/">使用文档</a> ·
    <a href="https://github.com/vastsa/PI-Desktop/blob/main/docs/zh-CN/guide/screenshots.md">界面预览</a> ·
    <a href="README.md">English</a>
  </p>
</div>

[![版本](https://img.shields.io/github/v/release/vastsa/PI-Desktop)](https://github.com/vastsa/PI-Desktop/releases)
[![下载量](https://img.shields.io/github/downloads/vastsa/PI-Desktop/total)](https://github.com/vastsa/PI-Desktop/releases)
[![Stars](https://img.shields.io/github/stars/vastsa/PI-Desktop)](https://github.com/vastsa/PI-Desktop/stargazers)
[![CI](https://github.com/vastsa/PI-Desktop/actions/workflows/ci.yml/badge.svg)](https://github.com/vastsa/PI-Desktop/actions/workflows/ci.yml)
[![许可证](https://img.shields.io/github/license/vastsa/PI-Desktop)](https://github.com/vastsa/PI-Desktop/blob/main/LICENSE)

PI-Desktop 将项目目录、可持续使用的 Agent 会话、代码审查和模型配置集中在一个桌面应用中，支持 macOS、Windows 和 Linux。打开仓库并选择模型，就能从首次工具调用跟进到最终代码变更。下次打开应用时，可以回到同一会话，从保存的历史继续工作。

本仓库提供 PI-Desktop 的中英文项目介绍。源代码、软件发布和问题跟踪均在 [PI-Desktop 项目仓库](https://github.com/vastsa/PI-Desktop)。

![PI-Desktop 首页](https://raw.githubusercontent.com/vastsa/PI-Desktop/main/docs/public/readme/home.webp)

## 快速开始

1. [下载适合你系统的最新稳定版](https://github.com/vastsa/PI-Desktop/releases/latest)。预览版可在[发布记录](https://github.com/vastsa/PI-Desktop/releases)中找到。当前发布线为 **0.24.x**。
2. 在 **设置 → 模型**中添加服务并选择模型。可以连接云端模型、兼容 API、自建网关，或 Ollama、LM Studio 等本地服务。
3. 打开本地项目目录并新建会话。用 **Agent** 执行开发任务，用 **Plan** 先审阅方案再执行，或用 **Goal** 指定目标与验收标准。

| 平台 | 架构 | 安装包 |
| --- | --- | --- |
| macOS | Apple Silicon、Intel | DMG、ZIP |
| Windows | x64 | 安装程序、ZIP |
| Linux | x64、ARM64 | AppImage、DEB、RPM |

macOS 安装包已完成签名和 Apple 公证。Linux 安装包要求 glibc 2.35 或更新版本。

## 项目与会话

- **保留项目上下文。** 按项目组织会话，搜索历史或从已有会话创建分支，用 `@` 引用文件，并在 Agent 运行时将新消息加入队列。支持导入 Claude Code、Codex、OpenCode 和 Pi 的本地会话。
- **跟进代码变更。** 查看流式回复、命令输出和代码差异，并在工作面板中打开文件和预览。
- **并行委派任务。** Subagent 在独立上下文中处理范围明确的任务，完成后向父会话汇报。Session Orchestrator 可以协调多个 Worker Session，每个都有自己的会话历史，可单独查看或继续执行。
- **按会话选择模型。** 在规划、实现和审查阶段切换已配置的模型，同时保留项目和会话历史。

项目、会话、设置和日志默认保存在本地。使用远程模型时，请求所需的上下文会直接发送给你配置的模型服务。需要授权的工具调用由会话权限策略判断，可放行、拒绝或请求你审批。

## 插件扩展

可以从应用内的插件市场安装插件，也可以直接安装 `.piplug` 包。插件可添加 Agent 工具、Skill、MCP 服务、面板、悬浮组件、主题和后台服务。Plugin SDK 和 CLI 提供开发模板，以及校验、打包和发布命令。[插件开发指南](https://github.com/vastsa/PI-Desktop/blob/main/docs/zh-CN/plugin-development.md) · [插件示例](https://github.com/vastsa/PI-Desktop/blob/main/examples/plugins/README.md)

## 技术架构

| 层级 | 职责 |
| --- | --- |
| React + TypeScript 渲染层 | 项目、会话、流式消息、代码审查和设置界面 |
| Electron 主进程与预加载层 | 窗口生命周期、类型化 IPC、进程监督 |
| Rust Host Core + SQLite | 本地持久化、权限校验和宿主服务 |
| Node.js Agent Runtime | 基于 `pi-ai`、`pi-agent-core` 和 `pi-coding-agent` 处理模型流式输出与 Agent 执行 |

[架构文档](https://github.com/vastsa/PI-Desktop/blob/main/docs/spec/02-architecture/01-architecture.md) · [Pi](https://github.com/badlogic/pi-mono)

## 从源码运行

需要 Node.js 22.19 或更新版本、[package.json](https://github.com/vastsa/PI-Desktop/blob/main/package.json) 指定的 pnpm 版本以及稳定版 Rust 工具链。

```bash
git clone https://github.com/vastsa/PI-Desktop.git
cd PI-Desktop
pnpm install --frozen-lockfile
cargo build --locked -p host-core
pnpm build:js
pnpm dev
```

按改动范围运行 `pnpm typecheck`、`pnpm lint` 或 `pnpm test`。[贡献指南](https://github.com/vastsa/PI-Desktop/blob/main/CONTRIBUTING.md)说明仓库约定，[产品规范](https://github.com/vastsa/PI-Desktop/blob/main/docs/spec/README.md)记录功能和接口契约。

## 社区与许可证

欢迎通过 [GitHub Issues](https://github.com/vastsa/PI-Desktop/issues)提交反馈，或加入 [QQ 开发者交流群](https://qm.qq.com/q/iWP8i0XxIc)、[Reddit](https://www.reddit.com/r/AIUO/) 和 [Linux.Do](https://linux.do/) 参与讨论。安全问题请按[安全策略](https://github.com/vastsa/PI-Desktop/blob/main/SECURITY.md)报告。

PI-Desktop 采用 [GNU LGPL v3.0](https://github.com/vastsa/PI-Desktop/blob/main/LICENSE) 许可证。感谢 Pi 项目、社区贡献者，以及为开发和审查工作提供工具的模型服务商。
