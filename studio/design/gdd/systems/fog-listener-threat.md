# System GDD — Fog Listener Threat

## 1. Overview
The Fog Listener is a non-combat pursuit threat that reacts to radio use, line of sight, and player noise. It creates readable escalation without weapon combat.

## 2. Player Fantasy
Fear comes from knowing the rules and hearing them fail. The player can choose silence, hide, or risk a broadcast for information.

## 3. Detailed Rules
- Threat states: Dormant, Investigate, Search, Pursue, Attack, Recede.
- It is dormant outside the authored encounter window.
- Active radio adds suspicion; powered relay rooms make it more interested.
- It prefers corridors and fog volumes and never teleports into the player's view.
- Search follows the last known signal point and checks nearby hide volumes.
- Hide breaks pursuit only after 2.0 s without line of sight and with radio off.
- Exposure starts at 0, increases by 35 on a resolved attack, and decays by 20 after 4 seconds without a resolved attack. It resets to the checkpoint value on reload; the default checkpoint value is 0.
- Hide contract: the player can enter only an authored hide volume while not in Attack; entering locks locomotion to the hide state, disables radio, and exposes Exit Hide. The threat must have no line of sight for 2.0 seconds before pursuit can break. Hide volumes are never saved as a separate inventory state.

## 4. Formulas
### Suspicion change
`deltaSuspicion = radioOn * 6 - (radioOff * noLineOfSight * 3)`

| Variable | Type | Range | Source | Description |
|---|---|---:|---|---|
| `radioOn` | int | 0–1 | signal system | Whether the radio is broadcasting |
| `radioOff` | int | 0–1 | signal system | Inverse of radioOn |
| `noLineOfSight` | int | 0–1 | threat query | 1 when the threat cannot see the player |
| `deltaSuspicion` | float | -3..6 / s | derived | Threat suspicion rate |

Output range: `-3..6` per second before clamping suspicion to `0..100`. Example: radio on gives `+6/s`; radio off without line of sight gives `-3/s`.

## 5. Edge Cases
- GIVEN the Listener is behind a closed gate WHEN pursuit begins THEN it searches the gate and cannot cross until its authored opening event.
- GIVEN the player hides while the threat is attacking WHEN the attack animation begins THEN resolve the attack first, then enter Search.
- GIVEN the Listener loses navigation data WHEN it reaches an invalid waypoint THEN fall back to the last valid waypoint and Recede after 4 seconds.
- GIVEN reduced-flash is enabled WHEN an attack occurs THEN use low-intensity pulse, spatial audio, and UI vignette instead of strobing.

## 6. Dependencies
- Depends on: Signal Tuning, Locomotion, Hide interaction, Game State, Audio.
- Provides to: Threat UI, exposure/lose, authored scare events, audio intensity.
- Locomotion exposes player position; signal exposes radio and relay noise; game state gates threat lifecycle.

## 7. Tuning Knobs
| Knob | Current | Safe range | Effect |
|---|---:|---:|---|
| Suspicion gain | 6/s | 3–10/s | Radio risk |
| Suspicion decay | 3/s | 1–6/s | Recovery pace |
| Hide break time | 2.0 s | 1–4 s | Hide reliability |
| Attack exposure | 35 | 20–60 | Failure proximity |

## 8. Acceptance Criteria
- GIVEN the player broadcasts in an active encounter WHEN 3 seconds pass THEN the Listener receives a signal event and can enter Investigate.
- GIVEN the player turns off the radio and hides WHEN line of sight is broken for 2 seconds THEN pursuit can transition to Search/Recede.
- GIVEN exposure reaches 100 WHEN the attack resolution completes THEN the Game State receives exactly one Lose event.
- GIVEN no encounter is active WHEN the player walks through a chapter THEN no hidden threat can damage or fail the run.
