---
layout: default
title: Claude Code + GLM 4.7 + MCP 配置指南
no_duoshuo: false
permalink : /claude-code-glm-mcp/
---

# Claude Code + GLM 4.7 + MCP 配置指南

最近在探索 Claude Code 这个强大的 AI 编程助手，发现它结合 GLM 4.7 和 MCP (Model Context Protocol) 可以发挥出惊人的效果。本文记录配置过程和使用经验。

## 什么是 Claude Code

Claude Code 是 Anthropic 官方推出的 CLI 工具，能够直接在命令行中使用 Claude 进行软件开发。它集成了代码编辑、文件操作、git 管理、bash 命令执行等功能，是开发者的得力助手。

## GLM 4.7 简介

GLM (General Language Model) 是智谱 AI 推出的大语言模型系列，GLM 4.7 在代码理解和生成方面表现出色，特别适合中文开发者使用。

## MCP (Model Context Protocol) 简介

MCP 是一个开放协议，允许 AI 应用连接到外部数据源和工具。通过 MCP，Claude Code 可以访问：

- 文件系统
- 数据库
- API 服务
- 自定义工具

## 配置步骤

### 1. 安装 Claude Code

```bash
# 使用 npm 安装
npm install -g @anthropic-ai/claude-code

# 或使用 Homebrew（macOS）
brew install claude-code
```

### 2. 配置 GLM 4.7

首先需要在智谱 AI 获取 API Key。

创建配置文件 `~/.config/claude-code/config.json`:

```json
{
  "providers": {
    "glm": {
      "baseUrl": "https://open.bigmodel.cn/api/paas/v4/",
      "apiKey": "your-glm-api-key-here",
      "model": "glm-4.7"
    }
  },
  "defaultProvider": "glm"
}
```

### 3. 配置 GLM MCP 服务器

使用智谱 AI 提供的 MCP 服务，需要先获取 API Key。

#### 联网搜索 MCP

```bash
claude mcp add -s user -t http web-search-prime \
  https://open.bigmodel.cn/api/mcp/web_search_prime/mcp \
  --header "Authorization: Bearer your_api_key"
```

功能：
- 实时网络搜索
- 获取最新信息
- 支持多种搜索引擎

#### 网页读取 MCP

```bash
claude mcp add -s user -t http web-reader \
  https://open.bigmodel.cn/api/mcp/web_reader/mcp \
  --header "Authorization: Bearer your_api_key"
```

功能：
- 提取网页内容
- 清理页面元素
- 转换为易读格式

#### 视觉理解 MCP

```bash
claude mcp add -s user zai-mcp-server \
  --env Z_AI_API_KEY=your_api_key \
  -- npx -y "@z_ai/mcp-server"
```

功能：
- 图片理解和分析
- OCR 文字识别
- 图表解析

#### 故障排除

如果视觉理解 MCP 遇到问题，可以尝试：

```bash
Z_AI_API_KEY=your_api_key npx -y @z_ai/mcp-server
```

### 4. 验证 MCP 配置

```bash
# 查看已配置的 MCP 服务器
claude mcp list

# 测试 MCP 连接
claude mcp test web-search-prime
```

## 使用示例

### 联网搜索

```bash
# 启动 Claude Code
claude

# 使用联网搜索
> 搜索 2025 年最新的 React 性能优化最佳实践

# 搜索并总结
> 查找 Vue 3.5 的新特性并给出中文总结
```

### 网页内容读取

```bash
# 读取并分析网页
> 读取 https://github.com/modelcontextprotocol/servers 的 README，列出所有可用的 MCP 服务器

# 批量处理
> 读取这个文章 https://example.com/article，提取其中的代码示例并整理成 Markdown 格式
```

### 视觉理解

```bash
# 分析本地图片
> 分析 screenshots/demo.png 中的 UI 布局，并用 HTML + Tailwind CSS 重新实现

# OCR 识别
> 提取 image.png 中的所有文字内容

# 图表分析
> 分析 chart.png 中的数据趋势并生成 CSV 文件
```

### 结合代码开发

```bash
# 完整工作流
> 搜索最新的 Next.js 15 最佳实践，读取官方文档，然后帮我创建一个符合最佳实践的项目结构

# 学习新技术
> 搜索 "Rust async await 教程"，找到最好的 3 篇文章并总结核心概念
```

## 实际应用场景

### 1. 技术调研

使用联网搜索 MCP 快速调研新技术：

```bash
> 搜索 "Rust vs Go 性能对比 2025"，找到最近的 benchmark 数据并总结
```

