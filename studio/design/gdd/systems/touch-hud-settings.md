# System GDD — Touch HUD, Settings, and Subtitles

## 1. Overview
Presents input controls, objectives, battery, signal state, subtitles, pause, accessibility, and ending choices without breaking the sparse horror composition.

## 2. Player Fantasy
The interface feels like a field kit, not a game dashboard: amber instrumentation is useful, quiet, and easy to read under stress.

## 3. Detailed Rules
- HUD shows battery, relay objective, signal state, and one contextual action at a time.
- Waveform is the main radio feedback; text labels clarify the objective but never solve the frequency.
- Subtitles are on by default and include speaker labels for radio voices.
- Settings include brightness, master/music/voice/SFX volume, vibration, subtitles, reduced flash, and sensitivity.
- Pause offers Resume, Restart Checkpoint, Settings, and Main Menu with confirmation.
- Critical threat cues have visual equivalents: vignette, directional waveform, or objective banner.
- Touch targets respect 96 dp minimum and maintain contrast against fog.

## 4. Formulas
### HUD contrast ratio target
`contrastRatio = (Lbright + 0.05) / (Ldark + 0.05)`

| Variable | Type | Range | Source | Description |
|---|---|---:|---|---|
| `Lbright` | float | 0–1 | UI colors | Relative luminance of brighter color |
| `Ldark` | float | 0–1 | UI colors | Relative luminance of darker color |
| `contrastRatio` | float | 1–21 | derived | Readability measure |

Output range: `1..21`. Example: white against charcoal should meet at least `4.5:1` for normal text.

## 5. Edge Cases
- GIVEN a small screen WHEN the HUD would overlap the right look zone THEN stack objective text above the safe margin.
- GIVEN reduced flash is enabled WHEN a relay completes THEN replace strobe with a stable amber ring and haptic tick.
- GIVEN subtitles are enabled WHEN text exceeds two lines THEN paginate at phrase boundaries, not mid-word.
- GIVEN the player pauses during a subtitle WHEN Resume is tapped THEN resume from the same line timestamp.

## 6. Dependencies
- Depends on: Input, Game State, Battery, Threat, Narrative, Settings/Save.
- Provides to: player feedback and accessibility verification.
- Game systems publish state; HUD does not poll scene objects directly.

## 7. Tuning Knobs
| Knob | Current | Safe range | Effect |
|---|---:|---:|---|
| Minimum button size | 96 dp | 88–128 dp | Touch accuracy |
| Subtitle max lines | 2 | 2–3 | Readability |
| Low battery threshold | 25 | 15–35 | Warning timing |
| UI opacity | 0.88 | 0.7–1.0 | Visibility vs immersion |

## 8. Acceptance Criteria
- GIVEN a supported phone aspect ratio WHEN the chapter starts THEN no core button is clipped or unreachable.
- GIVEN the player enables reduced flash WHEN threat feedback occurs THEN no strobe effect is shown.
- GIVEN the player changes sensitivity WHEN returning to gameplay THEN the new value applies immediately.
- GIVEN a critical objective changes WHEN the HUD updates THEN the player can identify the next action without opening a menu.
