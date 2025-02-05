# 超详细指南：如何利用 Cursor 在 VSCode 中进行 iOS 开发

近年来，人工智能技术逐渐渗透到开发领域，成为提升开发效率的重要工具。本文将深入探讨如何在 VSCode 中使用 Cursor，这款内置 AI 辅助功能的代码编辑器，来优化 iOS 开发流程。

Cursor 作为 VSCode 的分支，集成了多种 AI 辅助功能。如果你曾体验过 VSCode 中的 Copilot，那么 Cursor 将带给你更为强大的体验。它不仅具备 Copilot 的核心功能，还在此基础上增加了更多提升工作效率的工具。

本文将详细介绍如何为开源 SwiftUI Mastodon 客户端 Ice Cubes 配置 Cursor，并展示其核心功能的使用方法。

## 一、Cursor 的获取与安装

首先，你需要下载 Cursor。这款编辑器提供免费版本，但部分高级功能需要订阅（价格为 20 美元）。免费版本允许你体验一段时间，帮助你判断是否值得升级。如果你已拥有 OpenAI、Claude 或 Gemini 的密钥，可以直接在设置中进行配置。

下载完成后，需安装相关扩展并进行配置。

### 部署 Xcode Build Server

通过部署 [Xcode Build Server](https://github.com/SolaWing/xcode-build-server)，可以让 SourceKit-LSP 在 Xcode 之外运行，从而获得跳转到定义、查看引用、调用树分析等功能，这些功能与 Xcode 中的体验几乎一致。

![Xcode Build Server](https://bbtdd.com/img/6270879087.webp)

### 配置 xcbeautify

接下来，需要配置 [xcbeautify](https://github.com/cpisciotta/xcbeautify)，它可以在 Cursor 的终端中美观地打印 Xcodebuild 输出。

![xcbeautify](https://bbtdd.com/img/68375397163578.webp)

如果你还没有安装 [Swift 格式](https://github.com/nicklockwood/SwiftFormat)，建议现在部署。

### 安装扩展

启动 Cursor 后，打开扩展选项卡并安装以下扩展：

- **Swift 语言支持**：提供语法高亮和 Swift 语言功能。
- **Sweetpad**：使整个流程在 Xcode GUI 之外正常运行。你需要熟悉其功能、快捷方式及工作原理。

![Sweetpad](https://bbtdd.com/img/5194794705412739.webp)

安装 Sweetpad 后，使用 `CMD+SHIFT+P` 打开命令面板并选择相关选项，这将在项目根目录下创建 `buildServer.json`，使 Xcode Build Server 与项目目录协同工作。

![buildServer.json](https://bbtdd.com/img/232700214.webp)

### 构建与调试

完成配置后，点击构建并运行（从命令面板或 Sweetpad 选项卡）。此时，构建一次项目非常重要，这将激活自动完成、跳转到引用等功能。

之后，你可以使用 `F5` 连接调试器。可能需要为调试模式创建启动配置，建议在提示时选择 Sweetpad。

## 二、Cursor 的核心功能

### 1. Tab 自动补全

Cursor 内置了基于 AI 的自动补全功能，能够预测你的下一步操作。它会根据项目内容进行定制，提供更精准的代码建议。

![自动补全](https://bbtdd.com/img/94574156670.webp)

### 2. 内联编辑

在空行上按 `CMD+K` 可以从提示生成代码，或在代码行上按 `CMD+K` 将相关代码嵌入提示中，方便进行重构或修改。

![内联编辑](https://bbtdd.com/img/219128077367544.webp)

### 3. 聊天功能

按 `CMD+L` 打开聊天面板，可以与模型讨论任何与编码相关的问题。此功能支持嵌入代码、添加文件到上下文等操作。

![聊天功能](https://bbtdd.com/img/7953033880029.webp)

### 4. Composer

Composer 功能允许你批量编辑或生成多个文件，适合从头开始设置新项目或生成样板代码。

![Composer](https://bbtdd.com/img/77111230631462.webp)

## 三、使用 CoDesign 提升开发效率

CoDesign 是为设计师和开发者打造的设计资产管理平台，它支持设计稿上传、版本管理，帮助开发者快速获取前端样式、切图和标注信息。

![CoDesign](https://bbtdd.com/img/244913370.webp)

👉 [WildCard | 一分钟注册，轻松订阅海外线上服务](https://bbtdd.com/WildCard)