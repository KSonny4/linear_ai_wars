# [MEO-235] Create simple Python agents first

**Status:** Done

---

## Overview

SQLite is a good default for "10+ agents on Raspberry Pi": simple, fast enough, zero extra server, great for per-agent facts/episodes/snapshots.

Recommended stack: One shared LLM server (Ollama), One agent-runner container that spawns N agents (async tasks), SQLite volume for memory.