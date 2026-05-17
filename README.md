**[English](README.md) | [中文](README.zh.md)**

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

MIT
