# Technical Architecture — Signal in the Fog

## Runtime topology
- The Unity project lives in the workspace `unity/` subdirectory so the root can also carry the durable studio ledger and GitHub source documentation.
- Unity 6 3D URP project, offline-first, landscape Android target.
- One bootstrap scene owns services; three additive chapter scenes are loaded sequentially to keep memory bounded.
- Runtime services are plain C# MonoBehaviours with one owner each: `GameStateService`, `InputService`, `LocomotionController`, `SignalRelayController`, `BatteryService`, `FogListenerController`, `NarrativeService`, `SaveService`, `AudioFeedbackService`.
- UI uses UI Toolkit with one HUD document, one pause/settings document, and one ending document. UI reads read-only state and emits commands.

## Scene plan
- `Bootstrap`: service composition, settings load, input actions, persistent audio, scene transition.
- `Chapter_Gatehouse`: gatehouse geometry, Relay 01, first clue, battery pickup, hide volume, tutorial encounter.
- `Chapter_ServiceTunnels`: tunnel kit, Relay 02, two clues, battery pickup, two hide volumes, pursuit encounter.
- `Chapter_SummitArray`: summit geometry, Relay 03, two clues, battery pickup, ending console, final encounter.
- All scene transitions are owned by `GameStateService`; no gameplay system calls `SceneManager` directly.

## Data contracts
- Shared values are mirrored from `studio/design/registry/entities.yaml` into Unity `ScriptableObject` chapter data during editor authoring.
- Relay data exposes target frequency, tolerance, repair duration, completion event, and chapter id.
- Threat data exposes encounter window, patrol anchors, hide-volume ids, suspicion/exposure tuning, and authored state transitions.
- Save schema is versioned JSON and stores only serializable state, not scene object references.

## Input and accessibility
- Unity Input System actions map to Move, Look, Interact, Flashlight, Radio, Tune, Hide, Pause, and RestartCheckpoint.
- Touch UI invokes the same public commands as action callbacks.
- Every audio-only critical cue has a visual event; reduced-flash removes strobes; haptics are optional.

## Mobile performance budget
- 30 FPS target on mid-range Android.
- URP, baked environment lighting, capped real-time lights, 1K textures, pooled threat VFX, no HDRP.
- No runtime network dependency; no telemetry.
- Chapter scenes unload before loading the next; audio service persists.

## Build and validation
- Debug APK is produced for validation; release signing is configured only when credentials are available.
- Required gates: compile clean, scene startup, touch entry, core loop, content floor, asset replacement, UI/accessibility, Android build, APK launch path.
- Play Mode interaction and screenshots require the one-time runtime-validation consent recorded in `studio/stage.md`.
