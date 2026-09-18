# System GDD — Local Save and Resume

## 1. Overview
Provides deterministic offline saves for checkpoints, clue collection, settings, ending history, and pickup collection. It is resilient to interrupted mobile sessions.

## 2. Player Fantasy
The player can stop after a frightening session and return without losing meaningful progress, while failure still retains tension because it returns to a deliberate checkpoint.

## 3. Detailed Rules
- Save format is versioned JSON in the platform persistent-data path.
- Save is written on new game, relay completion, clue completion, pickup collection, setting changes, ending completion, and clean pause.
- Writes use temporary-file then replace semantics where supported.
- Save schema includes version, chapter, phase, checkpoint id, battery, clue ids, pickup ids, settings, and ending flags.
- Checkpoint restore uses the exact serialized battery and collected-state values from that checkpoint; it never resets battery to a chapter default.
- Resume validates version and required fields before restoring.
- Corrupt or incompatible data is moved to a recovery slot and the player is offered New Game.
- No network account or telemetry is required.

## 4. Formulas
### Save freshness
`freshness = min(1, secondsSinceCheckpoint / targetInterval)`

| Variable | Type | Range | Source | Description |
|---|---|---:|---|---|
| `secondsSinceCheckpoint` | float | 0+ | runtime | Time since last checkpoint |
| `targetInterval` | float | 30–180 s | design | Desired checkpoint interval |
| `freshness` | float | 0–1 | derived | UI/debug freshness indicator |

Output range: `0..1`. Example: 90 seconds after a 120-second target gives `0.75`.

## 5. Edge Cases
- GIVEN a save write is interrupted WHEN the game restarts THEN load the last complete save and never parse a partial file.
- GIVEN an older schema is found WHEN resume is selected THEN migrate supported fields and reset only unknown fields to defaults.
- GIVEN no save exists WHEN Continue is tapped THEN disable Continue and explain that New Game is required.
- GIVEN the app is killed during a threat WHEN it resumes THEN restore the last completed checkpoint, not the threat's transient position.

## 6. Dependencies
- Depends on: Game State, Narrative, Battery, Settings, chapter objective events.
- Provides to: Main Menu Continue, checkpoint restore, replay endings.
- Systems emit serializable events; Save owns file I/O and migration.

## 7. Tuning Knobs
| Knob | Current | Safe range | Effect |
|---|---:|---:|---|
| Save schema version | 1 | integer | Migration contract |
| Backup slots | 1 | 1–2 | Recovery safety |
| Autosave debounce | 0.5 s | 0.2–2 s | Write frequency |
| Checkpoint interval target | relay event | 30–180 s | Recovery pacing |

## 8. Acceptance Criteria
- GIVEN a relay completes WHEN the app is force-closed immediately after THEN the next launch restores the completed relay or the prior safe checkpoint deterministically.
- GIVEN settings change WHEN the player returns to the menu THEN settings persist across relaunch.
- GIVEN save data is corrupt WHEN Continue is selected THEN no crash occurs and recovery/New Game is offered.
- GIVEN the final ending completes WHEN the player chooses Replay THEN the final chapter can be entered without losing ending history.
