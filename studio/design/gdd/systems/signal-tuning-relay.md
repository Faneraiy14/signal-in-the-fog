# System GDD — Signal Tuning and Relay Interaction

## 1. Overview
Turns the three relay rooms into readable risk/reward puzzles. The player explores for a relay, aligns a narrow frequency band, then holds a repair interaction while the radio exposes their location.

## 2. Player Fantasy
The player becomes a field technician making a dangerous repair with improvised tools while an unseen listener learns the sound of every mistake.

## 3. Detailed Rules
- Each chapter contains one primary relay and one optional calibration terminal.
- Tuning opens a focused overlay and temporarily reduces movement to steady mode.
- Frequency is normalized to `0..100`; the target band is authored per relay.
- The target is revealed through waveform stability, not a text answer.
- A correct band requires absolute error ≤2.0 for 1.5 continuous seconds.
- Relay repair requires a 5-second hold with three authored micro-failures at 2 s, 3.5 s, and 4.5 s.
- Releasing early preserves no repair progress but does not reset the chapter.
- Signal active drains battery and raises the Fog Listener suspicion.

## 4. Formulas
### Tuning accuracy
`accuracy = max(0, 1 - abs(currentFrequency - targetFrequency) / 50)`

| Variable | Type | Range | Source | Description |
|---|---|---:|---|---|
| `currentFrequency` | float | 0–100 | tuner | Player-selected frequency |
| `targetFrequency` | float | 0–100 | relay data | Authored relay band center |
| `accuracy` | float | 0–1 | derived | Waveform stability value |

Output range: `0..1`. Example: target 62, current 60 gives `0.96`.

## 5. Edge Cases
- GIVEN the player enters the correct band WHEN the signal is interrupted by a scare THEN the stability timer pauses rather than completing invisibly.
- GIVEN battery reaches zero WHEN the tuner is open THEN close the tuner and show a recovery hint.
- GIVEN another player-facing event requests a scene load WHEN repair is active THEN cancel repair and save no partial progress.
- GIVEN a relay is already complete WHEN the player revisits it THEN show its story interaction but do not duplicate completion rewards.

## 6. Dependencies
- Depends on: Input, Battery, Game State, Narrative, Threat.
- Provides to: Chapter progression, radio audio state, UI waveform, checkpoint save.
- Threat consumes signal-active and relay-room noise events; UI consumes tuning accuracy.

## 7. Tuning Knobs
| Knob | Current | Safe range | Effect |
|---|---:|---:|---|
| Correct tolerance | ±2.0 | ±1–4 | Puzzle difficulty |
| Stability duration | 1.5 s | 0.8–2.5 s | Required precision |
| Repair duration | 5.0 s | 3–8 s | Exposure window |
| Tuning rate | 18 units/s | 10–30 | Touch response |

## 8. Acceptance Criteria
- GIVEN a relay is unpowered WHEN the player aligns its band and holds repair THEN it completes once after 5 seconds.
- GIVEN the player releases repair early WHEN the interaction ends THEN the relay remains incomplete and the radio closes.
- GIVEN a wrong frequency is selected WHEN the stability timer runs THEN no completion event fires.
- GIVEN the relay completes WHEN the completion event fires THEN chapter progress, audio, and checkpoint systems receive one event.
