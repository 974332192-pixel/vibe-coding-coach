# Vibe Coding Coach# Vibe Coding Coach

> 一个单文件 HTML 实现的「对话式 AI 教练」：Vibe Coding Coach 是一款通过8步结构化引导与智能工具匹配，将模糊想法转化为标准化AI开发执行清单的Vibe Coding前置导航工具。

👉 **在线立即体验：(https://p1chtzui5gtyi.space.mcode.cn)**

![demo](https://img.shields.io/badge/demo-single_file-orange) ![stack](https://img.shields.io/badge/stack-vanilla_JS-blue) ![llm](https://img.shields.io/badge/llm-DeepSeek-4d6bff) ![search](https://img.shields.io/badge/search-博查-00a86b)

------

## ✨ 这是什么

Vibe Coding Coach 致力于降低 AI 辅助编程的门槛，将“Vibe Coding”（氛围编程）从一种模糊的概念转化为可执行、可复用的标准化工作流。它不替代 AI 编码工具，而是vibe coding的引导助手，帮助用户在动手写代码前，通过结构化引导厘清需求、匹配工具、生成执行清单，让 AI 协作从“试错式对话”升级为“目标导向的精准开发”，真正实现“想法到项目”的高效转化。

适合：适合：

- 🎓 想入门编程/AI 开发但不知从哪下手的纯小白 
- 💼 准备做作品集/求职 demo 的开发者 
- 🛠️ 想用 AI 解决身边重复劳动的非技术人
- 🧪 给面试官演示「对话式 AI 产品」怎么设计

---

## 🚀 快速开始

**单文件，零依赖，浏览器直接打开：**

```bash
# 方式 1：直接双击打开
open index.html

# 方式 2：本地起个静态服务（推荐，避免某些 API 跨域问题）
python3 -m http.server 8000
# 然后访问 http://localhost:8000
```

打开后 **无需任何配置**，API Key 和联网搜索 Key 已经预置在文件里（`BUILT_IN_CONFIG`）。想换自己的 key，点右上角 ⚙️。

---

✨ 产品亮点
🧠 不会 "失忆" 的陪练：全程记住你的技术背景、预算、网络环境、核心需求，不会聊着聊着就忘记你是纯小白 / 零预算，不用反复重复信息
🎯 不瞎推荐的工具库：内置 37 个主流 AI 编程 / Agent / 设计 / 部署工具库，根据你的实际情况从 5 个维度加权匹配，不会上来就推荐贵价 / 需要翻墙的不适合工具
📝 聊完直接拿方案：对话过程中右侧自动生成完整项目计划书，包含工具清单、避坑提醒、实施步骤，聊完直接复制就能用，不用自己零散记笔记

---

## 🗺 8 步引导流程

💡 设计思路：我将「从模糊想法到可落地方案」的完整路径拆分为 8 个低门槛小步骤 —— 步骤过多会劝退纯小白，步骤过粗会让用户不知道如何回答；每一步都提供 emoji 选项按钮降低输入成本，同时保留自由输入框，流程是脚手架而非围墙，AI 可以接住任何用户问题。

| Step | 名称 | 目的 | 关键输出 |
|------|------|------|----------|
| **1** | 破冰与用户画像 | 摸清用户背景 | `profile.background` |
| **2** | 明确核心目的 | 区分探索/求职/痛点/商业 | `profile.purpose` |
| **3** | 挖掘具体痛点 | 剥洋葱 + 联网案例调研 | `profile.pain` |
| **3.5** | 痛点拆解 + 方案生成 | 给出 A/B 两个工程级方案 | `profile.pickedPlan` |
| **4** | 确定产品形态 | Skill / Agent / 融合体 | `profile.form` |
| **5** | 网络环境 | 国内/科学上网 | `profile.network` |
| **6** | 预算 | 0-50 / 50-150 / 150+ 元/月 | `profile.budget` |
| **7** | 工具精准推荐 | RAG + 联网 + 过滤 | `profile.pickedTool` |
| **8** | 获取工具 + 避坑 | 官网/注册/API Key 流程 | `plan_doc` |

每一步都用 **option button** 引导（3-4 个 emoji 选项），用户也可以随时在输入框自由打字 —— 流程是脚手架不是围墙，AI 会接住任何跑题。

---

## 🧠 核心机制

### 1. 实时记忆系统（`profile` + 决策历史）

- `profile` 对象跨 step 累积 9 个字段（背景、目的、痛点、形态、网络、预算、工具、方案、关键决策）
- 每轮 LLM 调用的 system prompt 都注入一个 **🧠 实时记忆快照**，让 AI "看到"用户聊到哪了
- 决策历史以 **时间线** 形式展示在方案书里，让用户能回看自己每一步的选择

### 2. RAG 工具库（37 个工具）

- 内置一份 JSON 工具库：覆盖 编程 IDE（Cursor / Trae / Codex）/ Agent 平台（扣子 / Dify）/ 设计（Figma AI）/ 部署（Vercel）等
- 按 `[背景, 目的, 形态, 网络, 预算]` 五个维度加权匹配
- Step 7 工具推荐时先过 RAG，没命中再走联网

### 3. 联网搜索（博查 API）

- Step 3 调研案例、Step 7 推荐最新工具时触发
- 通过博查（BochaiAI）API 检索，DeepSeek 联网搜索底层用的就是它
- key 没填也能跑，RAG 库够用；填了能查 2026 年最新工具

### 4. 演示版 vs 真实模式（`state.isRealMode`）

- **演示版**：按节点走脚本，AI 回复写死在 `NODES` 里，**不消耗 token**，适合 demo
- **真实模式**：每条消息都走 DeepSeek API，能自由对话、跳出节点限制
- 切换条件：localStorage 里有 `vcc_llm_config` 就进真实模式
- **预置 key 让用户一打开就进真实模式**，省去手动配置

### 5. 方案书实时生成（右侧预览）

- 跟着对话流，方案书在右边实时拼装：记忆状态 + 决策时间线 + 工具卡片 + 风险 + 实施步骤 + 收尾建议
- 聊完所有阶段直接可以 **复制 / 截图** 当 PRD 用

---

## ⚙️ 配置

打开右上角 ⚙️，可以改：

| 字段 | 说明 | 默认 |
|------|------|------|
| 服务商 | DeepSeek / OpenAI / Moonshot / 通义千问 / 自定义 | DeepSeek |
| Base URL | OpenAI 兼容格式的 API 入口 | `https://api.deepseek.com/v1` |
| 模型 | 服务商支持的模型列表 | `deepseek-chat` |
| API Key | 你的 LLM API Key | 预置 |
| 联网搜索 Key | 博查 API Key | 预置 |

🔒 隐私说明：所有 API Key 配置、对话记录、个人信息全部存储在浏览器本地 LocalStorage，**不上传任何服务器**，数据完全由用户自己掌控。

---

🔧 技术实现与二次开发
核心机制
实时记忆系统（profile + 决策历史）
profile 对象跨 step 累积 9 个字段（背景、目的、痛点、形态、网络、预算、工具、方案、关键决策）
每轮 LLM 调用的 system prompt 都注入一个 🧠 实时记忆快照，让 AI "看到" 用户聊到哪了
决策历史以时间线形式展示在方案书里，让用户能回看自己每一步的选择
RAG 工具库（37 个工具）
内置一份 JSON 工具库：覆盖 编程 IDE（Cursor / Trae / Codex）/ Agent 平台（扣子 / Dify）/ 设计（Figma AI）/ 部署（Vercel）等
按「背景，目的，形态，网络，预算」五个维度加权匹配
Step7 工具推荐时先过 RAG，没命中再走联网
联网搜索（博查 API）
Step3 调研案例、Step7 推荐最新工具时触发
通过博查（BochaiAI）API 检索，DeepSeek 联网搜索底层用的就是它
key 没填也能跑，RAG 库够用；填了能查 2026 年最新工具
演示版 vs 真实模式（state.isRealMode）
演示版：按节点走脚本，AI 回复写死在 NODES 里，不消耗 token，适合 demo
真实模式：每条消息都走 DeepSeek API，能自由对话、跳出节点限制
切换条件：localStorage 里有 vcc_llm_config 就进真实模式
预置 key 让用户一打开就进真实模式，省去手动配置
方案书实时生成（右侧预览）
跟着对话流，方案书在右边实时拼装：记忆状态 + 决策时间线 + 工具卡片 + 风险 + 实施步骤 + 收尾建议
聊完所有阶段直接可以复制 / 截图当 PRD 用
## 📂 项目结构

```
vcc/
├── index.html          # 一切都在这（HTML + CSS + JS，约 2700 行）
└── README.md           # 本文件
```

这是一个 HTML 文件。CSS 全部内联在 `<style>`，JS 全部内联在 `<script>`，LLM system prompt 是模板字符串。**整个产品 ≈ 156 KB**。

代码组织（行号大致）：

```
~140   HTML 骨架（聊天区 + 方案书预览 + 设置弹窗）
~190   状态管理（state, profile, confirmed）
~210   决策历史（addHistory / renderTimeline）
~250   实时记忆快照（getMemorySnapshot）
~490   RAG 工具库（37 个工具的 JSON）
~560   8 步节点定义（var NODES = {...}）
~990   方案书渲染（renderPlan）
~1200  教练 system prompt（COACH_PROMPT）
~1500  初始化（init, BUILT_IN_CONFIG, openSettings, saveConfig）
~1700  消息路由（节点导航 + 锁定检测）
~1900  输入处理（用户消息 + 真实模式调用 DeepSeek）
~2300  联网搜索（博查 API 调用）
~2400  决策路由（tool_calls JSON 解析）
```

---

## 🔧 自定义 / 扩展

### 改教练人设

编辑 `COACH_PROMPT`（约 1200 行），里面定义了：

- 语气基线、禁止行为（如不能说"我们已经聊了 X 轮"）
- 步骤闭环规则
- 何时用 RAG、何时联网
- 输出格式（HTML 标签约定）

### 改引导流程

编辑 `var NODES = {...}`（约 560 行）。每个节点结构：

```js
s1: {
  step: 'Step 1：...',           // 顶部 step indicator 文案
  agent: '欢迎...',                // 字符串 或 function(p){...} 动态生成
  question: '你...？',             // 引导问题（可选）
  chips: [                        // 底部 option buttons
    {l: '🌱 <b>纯小白</b>：...', n: 's2', set: {background: '纯小白'}},
    ...
  ]
}
```

- `l`：按钮文案（支持 HTML）
- `n`：点击后跳到哪个节点
- `set`：写入 `profile` 的字段
- `finalizePlan`：可选，标记当前 step 已完成方案生成

### 改 RAG 工具库

直接编辑 `TOOL_DB` 数组（约 490 行），每条工具的结构：

```js
{
  name: 'Cursor',
  category: 'AI 编程 IDE/编辑器',
  strength: '...',      // 一句话优势
  difficulty: '⭐⭐',   // 难度
  network: '🇨🇳 国内直连', // 网络需求
  deploy: '🟢 零部署',  // 部署成本
  cost: '...'           // 价格
}
```

匹配算法在 `matchTools(profile)`（约 750 行），按 5 个维度加权打分。

### 改预置 Key

直接改 `BUILT_IN_CONFIG` 和 `BUILT_IN_BOCHA_KEY`（约 1584 行）。

⚠️ **重要：把含真实 key 的 HTML 部署到公网 = 公开泄露 key**。生产环境请改用：
- Cloudflare Worker / 网关代理（key 放服务端 env）
- Cloudflare Pages Function + 环境变量
- 或者干脆去掉预置，让用户自己填

---

## 🐛 已知问题 / 待优化

- [ ] **key 安全**：当前 key 硬编码在 HTML 里，仅适合 demo。生产前必须重构（见上）。
- [ ] **联网 key 错别字**：注释里写的 `vcc_tavily_key` 是历史遗留，实际用的是博查。命名建议改成 `vcc_bocha_key`。
- [ ] **演示版文案硬编码**：所有 8 步的 AI 回复都写死在 NODES 里，改起来要全文搜。
- [ ] **方案书导出**：目前只能复制/截图，没法一键导出 PDF/Markdown。
- [ ] **多轮上下文窗口**：真实模式没做历史消息自动截断，长对话会撑爆 token。

---

## 📜 License

MIT
