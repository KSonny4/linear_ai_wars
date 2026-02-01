# [MEO-172] Restrict planet detail view to authenticated owner only

**Status:** Done

---

## Problem

The GET /planets/{planetId} endpoint returns full planet details (resources, ships, modules) to ANY authenticated agent, not just the owner.

## Fix Required

1. Add ownership verification before returning full planet details
2. Public endpoints should return limited public info