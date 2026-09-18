# Cross-System GDD Review — Signal in the Fog

**Date:** 2026-04-29  
**Reviewer:** Studio batch review  
**Scope:** Phase 2 design package and shared registry

## Review result
The first review found six substantive contract risks and several missing acceptance-critical details. All were resolved in the design package before architecture work began.

## Resolutions

1. **Chapter completion:** `Chapter and Game State` is the sole transition owner. `RelayRepaired` completes the authored chapter; the following narrative beat is presentation-only.
2. **Battery precision:** Battery is stored as a float from 0–100 and rounded only for HUD display. Drain formulas and examples now agree.
3. **Failure recovery:** Restart restores the exact serialized checkpoint battery and collected-state values. No chapter-default reset is used.
4. **Threat suspicion:** The formula now separates `radioOn`, `radioOff`, and `noLineOfSight`, making recovery behavior explicit.
5. **Scope baseline:** The concept now reports 10 coordinated systems, matching the systems index.
6. **Android Back:** Gameplay → pause; pause/menu → previous menu; title screen → OS exit only after confirmation.
7. **Hide/exposure contract:** The threat GDD now defines authored hide volumes, entry/exit rules, radio shutdown, line-of-sight break time, exposure start/attack/recovery, and checkpoint behavior.
8. **Objective and pickup registry:** Each chapter now lists one relay objective, unique battery pickup IDs, and unique hide-volume IDs.
9. **Ending eligibility:** The narrative bible and GDD both define `Answer` at three or more recovered clues; `Sever` is always eligible.

## Approval
No unresolved substantive cross-system conflicts remain for Phase 3 architecture. Implementation must preserve the ownership contracts in `systems-index.md` and the values in `registry/entities.yaml`.
