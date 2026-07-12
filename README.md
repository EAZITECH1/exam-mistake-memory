# Exam Mistake Memory — a study agent that never lets you fail the same question twice

> **Walrus Memory Prompt Jam** submission. System prompt, copy-pasteable into any MCP client.
> Built and proven on real Pharm.D coursework at Lagos State University College Of Medicine. Works for any exam.

---

## Problem

**Who:** anyone studying for a high-stakes exam with an AI assistant. Students, USMLE/bar/CFA candidates, certification takers.

**Pain:** every study session starts from zero. The agent re-explains what you already know and has no idea what you got wrong yesterday, which is the only thing that decides whether you pass. Your mistakes, the highest-value data in your entire prep, evaporate when the session closes. For me that's daily; I'm a pharmacy student with a CGPA to rescue and past questions to grind.

**Solution:** paste one system prompt. The agent stores every mistake to Walrus Memory the moment it happens, recalls your weaknesses before you ask, and drills you on exactly what you keep failing. Session two opens by attacking what session one exposed.

---

## Quick start

1. Install the Walrus Memory MCP server (or the Claude Code plugin for automatic memory hooks):

```json
{
  "mcp": {
    "memwal": {
      "type": "local",
      "command": ["npx", "-y", "@mysten-incubation/memwal-mcp"],
      "enabled": true
    }
  }
}
```

Claude Code plugin route: https://docs.wal.app/walrus-memory/mcp/claude-code

2. Copy the full prompt from [`prompts/exam-mistake-memory.md`](prompts/exam-mistake-memory.md) into your `CLAUDE.md` or agent system prompt.

3. Fill the config block at the top: your exam, your subjects, one short namespace tag per subject.

4. Run `memwal_login`, approve in your browser wallet.

5. Study. Answer practice questions. Get things wrong. That's the point; wrong answers become permanent memory.

---

## How it works

| Namespace | Purpose |
| --- | --- |
| `{subject-tag}` (one per subject) | Mistakes: subtopic, misconception, correct fact, severity, miss count |
| `exam-intel` | Exam-pattern observations: recurring question styles, repeated past questions |

**Write rules the agent follows without being asked:**

- Wrong or partially wrong answer → immediate `memwal_remember` with a structured entry
- 3+ mistakes in one quiz round → single `memwal_remember_bulk` call
- Pasted tutor feedback or marked scripts → `memwal_analyze`, each error becomes its own recallable memory
- First-attempt correct answers are never stored. Noise rots recall quality.
- Recall-before-write dedup: existing entry gets its miss counter bumped instead of a duplicate blob

**Recall rules:**

- Session start → semantic recall against the subject namespace, then a **Weakness Briefing**: top 5 weak topics ranked by misses × severity, recency-weighted
- Quizzing follows a 60/30/10 split: weak topics / new material / spot checks on mastered topics
- Mastery = 3 correct across 2+ separate sessions. One failed spot check resets it.
- Empty recall despite prior sessions → `memwal_restore` rebuilds the index from Walrus blobs
- The agent never asks for anything already in memory

The visible result: the agent's behaviour changes between sessions, not within one. It opens session two already knowing your weak spots, calls out repeat mistakes with their history, and stops re-teaching what you've mastered.

---

## Proof

| Item | Value |
| --- | --- |
| Agent ID | `65018e137d87ee19c3451e34c642740fa8a183979da02ba72fd47fdf570d2f9e` |
| Blobs written on Mainnet | `2` |
| Dedicated Sessions wallet | `0x9efad55f790d1f38647c565aa564cb381e145d3e7b635bb0538fcc0429f55a34` |
| Demo video (on Walrus) | pending |

Demo shows two real study sessions on my pharmacology past questions: mistakes written in session one, the Weakness Briefing recalling them cold in a fresh session two.

---

## Submission checklist

| Item | Status |
| --- | --- |
| Copy-pasteable prompt | ✅ [`prompts/exam-mistake-memory.md`](prompts/exam-mistake-memory.md) |
| Problem statement | ✅ above |
| ≥10 Mainnet blobs + agent ID | ✅ table above |
| Demo video <3 min on Walrus | ✅ link above |
| DeepSurge submission | ✅ |
| Walform submission | ✅ |
| Feedback form + GitHub issues | ✅ |
| Discord joined | ✅ |
| X post with #Walrus | pending |

---

## Stack

- **Client:** Claude Code (works in any MCP client: Cursor, Codex, Claude Desktop, OpenCode)
- **MCP:** `@mysten-incubation/memwal-mcp`
- **Storage:** Walrus Mainnet via the hosted relayer
- **Author:** Israel — EAZITECH ([@eazitechh](https://x.com/eazitechh)) · eazitech.wal.app
