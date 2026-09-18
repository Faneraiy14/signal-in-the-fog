# System GDD — Audio and Feedback

## 1. Overview
Owns adaptive ambience, radio voice treatment, threat cues, haptics, and visual/audio-independent feedback. The mix reinforces that listening is both tool and danger.

## 2. Player Fantasy
The player hears the station breathe: wind through broken seals, relay hum, distant metal, and a voice that may be human only when the radio is off.

## 3. Detailed Rules
- Exploration uses a low-density wind/structure bed with positional one-shots.
- Signal Scan adds narrow-band hiss and waveform pips; each frequency error has a distinct pitch drift.
- Threat adds low-frequency pressure, radio warble, and directional wet movement.
- Human voice is dry and close; Listener voice is phase-shifted and wider than the world.
- Relay completion resolves tension with an amber tonal chord, never a victory fanfare.
- Every threat or objective cue has a non-audio visual equivalent.
- Haptics use short ticks for tuning lock, one pulse for low battery, and a patterned pulse for threat.

## 4. Formulas
### Threat mix intensity
`mixIntensity = clamp(exposure / 100 + radioOn * 0.15, 0, 1)`

| Variable | Type | Range | Source | Description |
|---|---|---:|---|---|
| `exposure` | float | 0–100 | threat | Current danger exposure |
| `radioOn` | int | 0–1 | signal | Broadcast state |
| `mixIntensity` | float | 0–1 | derived | Threat audio bus intensity |

Output range: `0..1`. Example: exposure 50 with radio on = `0.65`.

## 5. Edge Cases
- GIVEN the player mutes audio WHEN a threat cue fires THEN visual directional feedback still communicates danger.
- GIVEN the app is backgrounded WHEN it resumes THEN loops restart from a safe mix snapshot rather than doubling.
- GIVEN voice volume is zero WHEN a critical line plays THEN subtitles and waveform timing remain intact.
- GIVEN reduced flash is enabled WHEN a low-frequency hit occurs THEN replace haptic intensity with the accessibility-safe pulse.

## 6. Dependencies
- Depends on: Game State, Threat, Signal Tuning, Battery, UI settings.
- Provides to: player feedback, pacing state, authored scare events.
- Audio reads published state only and never controls objective completion.

## 7. Tuning Knobs
| Knob | Current | Safe range | Effect |
|---|---:|---:|---|
| Threat low-pass floor | 180 Hz | 120–300 Hz | Pressure character |
| Radio hiss level | -18 dB | -24 to -12 dB | Information texture |
| Cue cooldown | 1.2 s | 0.6–3 s | Avoids repetitive pings |
| Haptic pulse length | 80 ms | 40–140 ms | Mobile readability |

## 8. Acceptance Criteria
- GIVEN radio turns on WHEN the mix updates THEN radio hiss and battery feedback begin within 0.2 seconds.
- GIVEN exposure rises WHEN threat intensity crosses a band THEN the mix changes without a click or abrupt volume jump.
- GIVEN the player disables haptics WHEN a relay locks THEN no vibration is requested.
- GIVEN audio is unavailable WHEN the player enters an encounter THEN visuals alone still expose the threat state.
