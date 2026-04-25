# tg-miniapp-fastbuild

**Deploy a Telegram Mini App to production in under 2 hours.**

A battle-tested skill for building Telegram Mini Apps with Railway, GitHub, and BotFather — including every gotcha from real deployment experience.

---

## What's Inside

This repo contains a single `SKILL.md` — a structured deployment guide designed to be used directly by AI coding agents (Claude, Cursor, etc.) or followed step-by-step by developers.

It covers the full stack:

- 🤖 **BotFather** — creating and configuring your Telegram Bot
- 🐙 **GitHub** — repo setup and CI/CD
- 🚂 **Railway** — deploying PostgreSQL + backend + frontend as separate services
- ⚡ **Webhook** — registering and verifying Bot webhook
- 🌍 **Multi-language** — bilingual Bot copy and language switching architecture

---

## Who This Is For

- Developers building their first Telegram Mini App
- AI agents tasked with deploying a Telegram Mini App
- Anyone who's been burned by Railway deployment quirks before

---

## How to Use

### With an AI agent (Claude, Cursor, etc.)

```
Read SKILL.md and use it to guide the deployment of a Telegram Mini App
with Railway + GitHub. Follow the flow exactly and use the gotchas table
to avoid common errors.
```

### As a developer

Read `SKILL.md` top to bottom before touching any code. The **Gotchas** section alone will save you hours.

---

## Stack

| Layer | Technology |
|-------|-----------|
| Frontend | React + Vite |
| Backend | Node.js + Express + Telegraf |
| Database | PostgreSQL |
| Hosting | Railway |
| CI/CD | GitHub → Railway (auto-deploy on push to main) |

---

## Key Insights

A few things this skill gets right that most tutorials miss:

**1. Don't use `Deploy from GitHub` in Railway**
Railway misidentifies the repo structure. Always start with `Empty Project` and add services manually.

**2. Never set PORT manually**
Railway injects PORT automatically. Setting it yourself breaks the build.

**3. Use `npm install` not `npm ci` in railway.json**
`npm ci` triggers a cache conflict bug in Railway's build environment. Always use `npm install`.

**4. WEBHOOK_URL must include `https://`**
Just the domain is not enough. The full URL with protocol is required for webhook registration.

**5. Share links must be `t.me/BOT_NAME/app`**
Any other format redirects to telegram.org instead of opening the Mini App.

---

## Real-World Proof

This skill was extracted from a production Telegram Mini App (personality test, bilingual RU/EN, deployed on Railway) that went from zero to live in a single session. All gotchas in `SKILL.md` were encountered and solved during that build.

---

## License

MIT — use it, fork it, build on it.

---

# tg-miniapp-fastbuild（中文版）

**两小时内将 Telegram Mini App 部署到生产环境。**

一份经过实战验证的部署指南，涵盖 Railway、GitHub 和 BotFather 的完整流程——包括所有真实踩过的坑。

---

## 里面有什么

这个 repo 包含一份 `SKILL.md`，可以直接被 AI 编程助手（Claude、Cursor 等）调用，也可以作为开发者的手把手部署指南。

覆盖完整技术栈：

- 🤖 **BotFather** — 创建和配置 Telegram Bot
- 🐙 **GitHub** — 仓库搭建与 CI/CD
- 🚂 **Railway** — 将 PostgreSQL、后端、前端作为独立服务分别部署
- ⚡ **Webhook** — 注册和验证 Bot webhook
- 🌍 **多语言** — 双语 Bot 文案与语言切换架构

---

## 适合谁用

- 第一次做 Telegram Mini App 的开发者
- 被交代了"部署一个 Telegram Mini App"任务的 AI agent
- 被 Railway 部署踩过坑、不想再踩第二次的人

---

## 如何使用

### 配合 AI 编程助手（Claude、Cursor 等）

```
读取 SKILL.md，按照其中的流程部署一个基于 Railway + GitHub 的
Telegram Mini App。严格按照流程执行，并参考避坑表规避常见错误。
```

### 作为开发者自用

从头到尾读完 `SKILL.md` 再动手写代码。光是**避坑清单**这一节就能帮你省掉好几个小时。

---

## 技术栈

| 层级 | 技术 |
|------|------|
| 前端 | React + Vite |
| 后端 | Node.js + Express + Telegraf |
| 数据库 | PostgreSQL |
| 部署平台 | Railway |
| CI/CD | GitHub → Railway（push 到 main 自动部署）|

---

## 核心经验

这份指南解决了大多数教程都没提到的问题：

**1. Railway 不要用 `Deploy from GitHub`**
Railway 会误判仓库结构。始终选 `Empty Project`，然后手动添加服务。

**2. 不要手动设置 PORT**
Railway 会自动注入 PORT。手动设置会直接导致构建失败。

**3. `railway.json` 里用 `npm install` 而不是 `npm ci`**
`npm ci` 会触发 Railway 构建环境的缓存冲突 bug，改成 `npm install` 就解决了。

**4. `WEBHOOK_URL` 必须包含 `https://`**
只填域名不够，必须是带协议头的完整 URL，否则 webhook 注册会静默失败。

**5. 分享链接格式必须是 `t.me/BOT_NAME/app`**
其他格式会跳转到 telegram.org，而不是打开 Mini App。

---

## 实战背书

这份指南提炼自一个真实上线的 Telegram Mini App——双语（俄语/英语）人格测试产品，部署在 Railway 上，整个部署过程在单次 session 内完成。`SKILL.md` 里的所有避坑内容，都是在这次构建中实际遇到并解决的。

---

## 许可证

MIT — 随意使用、fork、二次开发。
