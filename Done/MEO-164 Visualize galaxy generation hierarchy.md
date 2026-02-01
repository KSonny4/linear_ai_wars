# [MEO-164] Visualize galaxy generation hierarchy

**Status:** Done

---

## Goal

Create ASCII visualizations of galaxy structure at each hierarchical level, displayed in the web UI. This is MVP debugging/verification tooling.

## Hierarchy to Visualize

```
Galaxy (1000x1000 grid)
  └── Sectors (10x10 = 100 sectors, labeled A0-J9)
        └── Coordinates (100x100 per sector)
              └── Planets (with terrain + owner)
                    └── Modules (with levels)
                          └── Ships (stationed fleets)
```

## Comments

### Petr Kubelka (2026-01-31T20:56:29.409Z)

## Implementation Progress

### Completed
- **Level 1: Galaxy Overview** (`/galaxy/[galaxyId]`)
  - 10x10 sector grid with density visualization
  - Core sectors visually distinguished (S44, S45, S54, S55)
  - Click to navigate to sector detail
  - Uses `AsciiGalaxyOverview` component

- **Level 2: Sector Detail** (`/galaxy/[galaxyId]/sector/[sectorId]`)
  - Planet positions within sector
  - Keyboard navigation (WASD/arrows) for panning
  - Click planet to view details
  - Shows neighboring sectors
  - Uses `AsciiSectorMap` component

- **Level 3: Planet Detail** (`/galaxy/[galaxyId]/planet/[x]/[y]`)
  - Modules with level bars
  - Resources with ASCII progress bars and terrain bonuses
  - Stationed ships
  - Build queue with ETA
  - Ship queue with ETA
  - Incoming/outgoing fleets
  - Loyalty display
  - Uses `AsciiPlanet` component (fixed missing dependencies)

### Files Created/Modified
- `components/game/AsciiPlanet.tsx` - Fixed missing imports, simplified to use existing utilities

### Navigation Flow
```
Galaxy Overview → Sector Detail → Planet Detail
      ↑                ↑              ↑
   /galaxy/X    /galaxy/X/sector/Y  /galaxy/X/planet/A/B
```

### Note on Sector Naming
Web UI uses `S44` format while backend uses `A0-J9` format. This works independently but could be unified in a future task.

---
