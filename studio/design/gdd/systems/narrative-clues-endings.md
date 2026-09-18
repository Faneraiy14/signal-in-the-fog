# System GDD — Narrative Clues and Endings

## 1. Overview
Delivers the authored story through tapes, radio exchanges, environmental text, and two final choices. Narrative objects are replayable but do not interrupt locomotion without consent.

## 2. Player Fantasy
The player reconstructs a human tragedy from damaged evidence and must decide whether truth is worth carrying back into the world.

## 3. Detailed Rules
- Six story clues are authored: two per chapter, with one optional clue in each chapter.
- Clues are categorized as Human, False, or Listener-corrupted; the player is never shown the category directly.
- Radio conversations unlock after relay milestones and use subtitle-first delivery.
- At the Summit Array, the player chooses `Sever the Signal` or `Answer the Call`.
- Sever is always available; Answer requires at least three recovered clues.
- Ending state is saved so the player can replay the final chapter and see the other ending.

## 4. Formulas
### Answer eligibility
`answerEligible = (recoveredClues >= 3)`

| Variable | Type | Range | Source | Description |
|---|---|---:|---|---|
| `recoveredClues` | int | 0–6 | clue registry | Clues found by player |
| `answerEligible` | bool | false/true | derived | Whether Answer choice is enabled |

Output range: boolean. Example: 2 clues -> false; 3 clues -> true.

## 5. Edge Cases
- GIVEN a clue was found before a crash WHEN the checkpoint reloads THEN it is present if the clue-save event completed.
- GIVEN a tape is replayed WHEN the player exits it THEN no duplicate clue count is added.
- GIVEN the player reaches the ending with fewer than three clues WHEN Answer is selected by stale UI input THEN route to Sever and log a guarded choice.
- GIVEN subtitles are disabled WHEN a story beat plays THEN present equivalent waveform/visual cue and keep critical objective text enabled.

## 6. Dependencies
- Depends on: Game State, Save, Audio, UI, Signal Tuning.
- Provides to: ending choice, chapter gates, narrative journal, analytics-free local completion summary.
- UI owns reading controls; save owns clue persistence; audio owns voice/radio playback.

## 7. Tuning Knobs
| Knob | Current | Safe range | Effect |
|---|---:|---:|---|
| Total clues | 6 | 4–9 | Narrative density |
| Answer threshold | 3 | 2–6 | Exploration requirement |
| Radio line length | 12 s | 6–20 s | Pacing |
| Replay speed | 1x | 1x–1.5x | Accessibility/replay |

## 8. Acceptance Criteria
- GIVEN a clue interaction completes WHEN the player exits it THEN the clue count increases at most once.
- GIVEN three clues are recovered WHEN the final choice opens THEN Answer is enabled and explained by contextual text.
- GIVEN fewer than three clues are recovered WHEN the final choice opens THEN Answer is visibly locked and Sever remains actionable.
- GIVEN an ending completes WHEN the credits screen opens THEN the chosen ending and clue count persist locally.
