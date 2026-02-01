# [MEO-213] Prefetch adjacent sectors to eliminate transition blink

**Status:** Done

---

## Solution

1. **Prefetch adjacent sector data** - When viewing S55, prefetch S54, S56, S45, S65 (all 4 directions)
2. **Cache API responses** - Use React Query or SWR for caching
3. **Prefetch Next.js routes**
4. **Store prefetched data**

## Comments

### Petr Kubelka (2026-01-31T23:24:02.484Z)

## Resolution

**Issue:** Planets were not displaying in sector maps because the galaxy lookup was failing.

**Root Cause:** The URL parameter `galaxyName` contains the `galaxy_id` (UUID), but the lookup code was only searching by `galaxy.name`. The comparison `g.name.toLowerCase() === '19a59098-3556-4c01-aa2a-ee7108c76b08'` would never match.

**Fix:** Updated all galaxy lookup code to search by `galaxy_id` first, then fall back to name match.

**Files Modified:**
- `lib/hooks/useSectorData.ts`
- `app/(game)/galaxy/[galaxyName]/page.tsx`
- `app/(game)/galaxy/[galaxyName]/reports/page.tsx`
- `app/(game)/galaxy/[galaxyName]/planet/[x]/[y]/page.tsx`
- `.env.local` - Added `NEXT_PUBLIC_API_URL=http://localhost:8080`

**Test Added:**
- `tests/galaxy.spec.ts` - "should display planets in sector map"

**Verification:**
All 12 galaxy tests pass ✅

---

### Petr Kubelka (2026-01-31T23:20:50.283Z)

## Fix Summary

**Root Cause Identified:**
The galaxy lookup logic was only searching by galaxy name, but the URL parameter (`galaxyName`) is actually the `galaxy_id` (UUID format like `19a59098-3556-4c01-aa2a-ee7108c76b08`).

**Files Fixed:**
1. `lib/hooks/useSectorData.ts` - Now searches by `galaxy_id` first, then falls back to name match
2. `app/(game)/galaxy/[galaxyName]/page.tsx` - Same fix
3. `app/(game)/galaxy/[galaxyName]/reports/page.tsx` - Same fix
4. `app/(game)/galaxy/[galaxyName]/planet/[x]/[y]/page.tsx` - Same fix

**Additional Fixes:**
- Added `NEXT_PUBLIC_API_URL=http://localhost:8080` to `.env.local`

**Test Added:**
- Added Playwright test `should display planets in sector map` in `tests/galaxy.spec.ts` that:
  1. Verifies API returns planets
  2. Checks that the sector page displays the correct planet count
  3. Verifies planet symbols are visible in the map

**Testing Required:**
Tests need the game engine to be running (`docker compose up` from `infrastructure/docker/`)

---
