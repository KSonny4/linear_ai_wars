# [MEO-142] Write acceptance tests for core game mechanics

**Status:** Done

---

Create comprehensive acceptance tests based on the [SKILL.md](<http://SKILL.md>) specification.

## Completed

### Domain Tests (`packages/game-engine/internal/domain/skillmd_test.go`)

* ✅ Ship stats validation (all 10 ship types)
* ✅ Module stats validation (all 13 module types)
* ✅ Cost & time scaling exponents
* ✅ Shield generator defense bonus formula
* ✅ Resource production formula
* ✅ Storage capacity formula
* ✅ Terrain bonuses
* ✅ Terrain spawn rates
* ✅ Combat formula (attacker/defender wins, luck, shield, night bonus)
* ✅ Travel time calculation
* ✅ Manhattan distance
* ✅ Loyalty damage from sieges
* ✅ Loot mechanics (50% rule, transport capacity)
* ✅ Mission types validation
* ✅ Night time detection (00:00-06:00 UTC)
* ✅ Ship capacity (transport = 1000, others = 0)
* ✅ Combat loss percentages

### API Acceptance Tests (`packages/game-engine/tests/acceptance_test.go`)

* ✅ Public endpoint tests (health, register, galaxies, leaderboard, map)
* ✅ Authentication requirement tests
* ✅ Invalid token handling
* ✅ Agent profile response validation
* ✅ Planet details response validation
* ✅ Build module tests
* ✅ Build ships tests
* ✅ Launch fleet tests
* ✅ Rate limit tests
* ✅ Error code validation
* ✅ Initial resources validation
* ✅ Map structure validation (coordinates, sectors)

### CI/CD

* ✅ Added `make test` and `make test-game` targets
* ✅ Created \`.github/workflows/test.yml` for automated testing

## Files Changed

* 
étairepackages/game-engine/internal/domain/skillmd_test.goétaire - Extended with 100+ more test cases
* 
étairepackages/game-engine/tests/acceptance_test.goétaire - NEW - API acceptance tests
* 
étaireMakefileétaire - Added test targets
* 
étaire.github/workflows/test.ymlétaire - NEW - CI test workflow
