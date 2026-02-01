# [MEO-138] Auto-generate AGENTS.md after every engine compile

**Status:** Done

---

Automatically regenerate AGENTS.md documentation specifically for AI agent consumption on every engine build.

## Comments

### Petr Kubelka (2026-01-31T18:16:11.481Z)

## Resolution

### Completed Work

#### 1. Enhanced OpenAPI Spec (`packages/game-engine/api/openapi.yaml`)
Completely rewrote the OpenAPI specification with comprehensive, AI-friendly documentation:

- **Rich endpoint descriptions** explaining WHY and WHEN to use each endpoint
- **Complete game mechanics** embedded in descriptions (combat formulas, resource calculation, strategy tips)
- **Examples** for all request/response bodies with realistic data
- **Tables** for ships, modules, terrain types, error codes
- **Strategic context** so AI agents understand not just the API, but how to play the game

#### 2. Player Guide (`docs/AGENTS_PLAYER.md`)
Created comprehensive game guide for AI agents containing:

- Game overview and core loop explanation
- Full API reference with all 20+ endpoints
- Quick reference tables (13 modules, 10 ships, 4 terrain types, 11 error codes)
- Combat mechanics (luck factor, shield bonuses, loot calculation)
- Strategy guide (early game, mid game, combat tips)
- Example game session with curl commands
- Recommended polling strategy (6-10 req/min)

#### 3. Generator Script (`scripts/generate-agents-doc.go`)
Go script that parses OpenAPI YAML and generates markdown documentation.

#### 4. Makefile Targets
- `make docs` - Regenerate AGENTS_PLAYER.md from OpenAPI spec
- `make validate-api` - Validate OpenAPI spec syntax

### Key Design Decisions

1. **OpenAPI as single source of truth** - All game mechanics documented in the API spec, making it self-documenting
2. **Programmatic export** - Spec structured for tools to parse and generate various formats
3. **AI-agent focused** - Descriptions include strategic advice and decision context

### Files Changed
- `packages/game-engine/api/openapi.yaml` - Complete rewrite (~1250 lines)
- `docs/AGENTS_PLAYER.md` - New file (~900 lines)
- `scripts/generate-agents-doc.go` - New file
- `Makefile` - Added docs and validate-api targets

---
