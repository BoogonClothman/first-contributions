# 新手快速上手 GitHub + Profile README + 第一次提 PR 指南

> 作者：gFIT ([@lllxxxxxlll](https://github.com/lllxxxxxlll))
> 原始构建会话记录：[TRAE 共享链接](https://share.traecontent.cn/share/EQI.W7J_EDI7J9?enter_from=mobile)
> 适用对象：刚加入 openHIT-Lab、不太熟悉 GitHub 规范、想尽快把 profile 和 first PR 跑通的同学。

---

## 为什么读这份指南

你可能已经被三件事绕晕过：
1. **为什么有个仓库名必须和用户名一模一样？**
2. **`.github/workflows/xxx.yml` 写进去以后到底发生了什么？**
3. **第一次提 PR 到底要走哪几步？fork 什么？clone 什么？push 到哪？**

这份指南按"学习梯度"排序，每一步都有**可验证的产出**——跟着做完，你会得到：

- ✅ 一个面试官点进来会眼前一亮的 GitHub Profile 主页
- ✅ 一个已上线的个人博客（`xxx.github.io`）
- ✅ 会用 AI 写代码但知道 **push 前一定要自己 review diff**
- ✅ 第一个 merged PR（就是你正在看的这个 first-contributions 仓库）

---

## 0. 先把一个概念讲透：GitHub 的"同名仓库约定"

**同名仓库 = 两种不同用途，各走各的规则。** 这是新手最容易搞混的根源，放在最前面讲。

| 用途 | 仓库名长什么样 | 显示在哪 | visibility 要求 | 背后规则 |
|---|---|---|---|---|
| **A. Profile README**（美化主页用） | `<用户名>/<用户名>`，比如 `lllxxxxxlll/lllxxxxxlll` | `github.com/<用户名>` 主页正中间，头像和 Pinned 之间 | **必须 public**，否则不渲染 | 仓库名 == 用户名，且根目录有 `README.md`，GitHub 就自动渲染 README 到公开主页。**没有构建步骤**，push 完立刻生效。 |
| **B. GitHub Pages 个人网站**（搭博客用） | `<用户名>/<用户名>.github.io`，比如 `lllxxxxxlll/lllxxxxxlll.github.io` | `https://<用户名>.github.io` 独立域名 | public（private Pages 是 Team/Pro 付费） | 仓库名 == `<用户名>.github.io`，GitHub 自动启用 Pages，按仓库分支的部署源发布静态文件。一般配合 Actions 先 build 后 deploy。 |

**这是两个完全独立的仓库，互不影响。** 你可以同时有 A 和 B，它们的内容、构建流程、访问入口全部没关系。

> 踩坑备忘：Profile README 仓库如果你设置成了 private，**push 再多也不会在主页显示**。记得改成 public。

---

## 第一站：Profile README（零构建、成就感最快、30 分钟搞定）

这是你最好的 GitHub 第一份作业。零构建、零配置，推完立刻能看到效果。

### 1.1 建仓库

在 GitHub 右上角 **New Repository**：
- **Repository name** 必须完全等于你的用户名（比如用户 `lllxxxxxlll` 就填 `lllxxxxxlll`，大小写 GitHub 不敏感，但建议全小写）
- **Public**（必须）
- **Add a README file** 打钩
- Create Repository

### 1.2 写 README.md

README 就是普通 Markdown，怎么好看怎么写。社区里有几个常用"组件"能让你的 profile 立刻上一个档次：

| 组件 | 做什么 | 链接模板 |
|---|---|---|
| Banner 渐变横幅 | 顶部一整块大 banner + 名字/副标题，最提升气质 | [capsule-render.vercel.app/api](https://github.com/kyechan99/capsule-render) 拼参数即可 |
| Shields 徽章 | 个人网站/邮箱/状态/技术栈小按钮，100% 稳定不挂 | [shields.io](https://shields.io) 支持 GitHub/语言/工具 1000+ 种 |
| 打字机效果 | 几行字轮播切换的动效，不花哨但很有味道 | [readme-typing-svg.demolab.com](https://github.com/DenverCoder1/readme-typing-svg) |
| Contribution 贪吃蛇 | 蛇吃掉你的 contribution 格子，挺有趣，而且是用 GitHub Actions 自动生成的 | [Platane/snk](https://github.com/Platane/snk)（详见第三站） |

> ⚠ 避坑提示：社区里曾经很火的 `github-readme-stats`（Top Languages 动态卡片）**现在基本全面崩了**，所有 vercel / cloudflare worker 镜像要么 rate limit 要么直连失败。**别用，改用 shields.io 的语言徽章**（静态但永不挂），看 [我的 profile](https://github.com/lllxxxxxlll) Languages·Activity 区块就是这么写的。

### 1.3 主题适配（必做，否则一半人看着丑）

GitHub 用户一半用 light 一半用 dark。你写的图片不会自动换色，所以要做**双主题切换**，用 GitHub 官方支持的方案：

```html
<picture>
  <source media="(prefers-color-scheme: dark)"  srcset="xxx-dark.png#gh-dark-mode-only" />
  <source media="(prefers-color-scheme: light)" srcset="xxx-light.png#gh-light-mode-only" />
  <img src="xxx-light.png" alt="xxx" />
</picture>
```

Banner、蛇图、徽章都可以这么套两套。我的 profile README 里 Banner / Motto / Status / Snake / Footer 全做了双主题，直接 [抄我代码](https://github.com/lllxxxxxlll/lllxxxxxlll/blob/main/README.md) 改内容就行。

### 1.4 Push 到 main → 回 `github.com/<你>` 看效果

真的立刻就出来。GitHub 对 profile README 缓存只有几十秒。

---

## 第二站：GitHub Pages 个人网站（第一次接触 GitHub Actions）

做完 profile README，你已经明白"仓库里有个文件 → GitHub 自动显示"这条约定了。现在加一层：**push → build → deploy** 三段式，和公司的 pipeline 一模一样。

### 2.1 建 Pages 仓库

- **Repository name**：`<用户名>.github.io`（比如 `lllxxxxxlll.github.io`）
- Public
- 选一个模板：Hexo（中文社区资料多）、Hugo（快）、VitePress（Vue 生态）都行，随便选一个先跑起来，框架不影响你理解 CI/CD。

### 2.2 第一次看到 Actions 自动跑

你按 Hexo/Hugo 文档初始化完项目，推代码到 main 以后：进仓库 → 顶部 **Actions** tab。你会看到一个 workflow 正在 green 运行 / 已经 ✓ 成功。

点进 run 看一眼，这就是标准 CI/CD：**触发 → 构建 → 产物 → 部署**。对比你公司的 pipeline：

| 公司里的叫法 | GitHub Actions 对应 | Pages 场景里实际在做什么 |
|---|---|---|
| 触发（push / 打 tag / schedule） | `on: push: [main]` 写在 yml 顶部 | 你 push 代码到 main，自动触发 workflow |
| 启动 runner | `runs-on: ubuntu-latest` | GitHub 免费给你开一台临时 Ubuntu 虚拟机（免费额度个人账号 2000 分钟/月，肯定够）。workflow 跑完机器销毁。 |
| 拉代码 | `- uses: actions/checkout@v4` | 把你的仓库 clone 到 runner 里 |
| 准备构建环境 | `- uses: actions/setup-node@v4` | 装 node / 装 Go / 装 Python，版本由 `with: node-version: 20` 指定 |
| build 步骤 | `run: npm ci && npm run build` | 生成静态 HTML/CSS/JS |
| 上传产物 + 部署 | `- uses: actions/deploy-pages@v4` | 把 build 出来的目录传到 GitHub Pages 存储，CDN 分发 |

### 2.3 yml 文件长什么样

全部在 `.github/workflows/pages.yml` 里。给你最简版：

```yaml
name: Deploy Blog
on:
  push:
    branches: [main]         # 只有推 main 才触发
  workflow_dispatch:          # 允许手动点按钮 Run（必加，调试救星）

permissions:
  contents: read
  pages: write
  id-token: write

jobs:
  build-deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: 20
          cache: npm
      - run: npm ci
      - run: npm run build     # 产物在 ./dist 或 ./public

      - uses: actions/configure-pages@v5
      - uses: actions/upload-pages-artifact@v3
        with:
          path: ./public      # 这里填你框架的 build 输出目录
      - uses: actions/deploy-pages@v4
```

### 2.4 新手调 Actions 的正确姿势

1. **加 `workflow_dispatch`**：没它你只能改代码 push 触发调试，每次都污染 commit。加完手动 Run workflow 很方便。
2. **红了点进去看日志**：点失败的 run → 点红色 ❌ 的那个步骤 → 展开 stdout/stderr。**看前 10 行和最后 10 行，答案几乎都在里面。**
3. **`uses:` 的版本写死 `@v4`**：不要写 `@master`，上游改你的 pipeline 会炸。
4. **`permissions:` 权限不够 403**：默认 `GITHUB_TOKEN` 只有 `contents: read`。如果你的 job 要 push 代码回仓库（比如下一节的蛇图生成 SVG 推到 output 分支），显式写 `permissions: contents: write`。

---

## 第三站：Contribution 贪吃蛇（中级 Actions，覆盖真实场景）

这是非常好的教学案例——简单但覆盖了真实 CI/CD 会遇到的所有要素：**定时触发 + 手动触发 + 回写仓库 + 产物存到另一个分支**。

### 3.1 在 profile 仓库里加 `.github/workflows/snake.yml`

```yaml
name: Generate Snake

on:
  schedule:
    - cron: "0 0 * * *"      # 每天 UTC 0 点自动跑（北京时间 08:00）
  workflow_dispatch:          # 允许手动 Run（首次必须手动，因为 cron 等一天太久）

permissions:
  contents: write             # ★ 必须加，否则推 output 分支时 403

jobs:
  snake:
    runs-on: ubuntu-latest
    steps:
      - uses: Platane/snk@v3
        id: snake
        with:
          github_user_name: ${{ github.repository_owner }}
          outputs: |
            dist/github-contribution-grid-snake.svg
            dist/github-contribution-grid-snake-dark.svg
            dist/github-contribution-grid-snake.gif

      - uses: crazy-max/ghaction-github-pages@v4
        with:
          target_branch: output            # 产物存到 output 分支（污染源码历史）
          build_dir: dist
          keep_history: true
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

### 3.2 首次手动触发

仓库 → Actions → 左侧 **Generate Snake** → 右侧 **Run workflow** → 选 `main`。跑完刷新 Actions 列表，状态变 ✓ 后，README 里就能引用：

```
<img src="https://raw.githubusercontent.com/<用户名>/<用户名>/output/github-contribution-grid-snake-dark.svg" />
```

### 3.3 这一步练到的东西

- 两种触发方式并存（cron 自动 + workflow_dispatch 手动）
- 权限最小化思想：只有需要回写时才给 `contents: write`
- 产物存独立分支（`output`）不污染源码 main 的提交历史
- 第三方 Action `Platane/snk` 和 `crazy-max/ghaction-github-pages` 通过文件系统传产物（都在 `dist/` 下读）

---

## 第四站：用 AI (TRAE / Claude Code / Codex) 做开发

用 AI 写代码非常快，但 git 流程不能省。给你一套安全的习惯：

### 4.1 分支策略

**永远不在 main 上直接改。**
- 做 feature：`feature/xxx` 或 `feat/xxx`
- AI 帮你改：习惯上开 `trae/描述` 或 `ai/描述`
- 完成以后 `git checkout main && git merge --ff-only feature/xxx` 快进合并，再 push main

好处：AI 万一改错了直接删分支重来，不污染 main 的历史。

### 4.2 AI 写的代码自己 review

```bash
git diff         # 看具体改了哪些行
git status       # 看哪些文件被改了
```

**这两步 push 前一定要做。** AI 会引入 bug、会删你不想删的东西、会改乱缩进。它只是"比你写得快"，不是"比你写得对"。

### 4.3 鉴权：沙箱/CI 里 token 是分开存的

如果你用 TRAE 或任何沙箱 CI 环境工作，会遇到一个现象：**AI 能读你仓库、能看 issue，但 `git push` 失败报 403**。

原因：**应用层 OAuth token ≠ git credential**。Trae 的浏览器 UI 里你授权过，所以它能调 GitHub API；但沙箱里跑的 `git push` 是一个独立 CLI 进程，需要独立的凭据来源。

解决办法（推荐 gh CLI device flow）：

```bash
gh auth login --hostname github.com --git-protocol https --web
# 会给你一个 URL + 验证码，浏览器打开粘贴验证码授权
# 授权完成后运行：
gh auth setup-git --hostname github.com
```

`gh auth setup-git` 的作用是告诉本地 git 命令"推送时找 gh CLI 来拿 token"，这样之后 push 就不卡了。

> 这条流程在**无显示器无浏览器的无头环境**（实验室服务器、云 ECS、CI runner）里也通用，学会了以后会常常用。

---

## 一张对比表：四条路径各有什么"构建-部署"

| 路径 | 触发条件 | 构建步骤 | 产物 | 部署目标 |
|---|---|---|---|---|
| Profile README | push main | **没有**（零构建） | `README.md` | GitHub 主页（直接渲染） |
| GitHub Pages | push main / 手动 Run | `npm run build` 等 | 静态文件 HTML/CSS/JS | `*.github.io` 域名 |
| 蛇图 Actions | cron 每天 / 手动 Run | `snk` 生成 SVG | SVG/GIF | `output` 分支（被 README 引用） |
| first-contribution PR | 你 push 到自己 fork 的分支 | **没有**（改 md 文本） | 修改后的目录 + Contributors.md | 等 maintainer merge 到上游 main |
| 公司 CI/CD | push 代码 | build 镜像 | Docker Image | 部署到 K8s 泳道 |

心智模型是同一个：**触发 → 构建 → 产物 → 部署/落地**。换什么工具都套得上。

---

## 常见坑 & 速查 Q&A

| 现象 | 真实原因 | 解法 |
|---|---|---|
| Profile README 改完主页没显示 | 仓库是 private | Settings → 改成 public |
| Profile README 还是旧的 | GitHub CDN 缓存 | 等 1-2 分钟，或硬刷新 Cmd+Shift+R |
| snake.yml 跑了但 SVG 还是找不到 | `permissions: contents: write` 没加，push output 分支 403 | 在 yml 顶部加权限，重跑 Action |
| snake.yml 第一次跑 README 里还是空 | 没手动触发 workflow_dispatch | Actions → Generate Snake → Run workflow 手动跑一次 |
| GitHub Pages 打开 404 | 仓库名没带 `.github.io` 后缀，或 Source 选错分支 | Settings → Pages → Source 里选正确的 deploy 来源 |
| Pages 样式全乱了 | hexo/hugo/vitepress 的 baseUrl / path 没配对 | config 里 url 改成 `https://<用户名>.github.io`，如有子路径再配 `base` |
| `git push` 在沙箱/CI 报 403 | 没有 credential helper | `gh auth login --web` → 授权 → `gh auth setup-git` |
| Action 全红不会调 | 不看日志瞎改 | 点失败的 step，展开 stdout 看最后 20 行；看不懂复制去搜，90% 是别人踩过的坑 |
| `uses: xxx@master` 昨天好今天炸 | 上游改了版本 | 改成 `@v4` 这类固定 tag |
| 徽章/图片不显示 | 第三方服务（vercel/worker）挂了 | shields.io 是 GitHub 官方 CDN，优先用；图片自己存到仓库 assets 里走 `raw.githubusercontent.com` 最稳 |

---

## 接下来你可以做什么

1. **现在就动手建自己的 profile README 同名仓库**。先写最简单版本（Banner + 自我介绍 + 3 个徽章），push 看效果。
2. **搞 `xxx.github.io` 搭博客**。遇到 Actions 红了就按 Q&A 里的方法读日志。
3. **回到这个 first-contributions 仓库**：fork → clone → 建自己的 `HelloFrom<你昵称>/README.md` → 改 Contributors.md → push 分支 → 开 PR，把你刚走过的流程写进去。

---

> Talk is cheap. Show me the code. **Then go for it.**
> —— 不用等"准备好"，先把 commit 推上去。