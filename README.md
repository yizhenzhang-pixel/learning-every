````markdown
# Learning Everything · 30 天 AI 深度学习规划助手

一个完全前端、零后端部署的「学习路径生成器」。  
你只需要提供一个想学的主题 + 自己的 Gemini API Key，它就能自动为你：

- 生成 **30 天循序渐进学习大纲**
- 为每天撰写 **2000–3000 字深度讲义（Markdown + 公式 + 表格）**
- 按照艾宾浩斯曲线安排 **复习任务**
- 提供一个内置的 **AI 导师聊天窗口**，随时答疑

> 所有请求都直接从浏览器发送到 Google 的 Gemini API，**不经过任何第三方服务器**。

---

## ✨ 功能特点

- 🧱 **30 天系统学习路径**
  - 自动分为四个阶段：基础 / 核心 / 应用 / 整合
  - 每天包含：`day`、`title`、`goals`（2 个学习目标）

- 📚 **3000 字级深度讲义**
  - 自动判断偏文科 / 理科，生成不同结构
  - 支持 Markdown 标题、列表、引用、代码块
  - 公式用 `$...$` / `$$...$$` 包裹，并通过在线 LaTeX 渲染

- 🔁 **艾宾浩斯复习计划**
  - 固定使用间隔：+1 / +3 / +7 / +15 / +30 天
  - 在右侧「Review Tasks」区域提示当天应复习哪些日期的内容

- 🤖 **AI 导师对话**
  - 结合当前主题 + 所在学习日，作为系统上下文
  - 聊天记录保存在当前页面会话中

- 💾 **本地记忆 API Key**
  - 使用 `localStorage` 存储在浏览器本地：`le_gemini_api_key`
  - 方便你多次使用，无需重复粘贴

- 🎨 **现代化 UI 设计**
  - Tailwind CSS + 单文件 React 应用
  - 左侧：大纲 / 日历式导航  
    中间：当天讲义内容  
    右侧：进度条 + 复习任务 + AI 聊天

---

## 🧩 技术栈

- **前端框架**：React 18（UMD 版本，浏览器直接运行）
- **样式**：Tailwind CSS（CDN 引入）
- **构建方式**：直接在浏览器使用 `@babel/standalone` 编译 JSX，**无需打包工具**
- **大模型接口**：Google Gemini API（Generative Language API）
  - 模型：`gemini-2.5-flash-preview-09-2025`
- **渲染**：
  - 自定义 Markdown 渲染器 `SimpleMarkdown`
  - 在线 LaTeX 渲染：`https://latex.codecogs.com/svg.latex`

---

## 🚀 快速开始

### 1. 获取 Gemini API Key

1. 打开 Google AI Studio（通常是 `https://aistudio.google.com/`）
2. 登录你的 Google 账号
3. 在控制台中创建 API Key
4. 复制这串 Key，备用

> **注意**：免费额度和具体限制以官方说明为准。

---

### 2. 本地打开项目

本项目是单文件应用，只要一个 `index.html` 就能跑起来。

**方法一：直接双击打开**

1. 把代码保存为 `index.html`
2. 双击用浏览器打开  
   > 某些浏览器可能对本地文件的 `fetch` 有额外限制，如果接口报错，可以尝试方法二。

**方法二：启动一个简单本地服务器（推荐）**

比如使用 Python：

