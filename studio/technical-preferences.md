# Technical Preferences

## Engine & platform
- **Engine**: Unity
- **Engine builder skill**: unity-editor
- **Dimension**: 3D
- **Target platform(s)**: Android mobile APK

## Input & platform constraints
- **Input Methods**: Touch joystick, touch look, tap interaction, tap-and-hold flashlight, Android Back: gameplay → pause; pause/menu → previous menu; title screen → OS exit only after explicit confirmation.
- **Platform Notes**: Landscape orientation; target mid-range Android devices; avoid desktop-only controls; preserve readable UI at 1280x720 and 1920x1080 logical resolutions; package with an offline-first local runtime and no required network connection.
- **Performance budget**: 30 FPS target on mid-range Android; URP; baked lighting where possible; 1K texture ceiling for environment props; simple colliders; low overdraw UI; no HDRP.

## Accessibility
- **Accessibility tier**: Standard — readable high-contrast UI, vibration toggle, brightness control, subtitle toggle, reduced-flash option, and audio-independent visual threat cues.

## Relevant skills
- `unity-editor` — Unity project creation, scene/prefab authoring, compile checks, Play Mode, screenshots, and Android export.
- `unity-game-builder` — Unity game orchestration, project ledger, content floor, validation matrix, and packaging gates.
- `unity-horror-fps-endless` — horror FPS atmosphere and interaction conventions; adapted to a finite three-chapter exploration game rather than an endless runner.
- `game-project-validator` — compile, startup, runtime interaction, diagnostics, and evidence checks.
- `project-doc-maintainer` — durable PROJECT/STATUS/CHANGELOG handoff files.
- `agent-browser` — browser-based inspection/testing when a browser preview or GitHub web interaction is required.

## Location
- **Workspace root**: E:\077ee885-3fb1-4ef8-80a3-165475f721a6\assets\games\signal_in_the_fog\workspace
