# ADR-003 — Non-combat threat state machine

## Status
Accepted

## Decision
Implement the Fog Listener as an authored waypoint/state machine, not NavMesh-heavy emergent AI. It consumes radio/noise/visibility events and emits threat state, exposure, and failure requests.

## Rationale
The design depends on fair readable rules and a stable mobile performance budget. Authored anchors make pursuit legible and avoid expensive or unpredictable navigation.

## Consequences
- Each encounter must provide valid patrol/search anchors and fallback points.
- The Listener cannot teleport into view.
- Threat behavior must be tested against hide-volume and checkpoint contracts.
