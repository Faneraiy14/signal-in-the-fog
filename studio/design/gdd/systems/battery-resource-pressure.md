# System GDD — Battery and Resource Pressure

## 1. Overview
Battery is the only finite resource. It powers the flashlight and radio, creating a controlled choice between visibility and information.

## 2. Player Fantasy
Every light beam is a decision. The player is not counting ammunition; they are deciding when to see, when to listen, and when to move blind.

## 3. Detailed Rules
- Battery is a float percentage from 0 to 100; the HUD rounds to the nearest whole percentage for display.
- Flashlight drain is 0.035 units/s while on.
- Radio drain is 0.08 units/s while broadcasting.
- Battery pickups are authored in three locations and restore 25 units, capped at 100.
- At or below 25, the flashlight flickers and the HUD enters low-power state.
- At zero, flashlight and radio turn off and cannot be re-enabled until a pickup is collected.
- The player starts each new game at 85 battery; chapter transitions preserve battery.

## 4. Formulas
### Battery after frame
`batteryNext = clamp(batteryCurrent - (flashlightOn * 0.035 + radioOn * 0.08) * deltaTime + pickupAmount, 0, 100)`

| Variable | Type | Range | Source | Description |
|---|---|---:|---|---|
| `batteryCurrent` | float | 0–100 | resource state | Battery before update |
| `flashlightOn` | int | 0–1 | input | Flashlight state |
| `radioOn` | int | 0–1 | signal system | Radio state |
| `pickupAmount` | float | 0 or 25 | pickup event | One-shot recharge |
| `deltaTime` | float | 0–0.1 s | engine | Frame time |

Output range: `0..100`. Example: both tools on for 1 s consumes `0.115` units.

## 5. Edge Cases
- GIVEN a pickup is collected at full charge WHEN the event fires THEN consume the pickup but keep battery at 100.
- GIVEN battery reaches zero during repair WHEN radio shutdown occurs THEN cancel no repair progress and show the low-power cue.
- GIVEN a checkpoint reloads WHEN the pickup was collected before that checkpoint THEN it remains collected.
- GIVEN the app is backgrounded WHEN it resumes THEN battery must not drain while no gameplay frames run.

## 6. Dependencies
- Depends on: Input, Signal Tuning, Game State, Save.
- Provides to: Flashlight, radio, UI warning, audio flicker cues.
- Save owns collected-pickup persistence; UI owns presentation of the resource value.

## 7. Tuning Knobs
| Knob | Current | Safe range | Effect |
|---|---:|---:|---|
| Starting battery | 85 | 60–100 | Early pressure |
| Flashlight drain | 0.035/s | 0.02–0.06 | Visibility cost |
| Radio drain | 0.08/s | 0.04–0.12 | Information cost |
| Pickup recharge | 25 | 15–35 | Recovery value |

## 8. Acceptance Criteria
- GIVEN a full battery WHEN the flashlight is held for 10 seconds THEN the value decreases by about 0.35.
- GIVEN battery is at zero WHEN the player taps flashlight or radio THEN neither device activates.
- GIVEN a pickup is collected WHEN the battery HUD updates THEN it displays the capped post-pickup value.
- GIVEN a checkpoint reloads WHEN the player returns to the room THEN collected recharge items are not duplicated.
