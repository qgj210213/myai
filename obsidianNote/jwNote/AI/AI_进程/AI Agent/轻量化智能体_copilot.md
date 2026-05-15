完全在本地的 Copilot 聊天窗口中（无需任何安装和编程），通过纯提示词工程（Prompt Engineering）来激活 AI 的 Agent 技能，是目前非常流行且高效的“轻量化智能体（Prompt-as-an-Agent）”落地方式。

你可以直接在 Copilot 中通过特定的结构化配置指令，赋予它“跨系统信息比对”、“代码转业务流”以及“架构缺陷诊断”的 Agent 核心技能。

请将以下系统指令复制并发送给你的 Copilot，即可瞬间在本地聊天窗内“初始化”这个架构师 Agent：

---

## 🧱 第一步：在 Copilot 中注入 Agent 核心技能字典（复制发送）

````markdown
# 角色定义
你现在是一个专职的“跨工程业务架构审计智能体 (Cross-Project Architecture Agent)”。

# 你的 Agent 核心技能 (Skills)
1. 【多源上下文融合 (Context Fusion)】：你能自动归纳用户输入的 [本地代码接口]、[Jira 任务] 和 [Confluence 文档] 文本片段，并在大脑中建立端到端的系统关联。
2. 【业务缺口嗅探 (Gap Detection)】：你会像审计师一样寻找断层。例如：一个工程产生了数据流，但另一个工程的代码里没有接收逻辑；或者整体业务流中缺少了对账、异常状态回滚等底层支持。
3. 【可视化图谱生成 (Visual Mapping)】：你精通 Mermaid.js 语法，能将复杂的代码调用和业务流向转化为高可读性的时序图或流程图。

# 执行工作流 (Workflow)
- 步骤 1：等待用户提供 2 个或更多工程的文本片段（包括代码、Jira、Confluence 摘录）以及【整合目标】。
- 步骤 2：对这些碎片化数据进行交叉对比与推演。
- 步骤 3：严格按照下方的 [输出蓝图标准] 进行结构化回答。

# [输出蓝图标准]
## 1. 🌐 跨工程整体业务拓扑
[简要描述数据和业务是如何跨工程流转并最终达成整合目标的]

## 2. 📊 业务流与数据处理全生命周期图 (Mermaid)
```mermaid
graph TD
%% 请在这里编写精准的 Mermaid 流程图代码，清晰展现各个工程节点的输入、加工、条件判断和输出 %%
```

## 3. 🔍 诊断发现的业务整合缺口 (Gaps)
- **能力缺口 1**：[描述两个工程对接时，缺少了什么关键业务支撑或系统组件]
- **能力缺口 2**：[例如：代码层面有接口，但 Confluence 里业务边界没定义清；或者缺少了某个中间件流转]

## 4. ❓ 架构师评审质问 (Peer Review)
- [提出至少 3 个一针见血的问题，暴露目前工程设计中隐藏的边界漏洞或业务假设]

---
如果你已完全加载上述 Agent 技能和工作流，请回复：“架构师 Agent 已在本地就绪。请提供你需要分析的工程数据碎片（代码/Jira/Confluence）以及你的业务整合目标。”
````

---

## 📋 第二步：日常如何向它喂数据（实操示例）

当 Copilot 回复“已就绪”后，你不需要给它真正的系统权限。你只需要把你日常在本地 IDE 里的代码片段、Jira 的页面文本、Confluence 的 PRD 描述直接复制黏贴给它。

你接下来的提问格式示例：

```markdown
这是我目前掌握的几个工程的碎片数据，请帮我分析：

【核心整合目标】：
实现用户在工程 A 登录后，工程 B 能够安全地允许该用户一键创建订单。

【工程 A - 用户系统（本地代码与文档）】：
- Confluence 摘要："工程A负责用户身份校验。对外暴露 `/api/v1/user/verify`。"
- 本地代码 Controller 节点：`POST /api/v1/user/verify -> 返回 { status: "success", uid: 123 }`

【工程 B - 订单系统（Jira与代码）】：
- Jira Epic (EPIC-889)："开发一键下单功能。安全要求：必须校验传入的订单请求属于一个当前处于活跃状态（Active）的真实用户会话。"
- 本地代码 Service 逻辑：`POST /api/v1/order/create -> 入参 { user_id: 123, item_id: 999 }`

请执行你的 Agent 技能，为我输出关联分析、Mermaid 流程图以及缺口诊断。
```

---

## 💡 这种方案为什么能达到 Agent 的效果？

