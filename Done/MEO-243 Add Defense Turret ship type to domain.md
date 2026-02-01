# [MEO-243] Add Defense Turret ship type to domain

**Status:** Done

---

## Task

Add a new stationary defense ship type that can only defend, never attack.

## COMPLETED ✅

Added `ShipDefenseTurret` constant in `internal/domain/ship.go`. Added stats to `Ships` map: Attack: 60, Defense: 200, Speed: 0, Cost: 100/150/50.