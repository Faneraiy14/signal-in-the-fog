# ASSET_MANIFEST — Signal in the Fog

| Asset family | Source | Runtime use | Replacement / validation |
|---|---|---|---|
| Relay station structural kit | RETRIEVE or PROCEDURAL final kit | Scene-placed chapters | scale, collision, lighting, mobile draw calls |
| Tunnel and summit set dressing | RETRIEVE | Scene-placed props | grounding, silhouette, material slots |
| Player hands / flashlight / meter | RETRIEVE or PROCEDURAL visual root | First-person camera | camera framing, touch interaction visibility |
| Fog Listener silhouette | RETRIEVE or GENERATE | Threat prefab | forward axis, material, collider, threat visibility |
| Relay cabinets / antenna console | RETRIEVE | Objective prefabs | interact radius, grounded placement |
| Fuses / tapes / batteries | RETRIEVE or PROCEDURAL final props | pickups/clues | unique IDs, pickup feedback, save state |
| Fog VFX / waveform | PROCEDURAL | signal and threat feedback | reduced-flash mode, mobile performance |
| Radio static / ambience / threat beds | RETRIEVE or GENERATE | audio buses | state transitions, subtitle fallback |
| UI waveform theme | PROCEDURAL UI Toolkit | HUD, menus, subtitles | contrast, 96 dp touch targets |

No asset row is complete until it is either resolved to an imported file/prefab or explicitly documented as final procedural geometry and validated in context.
