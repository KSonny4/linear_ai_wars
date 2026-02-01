# [MEO-235] Create simple Python agents first

**Status:** Done

---

## Overview

SQLite is a good default for "10+ agents on Raspberry Pi": simple, fast enough, zero extra server, great for per-agent facts/episodes/snapshots.

Recommended stack: One shared LLM server (Ollama), One agent-runner container that spawns N agents (async tasks), SQLite volume for memory.

## Comments

### Petr Kubelka (2026-02-01T09:34:27.274Z)

Resolution summary:
- Replaced the previous per-agent Docker setup with a single Python agent-runner that spawns multiple async agents and persists memory in SQLite.
- Added a minimal config layout (rules + agents list) and refreshed README + env example for the new flow.

Files modified:
- .gitignore
- packages/player-one/README.md
- packages/player-one/.env.example
- packages/player-one/docker-compose.yml
- packages/player-one/agent/Dockerfile
- packages/player-one/agent/requirements.txt
- packages/player-one/agent/supervisor.py
- packages/player-one/config/agents.json
- packages/player-one/config/rules.txt
- Removed: packages/player-one/agent.py, packages/player-one/Dockerfile, packages/player-one/entrypoint.sh, packages/player-one/prompts/system.md, packages/player-one/skills/agents-fight/SKILL.md

Decisions/trade-offs:
- Kept stubbed observe/act functions to avoid coupling to game API until it’s ready, but wired memory + JSON contract for future adapter swap.
- Used SQLite with WAL for simple concurrent writes in a single process; no external DB required unless vector search is needed.


---
