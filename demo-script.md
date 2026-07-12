# Demo video script (target 2:30, hard cap 3:00)

Record Claude Code full-screen. Keep MemWal playground + Sui explorer in tabs. Blur ~/.memwal/credentials.json or any key if visible.

## 0:00–0:20 — Problem
"I'm a pharmacy student. Every AI study session starts from zero. It re-explains what I already know and forgets what I got wrong yesterday, which is the only thing that matters before an exam. So I wrote a system prompt that gives my study agent permanent memory on Walrus. My mistakes become its database."

## 0:20–0:35 — The prompt (scroll prompts/exam-mistake-memory.md)
"The rules are strict. Write on every wrong answer: the misconception, the correct fact, a severity score. Never store what I got right. Recall before every write so it bumps a miss counter instead of duplicating blobs. Works for any exam."

## 0:35–1:20 — Session 1 (mistakes)
Show: wrong answer → correction → memwal_remember firing.
"There. Wrong answer, and it wrote the memory without me asking. That's a blob on Walrus Mainnet, right now."
Show 2–3 more writes, then session-end summary with blob count.
"End of session: [N] mistakes stored. Now I close everything."

## 1:20–2:05 — Session 2 (payoff, fresh instance)
"New session, completely fresh context. Watch: prep me for pharmacology."
Show: memwal_recall firing → Weakness Briefing with session 1 misses.
"It knows. It quizzes my worst topic first, and when I slip on the same thing again..."
Show: repeat mistake → "You've missed this N times before" response.
"...it calls me out with the history. Behaviour change across sessions, not within one."

## 2:05–2:30 — Proof
Switch tabs: playground blob count → Sui explorer transactions on the dedicated wallet.
"Here's my agent ID, [N] blobs on Mainnet. Full prompt in the repo, config block at the top for your own exam. Built during the Walrus Prompt Jam, July 2026."
