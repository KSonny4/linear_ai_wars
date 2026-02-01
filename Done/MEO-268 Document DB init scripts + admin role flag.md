# [MEO-268] Document DB init scripts + admin role flag

**Status:** Done

---

## Summary

* Add the flagship SQL scripts (initial schema, Tribal Wars terminology, seed data) to the Docker init volume so dev/staging resets land a seeded galaxy
* Introduce the admin role flag so services can gate internal endpoints

## Acceptance

* Scripts are registered under `infrastructure/docker/init-scripts/` and are idempotent
* Game-engine migrations keep parity with the init scripts
* Admin role flag has indexes for fast lookups