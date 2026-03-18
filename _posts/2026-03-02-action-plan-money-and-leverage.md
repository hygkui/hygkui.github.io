---
layout: default
title: AI学习清单：12个必须掌握的技能
no_duoshuo: false
permalink: /ai-learning-checklist-20250302/
---

# AI学习清单：12个必须掌握的技能

以下是针对你提供的这个AI学习计划列表的**详细展开介绍**。这个列表是2026年初AI圈（尤其是X/Twitter、Facebook、Substack上）非常火的“周末必做计划”，由几位AI重度用户（如Yik Chan、sifuyik等）发起，目的是让普通人快速上手2026年最前沿的AI工具，从“聊天AI”升级到“能真正干活的AI代理”。

我按原顺序逐点解释**每一点到底是干啥的**、**为什么要做**、**核心功能和上手方式**，方便你直接照着操作。

### 1. Learn Claude Code

**干啥的**：这是Anthropic官方推出的**Claude Code**工具（终端版Claude）。  
它不是网页聊天，而是直接装在你电脑里，像命令行助手一样工作。你在项目文件夹里敲一句“claude”，然后用自然语言说“帮我建一个Todo App”，它就会自动生成完整代码、运行、调试、迭代。  
**为什么要做**：Claude在2025-2026年编码能力极强，这个工具把Claude变成你的“终端搭档”，零基础也能10分钟出原型，比Cursor或Aider更原生。  
**上手**：终端运行 `npm install -g @anthropic-ai/claude-code`，然后 `claude` 启动，绑定你的API Key即可。

### 2. Set up Perplexity Computer

**干啥的**：Perplexity.ai在2026年2月25日刚发布的**Perplexity Computer**（简称PC）。  
它是一个**云端超级AI代理系统**，能把整个复杂工作流从头做到尾（研究→规划→编码→部署→监控），可以连续跑几小时甚至几个月，还会自动创建子代理分工。  
**为什么要做**：传统聊天AI只能“告诉你怎么做”，而它直接“替你做完”。云端运行，更安全，比本地工具稳定。  
**上手**：Perplexity Max订阅（最高档）里直接点开用，支持400+ App集成。

### 3. Set up Claude Cowork (plug-ins, skills)

**干啥的**：Anthropic的**Claude Cowork**（桌面AI同事）。  
它用Claude的“Computer Use”能力，直接接管你的电脑桌面：看屏幕、点鼠标、打字、整理文件、建表格、做PPT、打开浏览器……真正像一个AI员工在你电脑上干活。  
**为什么要做**：从“问AI”升级到“让AI替你操作电脑”，解放双手。支持自定义skills（技能）和plug-ins（插件）。  
**上手**：Claude Desktop App里付费用户（$20/月起）直接开启，授权屏幕访问即可。

### 4. Set up OpenClaw

**干啥的**：开源的**OpenClaw**（🦞图标），一个真正“会做事”的个人/团队AI助手。  
它能清邮箱、发邮件、管日历、订机票、刷网页、自动化重复工作，主要通过Telegram/WhatsApp聊天控制。完全开源、可自己改代码，社区在狂建各种skills。  
**为什么要做**：它是2026年最火的“本地AI代理”之一，免费可自托管，比闭源工具更灵活（但要注意安全）。  
**上手**：一条命令 `curl -fsSL https://openclaw.ai/install.sh | bash`，装好后连API Key（推荐Claude Opus）和Telegram即可。支持VPS 24/7运行。

### 5. Experiment with agentic solutions

**干啥的**：**Agentic AI（代理式AI）实验**。  
就是把上面这些工具（Claude Cowork、OpenClaw、Perplexity Computer、Manus等）串起来，或者用CrewAI、AutoGen等框架，自己搭多代理系统，让AI自主规划、执行长链任务。  
**为什么要做**：2026年AI的核心趋势就是“agentic”（有主观能动性），实验能让你从使用者变成创造者。  
**上手**：先用现成工具，再试开源框架，每天做一个简单agent任务。

### 6. Use AI to create a business plan & strategy

**干啥的**：拿任意一个强AI（Claude Cowork / Perplexity Computer / OpenClaw）输入你的idea，让它输出**完整商业计划书**（市场分析、竞品、财务模型、营销策略、执行路线图）。  
**为什么要做**：以前要花几周做的事，现在几小时就出专业版，还能实时迭代。  
**上手**：给它角色（“你是麦肯锡资深顾问”）+ 详细背景 + 要求结构化输出。

### 7. Build an AI second-brain database

**干啥的**：搭建一个**AI增强的第二大脑**知识库。  
把你所有笔记、想法、文章、聊天记录扔进去，AI自动整理、关联、总结、搜索、生成新洞见。  
**为什么要做**：信息爆炸时代，人脑记不住，AI第二大脑能让你“外挂”无限记忆和思考能力。  
**上手**：常用组合：Notion + Claude / Mem.ai / Obsidian +插件 / Perplexity Collections。

### 8. Learn basic automation tools (Manus, MCP, Zapier)

**干啥的**：掌握2026年主流自动化组合：  

- **Zapier**：老牌无代码自动化，连接8000+ App（触发器+动作）。  
- **Manus**：新一代AI代理（$20/月），专门干端到端任务（研究、写报告、建网页），现在已深度集成Meta生态。  
- **MCP**（Model Content Protocol）：Zapier推出的AI协议，让Manus和其他AI能实时调用动作、传递内容，实现“AI大脑 + 自动化身体”的无缝对接。  
**为什么要做**：单靠聊天AI不够，必须学会让AI“连上现实世界”的自动化。  
**上手**：先学Zapier基础，再接Manus，最后配置MCP Server。

### 9. Become an elite prompt-engineer

**干啥的**：成为**顶级提示工程师**（Prompt Engineer）。  
掌握高级技巧：Chain of Thought、Few-shot、Tree of Thought、角色扮演、结构化输出、自我反思等。  
**为什么要做**：列表里明确写了——“你跟AI沟通越好，输出越强”。这是所有工具的“通用操作系统”。  
**上手**：每天练10个prompt，读Prompt Engineering Guide，参加社区挑战。

### 10. Read AI articles

**干啥的**：每天刷AI最新资讯、论文、产品发布、行业分析。  
**为什么要做**：AI领域每周都有新东西，不读就会落后。  
**上手**：推荐来源：Perplexity Discover、The Batch、AlphaSignal、Hacker News AI版块、Substack AI作者。

### 11. Dive into robotics

**干啥的**：从软件AI深入到**物理世界AI**（机器人）。  
学习ROS2、硬件接口、具身智能（Embodied AI）、家用/工业机器人项目。  
**为什么要做**：2026年AI正从屏幕走向现实，机器人是下一个万亿赛道（Figure、1X、Tesla Bot等）。  
**上手**：先玩开源项目（如用Claude控制Arduino/Raspberry Pi），再看Boston Dynamics或Unitree视频。

### 12. Research AI stocks/ETFs/investment arbitrages

**干啥的**：系统研究AI产业链投资机会。  
股票（NVIDIA、TSMC、ASML、Microsoft、Anthropic相关、机器人公司）、ETF（AI主题基金）、套利（不同交易所价差、期权等）。  
**为什么要做**：AI是当前最大风口，懂技术的人做投资更有优势。  
**上手**：用Perplexity Computer直接问“2026 AI投资组合推荐”，再自己验证。

---

这个列表的核心逻辑是：**从学会用最强单点工具 → 搭建代理系统 → 自动化落地 → 知识管理 → 投资闭环**，一周就能完成“AI普通用户 → AI重度玩家”的跃迁。
