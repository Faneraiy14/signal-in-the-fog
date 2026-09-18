# System GDD — Input and Touch Controls

## 1. Overview
Owns mobile input translation for movement, camera look, interaction, flashlight, radio tuning, hiding, pause, and restart. It emits intent events; gameplay systems do not read raw touch controls.

## 2. Player Fantasy
The player should feel cautious and physically present: one thumb keeps Mara moving while the other searches the darkness. Important actions must be reachable without precision tapping.

## 3. Detailed Rules
- Landscape orientation is required.
- Left virtual stick emits a normalized movement vector in `[-1, 1]` on both axes.
- Right drag emits camera delta; it is clamped per frame to prevent accidental teleporting.
- A contextual Interact button appears within 2.0 m of a usable object.
- Flashlight is a hold button; releasing it turns the beam off.
- Radio is a toggle button. While open, a horizontal tuner changes frequency.
- Hide is a context action at approved lockers, cabinets, and under-console spaces.
- Pause and Android Back open the pause screen; Back does not quit immediately.
- Every primary button is at least 96 dp on the target canvas and has a visible pressed state.

## 4. Formulas
### Normalized movement vector
`move = clampMagnitude(rawStick, 1.0)`

| Variable | Type | Range | Source | Description |
|---|---|---:|---|---|
| `rawStick` | Vector2 | unbounded | touch sample | Stick displacement after dead zone |
| `move` | Vector2 | magnitude 0–1 | derived | Intent passed to locomotion |

Output range: magnitude `0..1`. Example: raw `(0.7, 0.7)` becomes approximately `(0.707, 0.707)`.

### Camera delta
`cameraDelta = clamp(rawDrag * sensitivity * deltaTime, -maxStep, maxStep)`

Output range: `[-0.12, 0.12]` radians per frame per axis at default settings.

## 5. Edge Cases
- GIVEN a touch leaves the screen WHEN the stick is active THEN release it and emit zero movement.
- GIVEN two controls overlap WHEN the player touches the upper control THEN the newest valid pointer owns only that control.
- GIVEN a modal pause is open WHEN gameplay input arrives THEN discard gameplay input.
- GIVEN reduced-motion is enabled WHEN camera delta is applied THEN use the accessibility sensitivity multiplier.

## 6. Dependencies
- Depends on: Player Locomotion, Chapter/Game State, Touch HUD, Settings.
- Provides to: Locomotion, Signal Tuning, Flashlight/Battery, Hide/Threat, Pause.
- Locomotion depends on movement vector semantics; HUD depends on action availability events.

## 7. Tuning Knobs
| Knob | Current | Safe range | Effect |
|---|---:|---:|---|
| Stick dead zone | 0.12 | 0.05–0.25 | Rejects thumb drift |
| Look sensitivity | 1.0 | 0.5–1.8 | Camera response |
| Interact radius | 2.0 m | 1.4–2.6 m | Context action reach |
| Button size | 96 dp | 88–128 dp | Touch reliability |

## 8. Acceptance Criteria
- GIVEN a fresh install WHEN the player drags both sticks THEN movement and look remain independent.
- GIVEN an interactable is in range WHEN Interact is tapped THEN exactly one interaction begins.
- GIVEN the player opens pause WHEN any gameplay control is tapped THEN no gameplay state changes.
- GIVEN Android Back is pressed during play WHEN pause is closed THEN pause opens instead of exiting.
