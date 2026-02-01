# [MEO-172] Restrict planet detail view to authenticated owner only

**Status:** Done

---

## Problem

The GET /planets/{planetId} endpoint returns full planet details (resources, ships, modules) to ANY authenticated agent, not just the owner.

## Fix Required

1. Add ownership verification before returning full planet details
2. Public endpoints should return limited public info

## Comments

### Petr Kubelka (2026-01-31T22:36:05.456Z)

## Updated Implementation (per user feedback)

The API should be accessible to view other planets (for UI map clicks), but with different access levels:

### Access Control Model
1. **Owner** → Full details (resources, ships, modules, queues)
2. **Other agents** → Public info only (ID, name, coords, sector, terrain, points)
3. **Admin** → Full access to everything

### Additional Changes

**`internal/repository/agents.go`:**
- Added `IsAdmin` field to Agent struct
- Updated all SELECT queries to include `is_admin` column

**`internal/middleware/auth.go`:**
- Added `IsAdmin(ctx)` helper function

**`internal/api/planets.go` - Get handler updated:**
- Admins get full access via `GetPlanet`
- Owners get full access via `GetPlanetOwned`
- Others get public info via `GetPublicPlanet`

### Database Migrations
- Created `migrations/004_admin_role.sql` 
- Created `infrastructure/docker/init-scripts/004_admin_role.sql`

```sql
ALTER TABLE agents ADD COLUMN IF NOT EXISTS is_admin BOOLEAN NOT NULL DEFAULT FALSE;
CREATE INDEX IF NOT EXISTS idx_agents_is_admin ON agents(is_admin) WHERE is_admin = TRUE;
```

### To grant admin access
```sql
UPDATE agents SET is_admin = TRUE WHERE name = 'admin_agent_name';
```

---

### Petr Kubelka (2026-01-31T21:39:29.542Z)

## Fix Implemented

### Changes Made

**`internal/service/planet.go`:**
- Added `ErrNotPlanetOwner` error for access control
- Added `PublicPlanetResponse` struct (no sensitive data: only ID, name, coords, sector, terrain, abandoned, points)
- Added `GetPlanetOwned(ctx, galaxyID, planetID, agentID)` - returns full details only if agent owns the planet
- Added `GetPublicPlanet(ctx, galaxyID, planetID)` - returns only public info
- Added `GetPublicPlanetByCoords(ctx, galaxyID, x, y)` - returns only public info by coordinates
- Added `VerifyOwnership(ctx, galaxyID, planetID, agentID)` - utility for checking ownership
- Updated `StartBuild` to require `agentID` and verify ownership before building
- Updated `StartBuildShips` to require `agentID` and verify ownership before building ships

**`internal/api/planets.go`:**
- Updated `Get` handler to use `GetPlanetOwned` (returns 403 if not owner)
- Updated `Build` handler to pass `agentID` to service (returns 403 if not owner)
- Updated `BuildShips` handler to pass `agentID` to service (returns 403 if not owner)
- Updated `GetPublicByCoords` to use `GetPublicPlanetByCoords` (returns only public info)

### Security Impact
- **Before**: Any authenticated agent could see full details (resources, ships, modules) of ANY planet in their galaxy
- **After**: Only planet owners can see sensitive data; public endpoints return limited public info

### Testing
- All existing tests pass
- Build compiles successfully

---
