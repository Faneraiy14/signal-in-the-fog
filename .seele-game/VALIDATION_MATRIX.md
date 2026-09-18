# VALIDATION_MATRIX — Signal in the Fog

| Row | Method | Blocking | Status |
|---|---|---:|---|
| ledger.exists | Filesystem scan for all `.seele-game` files | yes | pending |
| ledger.current | Reconcile ledger with project state | yes | pending |
| project.created | `unity/` is a valid Unity project created through editor workflow | yes | passed |
| compile.clean | Unity compile/import diagnostics | yes | pending |
| scene.startup | Main scene starts without missing references | yes | pending |
| touch.entry | Touch-first menu/gameplay controls are reachable | yes | pending |
| prototype.core-loop | Move, tune, repair, threat, hide, win/lose/restart | yes | pending |
| content.floor | Required three chapters, clues, pickups, endings, escalation | yes | pending |
| content.3-minute-playthrough | Runtime slice shows variation and recovery | yes | pending |
| asset.basic | Every imported asset has usable materials/colliders/orientation | yes | pending |
| asset.replacement | Greybox stand-ins replaced or accepted as intentional final geometry | yes | pending |
| scene.placement | Placed/spawned assets grounded, readable, and coherent | yes | pending |
| ui.accessibility | UI Toolkit HUD, subtitles, contrast, reduced flash, settings | yes | pending |
| android.build | Signed/debug APK build completes and file is inspectable | yes | pending |
| playability.smoke | Approved runtime smoke: start, movement, primary verb, feedback, state change | yes | awaiting consent |
| apk.install-launch | APK installs/launches on available Android validation path | yes | pending |

Runtime rows requiring Play Mode interaction or screenshots stay blocked until the one-time user runtime-validation consent is recorded in `studio/stage.md`.
