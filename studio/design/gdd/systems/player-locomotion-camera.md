# System GDD — Player Locomotion and Camera

## 1. Overview
Provides first-person movement, collision, camera limits, and hide-space positioning. Mara is deliberately human-scale and vulnerable; there is no combat movement or jump.

## 2. Player Fantasy
Walking through the station should feel measured and unsafe. The player reads corners, doorways, and light pools instead of sprinting through a level.

## 3. Detailed Rules
- Character controller uses capsule collision and gravity.
- Walk speed is 2.2 m/s; an optional steady mode reduces speed to 1.4 m/s while hiding or lining up a signal.
- Vertical camera pitch is clamped to `[-75°, 75°]`.
- Horizontal yaw is unrestricted but interpolated to avoid nausea.
- Stairs use a 0.25 m step offset; ledges above 0.35 m block movement.
- Crouch is not a free movement mode; Hide transitions the player into a designated hide volume and locks movement until exit.
- Doors and gates own their colliders and report passability to locomotion.

## 4. Formulas
### Ground displacement
`displacement = move * speed * deltaTime`

| Variable | Type | Range | Source | Description |
|---|---|---:|---|---|
| `move` | Vector2 | magnitude 0–1 | Input | Desired planar direction |
| `speed` | float | 1.4–2.2 m/s | state | Current locomotion speed |
| `deltaTime` | float | 0–0.1 s | engine | Frame time |
| `displacement` | Vector3 | 0–0.22 m/frame | derived | Collision-tested movement |

Output range: `0..0.22 m` at the 30 FPS target. Example: full walk for 1/30 s = `0.073 m`.

## 5. Edge Cases
- GIVEN the player is inside a hide volume WHEN the threat is not in pursuit THEN Exit Hide is available and movement resumes.
- GIVEN a door closes on the player WHEN collision blocks the capsule THEN the door remains open until the player clears its safety volume.
- GIVEN the controller loses ground contact WHEN gravity is applied THEN fall speed is capped at 18 m/s.
- GIVEN a chapter loads WHEN the spawn point overlaps geometry THEN use the chapter fallback spawn marker.

## 6. Dependencies
- Depends on: Input, Chapter/Game State, door/interactable ownership.
- Provides to: Threat distance/visibility, Camera feedback, Audio listener position, Save checkpoint.
- Threat consumes the capsule position and hide state; doors consume movement collision callbacks.

## 7. Tuning Knobs
| Knob | Current | Safe range | Effect |
|---|---:|---:|---|
| Walk speed | 2.2 m/s | 1.8–2.6 | Baseline tension |
| Steady speed | 1.4 m/s | 1.0–1.8 | Signal alignment control |
| Pitch clamp | ±75° | ±65–85° | Comfort/awareness |
| Gravity | 18 m/s² | 12–24 | Grounding |

## 8. Acceptance Criteria
- GIVEN a flat corridor WHEN the player holds full forward input for 1 second THEN displacement is close to 2.2 m.
- GIVEN a wall blocks the player WHEN movement is held into it THEN no tunneling occurs.
- GIVEN a hide transition completes WHEN the player rotates the camera THEN camera remains inside the hide-space limits.
- GIVEN a chapter checkpoint loads WHEN the scene becomes ready THEN the player is upright, grounded, and facing the authored direction.
