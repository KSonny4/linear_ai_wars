# [MEO-244] Add fleet launch validation for stationary ships

**Status:** Done

---

## Task

Prevent stationary ships (Speed=0) from being sent on any mission.

## COMPLETED ✅

Added validation in `FleetService.Launch()` (`internal/service/fleet.go`). Block stationary ships from being sent on missions.