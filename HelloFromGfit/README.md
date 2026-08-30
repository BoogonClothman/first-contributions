# gFIT

> Talk is cheap. Show me the code. **Then go for it.**

诸位好，我是 gFIT（[@lllxxxxxlll](https://github.com/lllxxxxxlll)），AI Agent Engineer，专注把 AI Agent 技术应用到分布式系统的根因分析自动化 —— **在 infra 中懂 Agent，在 Agent 中懂 infra。**

---

## 📝 完整实战指南（本项目构建全过程）

> **推荐新入门同学对照看：** 这份会话记录就是我**从零开始美化 Profile README → 做个人网站 → 到 openHIT 提交第一次 PR** 的完整过程，每一步为什么做、踩了什么坑、怎么排查全记录了。

🔗 **[TRAE 会话记录：从 Profile README 美化到 First Contribution](https://share.traecontent.cn/share/EQI.W7J_EDI7J9?enter_from=mobile)**

会话里覆盖的内容（对照这份记录，你也能走完自己的第一次 PR）：

1. **同名仓库原理**：为什么 `<用户名>/<用户名>` 能渲染到主页？为什么 `<用户名>.github.io` 能做个人网站？—— GitHub 两条独立的 convention，以及 public/private 对可见性的影响。
2. **Profile README 美化实操**：Banner 配色、双主题适配（dark/light mode）、徽章方案选型（为什么放弃 Top Languages 动态卡改用 shields.io 静态徽章）、贪吃蛇 Actions。
3. **GitHub Actions 是什么**：和公司 pipeline 类比（触发 → 构建 → 部署三段式），第一次写 `.github/workflows/xxx.yml` 时要注意的 `on:` / `permissions:` / `uses:` 三件事。
4. **第一次提 PR 的完整流程**：fork 上游 → 克隆自己 fork → 建分支 → 改内容 → push → 开 PR → 等 review。
5. **沙箱 & CI 中的鉴权机制**：为什么应用层 OAuth token 不能直接给 `git push` 用？device flow 登录 gh CLI 的实操、凭据隔离的真实含义。

---

## 给新入门同学的建议 ✨

1. **尽早 fork 一个 first-contribution 仓库走一遍完整流程** —— 比读十遍教程都有效。不知道怎么写就直接把需求丢给 AI，但一定要打开 diff 看一眼 AI 到底改了什么。
2. **开自己的同名仓库（`<你的用户名>/<你的用户名>`）练手 profile README** —— 完全零门槛，push README 就能看到改了什么，是学 GitHub 最好的第一份作业。接着搞 `xxx.github.io` 仓库搭个人博客，会遇到 Actions、build、部署，一套下来就理解什么是 CI/CD 了。
3. **Talk is cheap, show me the code —— 然后 go for it。** 别等"准备好"：把想法落到 commit，把项目部署到公网，哪怕一开始很丑也比空想一万次强。刷题、比赛、做 toy project、找实习——**动作本身就会倒逼学习。**
4. **别怕跟组织里的人交流**：提 issue 要描述清楚复现步骤、改了什么、期望什么；发 PR 跑的是 Action 失败了就点开日志读 10 行，答案几乎都在里面。
5. **用 AI 但别丢工程基本功**：`git diff`、`git status`、读日志、追源码，这些能力 AI 替不了你。AI 写的代码，**push 前一定要自己 review**。

## 主攻方向

- 🧠 **AI / Agent 工程**：Eino · MCP · ReAct · Plan-Execute · 自动化值班 Agent（RCA 场景）
- 🖥 **后端 & 分布式**：Go · SpringBoot · RedKV · Kafka · Redis · 根因定位
- ☁ **云原生 / Infra**：Docker · Nginx · Linux · Prometheus · JVM

## 欢迎来玩 👋

- 👤 **GitHub Profile**：[github.com/lllxxxxxlll](https://github.com/lllxxxxxlll) —— Profile README 是赛博风，做个参考
- 🌐 **个人网站 / 博客 / 项目**：[lllxxxxxlll.github.io](https://lllxxxxxlll.github.io/) —— 有 Agent、算法、踩坑笔记
- 📮 **邮箱**：[3108827314@qq.com](mailto:3108827314@qq.com)

期待和 openHIT Lab 的各位一起写代码、做项目、冲 PR、go for it 🔥