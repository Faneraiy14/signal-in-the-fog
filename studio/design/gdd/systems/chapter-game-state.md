# System GDD — Chapter and Game State

## 1. Overview
Owns the authoritative game state machine, chapter transitions, win/lose/restart flow, checkpoint events, pause, and ending selection. Systems subscribe to state changes rather than changing global state directly.

## 2. Player Fantasy
The player always understands what kind of danger they are in and what progress remains, even when the world itself is disorienting.

## 3. Detailed Rules
- Boot enters Main Menu, then Chapter 1 on New Game.
- Chapters are `Gatehouse`, `Service Tunnels`, and `Summit Array`.
- Runtime phases are `Exploration`, `SignalScan`, `Threat`, `Paused`, `Ending`, `Win`, and `Lose`.
- A chapter completes when its relay objective completes. The following narrative beat is a presentation gate that runs after `RelayRepaired`; it does not add a second quest layer.
- Checkpoints are written after each restored relay and at chapter start; restart restores the exact serialized checkpoint battery and collected-state values.
- Lose returns to the latest checkpoint after a short failure card; Restart from pause resets the active chapter checkpoint.
- The third relay opens `Sever` and `Answer` ending choices; both end in a credits screen.
- Android Back pauses during gameplay, returns from pause/menu to the previous menu, and exits from the title screen only after explicit confirmation.

## 4. Formulas
### Chapter progress
`progress = completedObjectives / totalObjectives`

| Variable | Type | Range | Source | Description |
|---|---|---:|---|---|
| `completedObjectives` | int | 0–3 | objective manager | Relay/story objectives done in chapter |
| `totalObjectives` | int | 1–3 | chapter data | Authored chapter objective count |
| `progress` | float | 0–1 | derived | UI progress value |

Output range: `0..1`. Example: 2 of 3 objectives gives `0.667`.

## 5. Edge Cases
- GIVEN a pause request during a cutscene WHEN the cutscene is skippable THEN pause at the next safe frame.
- GIVEN a scene load fails WHEN a checkpoint is requested THEN retain the current save and show a recoverable load error.
- GIVEN the player dies during a relay repair WHEN reload begins THEN the relay remains incomplete unless its checkpoint event already fired.
- GIVEN New Game is chosen with an existing save WHEN confirmation is accepted THEN replace progress only after the confirmation action.

## 6. Dependencies
- Depends on: Save/Resume, Relay Interaction, Narrative, UI, Audio.
- Provides to: every system through a read-only state service and transition events.
- Save consumes checkpoint events; UI and audio consume phase transitions.

## 7. Tuning Knobs
| Knob | Current | Safe range | Effect |
|---|---:|---:|---|
| Checkpoint cadence | relay complete | 30–180 s | Recovery burden |
| Failure card duration | 2.0 s | 1–4 s | Pacing after loss |
| Pause fade | 0.2 s | 0.1–0.5 s | Input feedback |
| Ending choice timeout | none | none–30 s | Player agency |

## 8. Acceptance Criteria
- GIVEN a new install WHEN New Game is tapped THEN Chapter 1 starts from a deterministic spawn.
- GIVEN all chapter objectives are done WHEN the relay completion event fires THEN the next chapter opens exactly once.
- GIVEN a threat attack fills exposure WHEN the lose event fires THEN gameplay stops and the checkpoint screen appears.
- GIVEN either final ending is selected WHEN the ending sequence completes THEN progress is saved and replay is available.
