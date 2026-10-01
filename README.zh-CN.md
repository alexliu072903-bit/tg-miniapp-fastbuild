# tg-miniapp-fastbuild

**[English](README.md) | 中文**

一份 Telegram Mini App 的部署指南，写成了 skill。照着一步步做，就能让 Mini App 经过 BotFather、GitHub 和 Railway 部署到生产环境。

支持 Claude Code、Codex、Cursor，以及任何能加载 `SKILL.md` 的 Agent。开发者也可以把它当作普通指南来读。

## 它覆盖什么

- **BotFather**：创建和配置 Bot。
- **GitHub**：仓库搭建与 CI/CD。
- **Railway**：把 PostgreSQL、后端、前端作为独立服务分别部署。
- **Webhook**：注册，并检查它是否生效。
- **双语**：双语 Bot 文案与语言切换的结构。

仓库里只有一份 `SKILL.md` 和一个 `example.js`。

## 适合谁用

- 第一次做 Telegram Mini App 的开发者。
- 被要求部署 Telegram Mini App 的 AI Agent。
- 已经在 Railway 部署上踩过坑的人。

## 安装

把仓库克隆到你的 Agent 的 skills 目录。

Claude Code：

```bash
git clone https://github.com/alexliu072903-bit/tg-miniapp-fastbuild ~/.claude/skills/tg-miniapp-fastbuild
```

Codex：

```bash
git clone https://github.com/alexliu072903-bit/tg-miniapp-fastbuild ~/.codex/skills/tg-miniapp-fastbuild
```

Cursor，或者其他没有 skills 目录的 Agent，让它去读 `SKILL.md` 即可。

## 如何使用

配合 Agent：

```text
读取 SKILL.md，按照其中的流程，用 Railway 和 GitHub 部署一个 Telegram Mini App。
按顺序执行，并参考避坑表规避常见错误。
```

自己用的话，动手写代码之前，从头到尾读完 `SKILL.md`。光是避坑那一节，就能帮你省下几个小时。

## 技术栈

| 层级 | 技术 |
| --- | --- |
| 前端 | React + Vite |
| 后端 | Node.js + Express + Telegraf |
| 数据库 | PostgreSQL |
| 部署平台 | Railway |
| CI/CD | GitHub 到 Railway，每次 push 到 `main` 自动部署 |

## 容易让部署失败的五件事

1. **不要在 Railway 里用 “Deploy from GitHub”。** Railway 会误判仓库结构。从 Empty Project 开始，自己添加服务。
2. **不要手动设置 `PORT`。** Railway 会自动注入，手动设置会让构建失败。
3. **在 `railway.json` 里用 `npm install`，不要用 `npm ci`。** `npm ci` 会在 Railway 的构建环境里遇到缓存冲突。
4. **`WEBHOOK_URL` 必须带 `https://`。** 只写域名，Webhook 注册不会成功。
5. **分享链接必须是 `t.me/BOT_NAME/app` 这种格式。** 其他格式会把人带到 telegram.org，而不是打开 Mini App。

## 来源

这份指南提炼自一个已上线的 Telegram Mini App（一个俄语和英语的人格测试，部署在 Railway 上），它在一次对话里从零做到上线。`SKILL.md` 里的每一条避坑项，都是在那里遇到并解决的。

## License

MIT