```bash
# Python 3
python -m http.server 8000
````

然后浏览器访问：

```text
http://localhost:8000/index.html
```

---

## 🛠 使用说明

1. 打开页面后，在首页看到两个输入框：

   * 「想深入学习的领域」：例如：

     * `微观经济学`
     * `复杂系统与涌现`
     * `深度学习原理`
     * `React 原理与性能优化`
   * 「Gemini API Key」：粘贴你在 AI Studio 里申请的 Key

2. 点击 **「生成学习路径」**：

   * 第一步：调用 `fetchStudyOutline` 生成 30 天学习大纲（结构化 JSON）
   * 第二步：组装成内部 `plan`，并自动选中第 1 天
   * 第三步：自动为第 1 天调用 `fetchDayContent` 生成详细讲义

3. 左侧：

   * 显示 1–30 天的列表，包含：

     * 阶段标签（基础 / 框架 / 应用 / 整合）
     * 今日是否完成（打卡）
     * 今日是否为其他天的复习目标（黄标 + 数量）

4. 中间内容区：

   * 标题区域：Phase、Day、学习目标（`goals`）
   * 内容区域：渲染好的 Markdown + 公式 + 表格
   * 底部打卡按钮：

     * 点击后会标记当天为已完成，右侧进度条更新

5. 右侧：

   * **Progress**：统计已打卡天数 / 总天数，进度条显示百分比
   * **Review Tasks**：显示当前天应该复习的历史日期，点击可跳转
   * **AI Tutor**：

     * 你可以提问「今天看不懂的概念」「让它用故事解释某段推导」等
     * 上下文中包含当前学习主题与天数

---

## 🔐 安全与隐私

* **API Key 存储**

  * 仅通过浏览器 `localStorage` 存在本地：键名 `le_gemini_api_key`
  * 不会被上传到任何第三方服务器（除你的浏览器访问 Gemini 官方接口外）

* **数据传输**

  * 所有请求直接发往官方 `https://generativelanguage.googleapis.com` 端点
  * 建议通过 HTTPS 访问本页面

* **内容存储**

  * 项目没有实现持久化后端，讲义内容和聊天记录只存在当前会话中
  * 刷新页面后会清空（除了 API Key）

---

## 📁 文件结构

目前是极简单文件结构：

```text
.
└── index.html    # 你现在看到的全部代码都在这里
```

如需拆分为多文件 / 模块化，可以按以下方向改造：

* 把 React 代码拆到 `src/` 目录，改用打包工具（如 Vite）
* 把 Markdown 渲染器单独抽成组件文件
* 引入类型系统（例如 TypeScript）

---

## 🧱 核心模块说明（简略）

* `SimpleMarkdown`：自实现 Markdown 渲染

  * 支持：标题、列表、有序列表、引用、代码块、表格、行内代码、LaTeX 公式
* `fetchStudyOutline(topic, apiKey)`：

  * 调用 Gemini 生成 30 天 JSON 结构大纲
* `fetchDayContent(topic, dayInfo, apiKey)`：

  * 为某一天生成 2000–3000 字讲义
* `fetchChatResponse(history, topic, dayContext, apiKey)`：

  * 用聊天历史 + 主题 + 当前天数 作为上下文进行问答
* `generateReviewSchedule(days)`：

  * 生成艾宾浩斯复习日程
* `assemblePlan(outlineData)`：

  * 把大纲和复习日程合并成最终 `plan` 数组

---

## 🔧 二次开发建议

如果你想在这个项目基础上继续扩展，可以考虑：

* ✅ 增加「导出」功能：

  * 将单日讲义导出为 Markdown / PDF
* ✅ 增加多语言支持：

  * 根据用户选择生成中文 / 英文讲义
* ✅ 增加「重新生成这一天讲义」按钮：

  * 对某一天不满意可以重试
* ✅ 持久化学习进度：

  * 使用 `localStorage` 或接入后端存储打卡状态和内容
* ✅ 自定义学习时长：

  * 不局限 30 天，允许创建 7 / 14 / 60 天计划

---

## ⚠️ 注意事项

* 当前使用的模型名为：`gemini-2.5-flash-preview-09-2025`
  如果之后官方更换 / 下线，请在以下位置同步修改：

  ```js
  const endpoint = `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview-09-2025:generateContent?key=${apiKey}`;
  ```

* 如果接口报错：

  * 检查 API Key 是否正确、是否有权限
  * 检查是否命中用量限制
  * 检查当前网络是否能访问 Google 域名

---

## 📄 许可证

个人学习 / 实验用途随意使用。
如用于商业场景，请根据你依赖的第三方服务（例如 Gemini API）条款自行评估合规性。