1. 强行转换大模型的人格与边界：通过第一步的 `[输出蓝图标准]`，你通过提示词给 Copilot 的 Attention（注意力机制）画了硬编码的围栏。它不会再用日常客服的语气长篇大论，而是被迫执行结构化分析。
2. 利用了 Copilot 的原生渲染能力：现在的 Microsoft Copilot 或 GitHub Copilot 聊天窗口原生支持 Mermaid 语法渲染。当它吐出 ` ```mermaid ` 代码块时，你的聊天窗口里会自动展示出彩色的流程图，直接满足你“流程图方式显示”的需求。
3. 零成本、即用即走：不需要任何 Python 环境、不需要申请任何 API Key，只要把这套提示词框架存进你的记事本里，随时粘贴进 Copilot 就能立刻办公。

你可以直接把第一步的提示词发给你现在的 Copilot 工具，看看它的反应。在日常体验中，你是否希望针对你们团队特定的安全规范（如数据脱敏、高并发要求）让它提出更严格的审计质问？


---
对于您在本地使用的 VS Code 里的 GitHub Copilot 和 Copilot CLI，它们的上下文存储逻辑、管理方式以及持久化配置技巧各有不同。

---

## 1. 📂 VS Code 里的 GitHub Copilot (Chat 窗口)

在 VS Code 的 Copilot Chat 侧边栏中，您的 Agent 框架和喂给它的代码数据的生命周期如下：

- 当前会话内存：上下文直接保存在当前 Chat 会话窗口的运行内存中。只要您不点击面板上方的 “New Chat（新建对话）” 按钮或关闭 VS Code，Copilot 就会通过滑动窗口机制，在后续对话中一直记住自己是“架构师 Agent”。
- 物理历史存储：GitHub Copilot 会将您的本地历史对话加密缓存在本地计算机的用户数据目录中。
    
    - _Windows 路径_：`%APPDATA%\Code\User\globalStorage\github.copilot-chat`
    - _macOS 路径_：`~/Library/Application Support/Code/User/globalStorage/github.copilot-chat`
    - 这些历史仅供您在 VS Code 中翻阅（通过点击 `Show Past Chats` 按钮），不会自动跨窗口跨工程跨设备共享。
    

## 💡 VS Code 专属技巧：免复制粘贴，让 Agent 在当前工程永久常驻

为了不让您每次开新对话都复制粘贴那段“架构师技能指令”，您可以利用 GitHub Copilot 的 自定义指令文件 功能：

1. 在您当前的工程根目录下，创建一个名为 `.github/copilot-instructions.md` 的文件。
2. 将前文中我为您编写的 第一步：Agent 核心技能字典 提示词原封不动复制进去并保存。
3. 效果：此后，在这个工程下打开的任何全新 Copilot Chat 窗口，Copilot 都会在后台无形中先读取这个文件，直接以“架构师 Agent”的身份和特定格式为您服务。

---

## 2. 💻 Copilot CLI (命令行工具)

如果您在终端（Terminal）中使用的是 `gh copilot`（GitHub Copilot CLI），它的上下文存储机制与图形界面完全不同：

- 完全“无状态”（Stateless）的一性次交互：Copilot CLI 的核心设计目标是“快捷命令解释与执行”。当你输入 `gh copilot explain "一段指令"` 时，它没有任何会话上下文的概念。每一次回车都是一次完全独立的、全新的请求。
- 上下文存储位置：它不存储任何长对话内容。它的“工作记忆”仅限于你单次输入到命令行中的这一句话，以及当前终端所处的路径名称。
- 不适合复杂分析：因此，Copilot CLI 无法像 VS Code Chat 窗口那样通过连续喂数据来实现复杂的跨工程、跨 Jira/Confluence 数据的深度 Agent 审计任务。

## 💡 Copilot CLI 专属技巧：通过别名（Alias）封装单步 Agent 技能

虽然 CLI 无法进行多轮复杂分析，但您可以把“单工程代码转 Mermaid 流程图”的单一 Agent 技能封装成一个终端别名，快速调用。  
例如，在您的 `~/.bashrc` 或 `~/.zshrc` 中配置这样一个别名：

```bash
alias explain_flow="gh copilot explain \"请分析当前目录下的核心业务代码逻辑，并强制只用标准的 Mermaid.js 语法(graph TD)输出一份数据生命周期流程图，不要带有任何额外的解释文字：\""
```

配置后，在任何本地代码工程目录下，只需在终端敲入 `explain_flow`，CLI 就会以特定 Agent 技能视角直接为你输出当前代码的流程图。

---

## 🔒 终极安全避坑指南（针对企业本地代码）

由于您分析的是公司内部的本地代码、Jira 和 Confluence，请务必在 VS Code 设置中检查以下开关：

1. 打开 VS Code 设置（`Ctrl + ,` 或 `Cmd + ,`）。
2. 搜索 `github.copilot.telemetry` 或 `training`。
3. 确保关闭“允许 GitHub 使用我的代码段进行模型训练”的相关勾选项（如果您使用的是 GitHub Copilot Business/Enterprise 企业版，该选项默认在组织端关闭并强制加密隔离，无法用于公网训练，非常安全）。

您接下来打算先尝试在 VS Code 中配置这个 `.github/copilot-instructions.md` 常驻架构师文件，还是直接在当前窗口试一下它的 Mermaid 图形渲染效果？