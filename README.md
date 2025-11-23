
Learning Everything

这是一个基于 Gemini API 的 30 天学习规划工具。
输入学习主题和你的 Gemini API Key，即可自动生成：

1. 30 天学习大纲
2. 每天 2000–3000 字的详细讲义
3. 艾宾浩斯式复习计划
4. 内置 AI 导师问答窗口

所有请求均在浏览器本地执行，直接发送到 Google Gemini 接口，没有任何后端服务器。

---

功能特点

1. 30 天学习路径
   自动为你的主题生成 day、title、goals，并分成四个阶段：

   * 1–5 天：基础期
   * 6–15 天：原理/框架期
   * 16–25 天：应用期
   * 26–30 天：整合期

2. 深度讲义

   * 每天 2000–3000 字内容
   * 自动判断文科或理科结构
   * 自动排版
   * 支持代码块与公式

3. 复习计划
   按照固定间隔自动生成复习任务：+1、+3、+7、+15、+30 天。

4. 内置 AI 导师
   可以随时提问，AI 会结合当前主题和当前学习日回答。

5. 本地保存 API Key
   使用 localStorage 保存，用于下次自动填充。

---

技术说明

* React 18（CDN 方式）
* Tailwind CSS
* Babel Standalone（浏览器直接编译 JSX）
* Gemini Generative Language API
* 自定义 Markdown 渲染器
* 在线 LaTeX 公式渲染

---

使用步骤

1. 在 Google AI Studio 申请你的 Gemini API Key
2. 将项目保存为 index.html
3. 本地打开即可
   推荐使用简易本地服务器，例如命令：
   python -m http.server 8000
4. 页面打开后，输入学习主题与 API Key，点击生成学习路径即可使用。

---

界面结构

左侧：学习大纲
中间：当天讲义内容
右侧：学习进度、复习任务、AI 导师聊天窗口

---

主要功能模块（逻辑）

* fetchStudyOutline
  用于向 Gemini 请求 30 天大纲（结构化 JSON）。

* fetchDayContent
  用于为每一天生成详细讲义。

* fetchChatResponse
  用于处理右侧 AI 对话窗口。

* generateReviewSchedule
  根据算法生成复习计划。

* assemblePlan
  将原始大纲和复习计划组合成最终可显示结构。

---

常见问题

1. 刷新页面内容是否会丢失？
   会。讲义内容与聊天记录只存在本次会话中。
   只有 API Key 会保存在浏览器 localStorage。

2. 网络错误怎么办？
   检查 API Key 是否有效、网络是否能访问 Google API。

3. 为什么必须用小型本地服务器？
   某些浏览器会对 file:// 环境的 fetch 发起限制，导致 Gemini API 请求失败。

---

许可

可自由用于学习与个人项目。
如用于商业用途，请自行确认 Gemini API 服务条款。

