// tg-miniapp-fastbuild — example code
// Copy and adapt these snippets for your project

// ─────────────────────────────────────────────
// 1. Bot setup with Telegraf
// ─────────────────────────────────────────────

const { Telegraf } = require('telegraf')

const bot = new Telegraf(process.env.BOT_TOKEN)

// Register webhook on startup
async function startBot() {
  await bot.telegram.setWebhook(`${process.env.WEBHOOK_URL}/bot/webhook`)
  console.log(`[bot] Webhook registered: ${process.env.WEBHOOK_URL}/bot/webhook`)
}

// ─────────────────────────────────────────────
// 2. /start command — bilingual
// ─────────────────────────────────────────────

bot.command('start', async (ctx) => {
  const lang = ctx.from?.language_code?.startsWith('ru') ? 'ru' : 'en'

  const copy = {
    en: {
      message: "Your welcome message here.",
      button: "🚀 Open App",
    },
    ru: {
      message: "Ваше приветственное сообщение здесь.",
      button: "🚀 Открыть",
    },
  }

  await ctx.reply(copy[lang].message, {
    reply_markup: {
      inline_keyboard: [[
        {
          text: copy[lang].button,
          web_app: { url: process.env.MINI_APP_URL }
        }
      ]]
    }
  })
})

// ─────────────────────────────────────────────
// 3. Express webhook endpoint
// ─────────────────────────────────────────────

const express = require('express')
const app = express()

app.use(express.json())

app.post('/bot/webhook', (req, res) => {
  bot.handleUpdate(req.body, res)
})

app.get('/health', (req, res) => {
  res.json({ status: 'ok' })
})

const PORT = process.env.PORT || 3000
app.listen(PORT, async () => {
  console.log(`[server] Running on port ${PORT}`)
  await startBot()
})

// ─────────────────────────────────────────────
// 4. railway.json — frontend build config
// ─────────────────────────────────────────────

// Save this as frontend/railway.json
// IMPORTANT: use npm install, NOT npm ci
// npm ci causes EBUSY cache conflict in Railway's build environment

/*
{
  "$schema": "https://railway.app/railway.schema.json",
  "build": {
    "builder": "NIXPACKS",
    "buildCommand": "npm install && npm run build"
  },
  "deploy": {
    "startCommand": "npx serve dist -p ${PORT:-3000} -s",
    "restartPolicyType": "ON_FAILURE",
    "restartPolicyMaxRetries": 10
  }
}
*/

// ─────────────────────────────────────────────
// 5. React — bilingual state architecture
// ─────────────────────────────────────────────

/*
// App.jsx
import { useState } from 'react'
import { questionsEn } from './data/questions-en'
import { questionsRu } from './data/questions-ru'
import { typesEn, scoringMatrixEn, specialRulesEn } from './data/types-en'
import { typesRu, scoringMatrixRu, specialRulesRu } from './data/types-ru'

export default function App() {
  const [lang, setLang] = useState(null)       // 'en' | 'ru'
  const [page, setPage] = useState('language') // initial page

  const langData = lang === 'ru'
    ? { questions: questionsRu, scoringMatrix: scoringMatrixRu, types: typesRu, specialRules: specialRulesRu }
    : { questions: questionsEn, scoringMatrix: scoringMatrixEn, types: typesEn, specialRules: specialRulesEn }

  const handleSelectLang = (selectedLang) => {
    setLang(selectedLang)
    setPage('welcome')
  }

  const handleRestart = () => {
    setPage('language') // return to language selection, clear lang
    setLang(null)
  }

  if (page === 'language') return <LanguagePage onSelect={handleSelectLang} />
  if (page === 'welcome')  return <WelcomePage lang={lang} onStart={() => setPage('quiz')} />
  if (page === 'quiz')     return <QuizPage {...langData} onFinish={(result) => { setResult(result); setPage('result') }} />
  if (page === 'result')   return <ResultPage result={result} lang={lang} onRestart={handleRestart} />
}
*/

// ─────────────────────────────────────────────
// 6. Scoring algorithm
// ─────────────────────────────────────────────

function calculateResult(answers, scoringMatrix, types, specialRules) {
  const scores = {}
  for (const code of Object.keys(types)) scores[code] = 0

  for (const [qId, option] of Object.entries(answers)) {
    const entry = scoringMatrix[qId]?.[option]
    if (!entry) continue
    scores[entry.primary] = (scores[entry.primary] || 0) + 2
    scores[entry.secondary] = (scores[entry.secondary] || 0) + 1
  }

  const { superTypes = [], superThreshold = 6, minScore = {} } = specialRules || {}

  // Super types win immediately if threshold reached
  const superWinner = superTypes
    .filter(c => (scores[c] || 0) >= superThreshold)
    .sort((a, b) => scores[b] - scores[a])[0]
  if (superWinner) return types[superWinner]

  // Sort by score descending
  const sorted = Object.entries(scores).sort(([, a], [, b]) => b - a)
  let winner = sorted[0][0]

  // Tiebreaker: use last question's primary type
  if (sorted[0][1] === sorted[1]?.[1]) {
    const lastQId = Object.keys(answers).at(-1)
    const tiebreaker = scoringMatrix[lastQId]?.[answers[lastQId]]?.primary
    if (tiebreaker) winner = tiebreaker
  }

  // Minimum score threshold check
  const min = minScore[winner]
  if (min && scores[winner] < min) winner = sorted[1]?.[0] ?? winner

  return types[winner]
}

module.exports = { calculateResult }

// ─────────────────────────────────────────────
// 7. Data structure templates
// ─────────────────────────────────────────────

/*
// questions-en.js
export const questionsEn = [
  {
    id: 'Q1',
    text: 'Question text here',
    options: {
      A: 'Option A text',   // no leading/trailing quotes
      B: 'Option B text',
      C: 'Option C text',
      D: 'Option D text',
    }
  },
]

// types-en.js
export const typesEn = {
  TYPE_CODE: {
    code: 'TYPE_CODE',
    name: 'Type Display Name',
    description: 'Type description text...',
    staticCounts: 5412,
  },
}

export const scoringMatrixEn = {
  Q1: {
    A: { primary: 'TYPE_A', secondary: 'TYPE_B' },
    B: { primary: 'TYPE_C', secondary: 'TYPE_D' },
    C: { primary: 'TYPE_E', secondary: 'TYPE_F' },
    D: { primary: 'TYPE_G', secondary: 'TYPE_H' },
  },
}

export const specialRulesEn = {
  minScore: { 'TYPE_CODE': 8 },  // type needs min 8pts to win
  superTypes: [],                 // types that win at threshold regardless of others
  superThreshold: 6,
}
*/

// ─────────────────────────────────────────────
// 8. Share link — correct format
// ─────────────────────────────────────────────

/*
// Always use this format in SharePanel.jsx
// Other formats will redirect to telegram.org instead of opening the Mini App

const BOT_USERNAME = import.meta.env.VITE_BOT_USERNAME
const shareUrl = `https://t.me/${BOT_USERNAME}/app`

const shareText = lang === 'ru'
  ? `Я — ${typeName}! Узнай свой тип 👇 ${shareUrl}`
  : `I'm ${typeName}! Find your type 👇 ${shareUrl}`
*/