Claude 会：
- 使用 web-search-prime 搜索相关内容
- 阅读多个来源
- 整理出对比报告

### 2. 文档学习

结合网页读取 MCP 深度学习官方文档：

```bash
> 读取 https://docs.python.org/3.12/whatsnew/3.12.html，总结 Python 3.12 的重要更新
```

### 3. UI 还原

使用视觉理解 MCP 从设计图生成代码：

```bash
> 分析 design.png 中的登录页面，用 React + Tailwind CSS 实现
```

### 4. 数据分析

从图表中提取数据：

```bash
> 分析 report.png 中的销售数据图表，生成 Excel 表格
```

## 高级技巧

### 1. 组合使用多个 MCP

在同一个任务中串联使用多个 MCP：

```bash
> 搜索 "2025 年最佳 AI 编程工具"，访问前 3 篇文章，分析其中的工具对比图，生成 Markdown 报告
```

Claude 会自动：
- 使用 web-search-prime 搜索
- 使用 web-reader 读取文章
- 使用 zai-mcp-server 分析图表
- 整合信息生成报告

### 2. API Key 管理

为安全起见，建议使用环境变量：

```bash
# 在 ~/.zshrc 或 ~/.bashrc 中添加
export GLM_API_KEY="your_api_key"
export Z_AI_API_KEY="your_zai_api_key"

# 使用时
claude mcp add -s user -t http web-search-prime \
  https://open.bigmodel.cn/api/mcp/web_search_prime/mcp \
  --header "Authorization: Bearer $GLM_API_KEY"
```

### 3. 调试 MCP 请求

如果遇到问题，可以查看详细日志：

```bash
# 启用调试模式
claude --debug

# 测试单个 MCP
claude mcp test web-reader
```

## 常见问题

### Q: MCP 连接失败怎么办？

1. 检查 API Key 是否正确
2. 验证网络连接是否正常
3. 确认智谱 AI 服务状态
4. 查看错误日志：`claude mcp test <server-name>`

### Q: GLM API 频率限制？

智谱 AI API 有频率限制，可以考虑：
- 使用多个 API Key 轮换
- 添加请求队列避免突发请求
- 升级到更高的套餐

### Q: 视觉理解 MCP 报错？

确认：
- Z_AI_API_KEY 已正确设置
- 网络可以访问 npm registry
- 已安装最新版 Node.js

如果仍有问题，使用故障排除命令单独测试。

### Q: 搜索结果不准确？

尝试：
- 使用更具体的关键词
- 添加时间限制（如 "2025年"）
- 结合网页读取深度分析

## 性能优化

### 1. 并发工具调用

Claude 可以同时调用多个 MCP 工具，大幅提升效率。例如：
- 同时搜索多个关键词
- 批量读取多个网页
- 并行处理多个图片

### 2. 缓存机制

对于重复查询，合理利用对话上下文避免重复请求。

### 3. 成本控制

- web-search-prime：按搜索次数计费
- web-reader：按页面大小和数量计费
- zai-mcp-server：按图片处理次数计费

建议：
- 明确需求后再调用 MCP
- 避免不必要的重复搜索
- 一次性提出完整需求

## 总结

Claude Code + GLM MCP 的组合为开发者提供了强大的 AI 辅助能力，特别是对中文开发者非常友好。

### 核心优势

1. **联网能力**：实时获取最新信息
2. **网页理解**：深度解析网页内容
3. **视觉理解**：图片分析和 OCR
4. **中文优化**：GLM 模型对中文支持更好
5. **简单易用**：一条命令即可配置 MCP

### 最佳实践

- 明确任务需求，选择合适的 MCP
- 组合使用多个 MCP 发挥最大价值
- 注意 API 成本和频率限制
- 保护好 API Key，使用环境变量管理

### 推荐工作流

```bash
# 1. 配置 MCP
claude mcp add -s user -t http web-search-prime ...
claude mcp add -s user -t http web-reader ...
claude mcp add -s user zai-mcp-server ...

# 2. 验证配置
claude mcp list

# 3. 开始使用
claude
> 搜索并学习最新的技术栈...
```

---

**备注**：本文记录配置过程，实际使用中请根据最新文档进行调整。

## 参考资源

- [Claude Code 官方文档](https://code.claude.com/docs)
- [智谱 AI 开放平台](https://open.bigmodel.cn)
- [智谱 AI MCP 文档](https://open.bigmodel.cn/dev/mcp)
- [MCP 协议规范](https://modelcontextprotocol.io)
- [Claude Code GitHub](https://github.com/anthropics/claude-code)
