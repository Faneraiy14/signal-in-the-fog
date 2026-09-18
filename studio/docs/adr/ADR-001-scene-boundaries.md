# ADR-001 — Unity project and scene boundaries

## Status
Accepted

## Decision
Use a Unity 6 URP project with a persistent Bootstrap scene and three sequential chapter scenes. Chapter State owns transitions; services persist only when their state must survive scene unload.

## Rationale
This keeps Android memory predictable, preserves authored pacing, and prevents gameplay systems from becoming mutually coupled scene loaders.

## Consequences
- Every chapter needs deterministic spawn, relay, clue, pickup, and hide-volume IDs.
- Scene transition and save tests are blocking validation rows.
- The final APK can still run offline with no external service.
