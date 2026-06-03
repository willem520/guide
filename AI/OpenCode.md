# OpenCode
OpenCode是一款开源的终端AI编程助手，允许开发者在CLI环境中直接调用AI完成代码编写、调试及重构任务

## 核心功能与特点
> * 双模式工作流：内置Plan（规划）与Build（构建）两种Agent模式，可通过Tab键快速切换
>   * Plan模式：只读权限，用于分析代码结构、规划改动，默认拒绝修改文件，适合探索未知项目
>   * Build模式：拥有完整全县，负责实际代码生成、编辑及工具调用
> * 多模型兼容：不绑定特定AI提供商，支持多种大语言模型，包括Claude、GPT、Gemini以及国内模型（DeepSeek）等
> * 终端原生体验：专为命令行设计，提供原生TUI界面，支持上下文感知，能自动扫描项目文件理解代码结构

## 安装及使用
### 安装
> 参考官方文档 https://opencode.ai/docs/zh-cn 即可完成。注意使用OpenCode前提条件（现代终端模拟器&要使用的LLM提供商的API密钥）

### 使用
使用opencode命令即可进入TUI界面
> **斜杠命令（/命令）**
> 
> 输入/可查看相应命令
> 
> ![avatar](opencode_tui.png)
>
> **Base命令（!命令）**
> 
> 输入!后，控制台会变为shell模式，在该模式下可以直接输入shell命令
> ![avatar](opencode_shell.png)
> 
> **输入**
> 在控制台输入对应内容，回车后，即可执行（注意，Build模式下会直接修改并生效，Plan模式下只会生成计划，不会发生变更）
> ![avatar](opencode_input.png)

## Skills