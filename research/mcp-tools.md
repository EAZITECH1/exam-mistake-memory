# Walrus Memory MCP tool surface

Verified against https://docs.wal.app/walrus-memory/mcp/overview on July 12, 2026.

| Tool | What it does | How this prompt uses it |
| --- | --- | --- |
| `memwal_remember` | Save a durable fact | Fires on every wrong answer with a structured entry (topic, misconception, correct fact, severity, miss count) |
| `memwal_remember_bulk` | Save several facts in one call | 3+ mistakes in a single quiz round batch into one call |
| `memwal_recall` | Semantic search across memories | Session-start Weakness Briefing; dedup check before every write |
| `memwal_analyze` | Extract and save multiple facts from a passage | Pasted tutor feedback and marked scripts, each error becomes its own memory |
| `memwal_restore` | Rebuild search index from Walrus blobs | Fallback when recall returns empty despite prior sessions |
| `memwal_health` | Connectivity check | Setup verification |
| `memwal_login` / `memwal_logout` | Credential management via browser wallet | One-time sign-in; credentials land in ~/.memwal/credentials.json (mode 0600) |

## Notes from setup

- The npm package (`@mysten-incubation/memwal-mcp`) runs locally and bridges tool calls to the hosted relayer, which handles embeddings, Seal encryption, and Walrus storage.
- Two install paths on Claude Code: plain MCP server, or the plugin which adds lifecycle hooks that reinforce automatic save/recall. I used the plugin.
- Recall is semantic, not a namespace dump. The prompt words its recall triggers as natural-language queries scoped to a subject tag for that reason.
- The delegate private key never appears in the prompt, the repo, or the demo; login handles it.
