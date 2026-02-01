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