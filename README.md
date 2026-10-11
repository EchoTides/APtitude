# APtitude — AP 刷题练习器

AP + aptitude：帮你练出 AP 考试的好状态。

单文件 AP 练习 Web 应用：AI 出题（选择题 + 论问题）、作答、AI 批改、按课程归档练习记录、刷题曲线与成绩报告，界面风格参考 College Board 的 AP Classroom。

> ⚠️ Unofficial practice tool. Not affiliated with or endorsed by College Board.

## ✨ 功能特性

| 模块 | 说明 |
| --- | --- |
| **多供应商** | OpenAI (ChatGPT)、DeepSeek、Anthropic (Claude)、OpenRouter，或任意 OpenAI 兼容端点；Claude 自动切换原生 `/v1/messages` 协议 |
| **AI 出题** | AP 风格题目生成，支持 Multiple Choice / Free Response / Mixed 三种格式；需要图表时由 AI 输出结构化数据，应用渲染为数据表格 / SVG 柱状图 / 折线图 |
| **选择题作答** | 逐题作答、进度条、每题可配置"验证机会"（Check Answer 只判对错、不泄露正确答案，答对即锁定） |
| **论问题（FRQ）** | 带评分标准与满分范文；提交后 AI 按评分标准自动批改（逐题给分 + 针对性反馈），失败可重试 |
| **做题记录** | 每次练习按课程独立归档（开始/提交日期、得分、逐题作答轨迹、首次选择、修改次数、验证日志、用时） |
| **统计视图** | Home 课程网格（35 门课程）、Progress 每门课程得分曲线、Reports 最近 30 天答题量与正确率（FRQ 加权） |
| **历史管理** | Past Practice 列表支持 Resume 续做 / Review 回顾 / 删除；同科目多次练习互不覆盖 |
| **隐私** | API Key 仅存本浏览器 localStorage，只发往你配置的端点；所有练习数据仅存本地 |

## 🚀 快速开始

1. 用浏览器打开 `index.html`（或部署到任意静态托管）
2. 首次进入自动弹出设置面板：选择供应商预设（自动填入 Base URL 与默认模型）→ 填入 API Key
3. 选好科目、题量（5/10/20）、难度、验证机会次数、题目格式（MCQ / FRQ / Mixed）→ Test Connection → Save
4. 首页点击课程卡片 → Generate Questions 开始刷题
5. 页面内 **Tutorial** 导航包含完整使用教程（含 FAQ）

## 🛠 技术说明

- **单文件** `index.html`：内联 CSS + 原生 JavaScript，零外部依赖
- 调用 `POST {baseURL}/chat/completions`（Anthropic 为 `/v1/messages`）；出题使用 `response_format: {"type":"json_object"}`，服务商不支持时自动降级重试一次
- 解析容错：自动剥离 ```json 代码围栏、字段级校验、友好错误提示
- 所有动态内容经 HTML 转义（XSS 防护）；数据持久化于 localStorage（配置 + 练习记录）

## 📦 部署到 GitHub Pages

1. 本仓库即静态站点：`index.html` + `.nojekyll`
2. 推送到 GitHub 后，在仓库 **Settings → Pages** 将 Source 设为 `main` 分支根目录（`/`）保存即可

---

Made with ♥ by Ambar
