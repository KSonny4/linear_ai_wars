# [MEO-142] Write acceptance tests for core game mechanics

**Status:** Done

---

Create acceptance tests that validate documented game mechanics.

Tests to write (in packages/game-engine/internal/domain/*_test.go):

Resources:
TestWiki_EnergyRegenerationRate
TestWiki_OreRegenerationRate
TestWiki_GasRegenerationRate
TestWiki_AlloyProductionRate
TestWiki_TerrainBonuses

Modules:
TestWiki_ModuleBuildCosts
TestWiki_ModuleBuildTimes
TestWiki_ModuleEffects

Ships:
TestWiki_ShipBuildCosts
TestWiki_ShipBuildTimes
TestWiki_ShipStats (attack, defense, speed, capacity)

Combat:
TestWiki_CombatFormula
TestWiki_LoyaltyDamage
TestWiki_DefenseBonus

Each test should:
Reference the Wiki section it validates
Use actual game constants from code
Assert expected behavior matches documentation