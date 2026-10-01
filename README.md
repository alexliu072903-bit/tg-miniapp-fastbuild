# tg-miniapp-fastbuild

**English | [中文](README.zh-CN.md)**

A deployment guide for Telegram Mini Apps, written as a skill. Follow it step by step to take a Mini App through BotFather, GitHub, and Railway to production.

It works with Claude Code, Codex, Cursor, and any agent that loads a `SKILL.md`. A developer can also read it as a plain guide.

## What it covers

- **BotFather**: creating and configuring the bot.
- **GitHub**: repository setup and CI/CD.
- **Railway**: PostgreSQL, backend, and frontend as separate services.
- **Webhook**: registering it and checking that it works.
- **Two languages**: bilingual bot copy and the language-switching structure.

The repository holds one `SKILL.md` and an `example.js`.

## Who it is for

- Developers building their first Telegram Mini App.
- AI agents asked to deploy a Telegram Mini App.
- Anyone who has already lost time to Railway deployment quirks.

## Install

Clone the repository into your agent's skills directory.

For Claude Code:

```bash
git clone https://github.com/alexliu072903-bit/tg-miniapp-fastbuild ~/.claude/skills/tg-miniapp-fastbuild
```

For Codex:

```bash
git clone https://github.com/alexliu072903-bit/tg-miniapp-fastbuild ~/.codex/skills/tg-miniapp-fastbuild
```

For Cursor, or any agent without a skills directory, tell the agent to read `SKILL.md`.

## How to use

With an agent:

```text
Read SKILL.md and use it to deploy a Telegram Mini App with Railway and GitHub.
Follow the steps in order and check the gotchas table to avoid common errors.
```

On your own, read `SKILL.md` from top to bottom before you write any code. The gotchas section alone can save you hours.

## Stack

| Layer | Technology |
| --- | --- |
| Frontend | React + Vite |
| Backend | Node.js + Express + Telegraf |
| Database | PostgreSQL |
| Hosting | Railway |
| CI/CD | GitHub to Railway, deploying on every push to `main` |

## Five things that break a deployment

1. **Do not use "Deploy from GitHub" in Railway.** Railway misreads the repository structure. Start from an Empty Project and add the services yourself.
2. **Never set `PORT` by hand.** Railway injects it, and setting it breaks the build.
3. **Use `npm install`, not `npm ci`, in `railway.json`.** `npm ci` runs into a cache conflict in Railway's build environment.
4. **`WEBHOOK_URL` must include `https://`.** The bare domain is not enough for webhook registration.
5. **Share links must look like `t.me/BOT_NAME/app`.** Any other format sends people to telegram.org instead of opening the Mini App.

## Where it comes from

The guide was extracted from a production Telegram Mini App (a personality test in Russian and English, deployed on Railway) that went from zero to live in one session. Every gotcha in `SKILL.md` was hit and solved there.

## License

MIT
