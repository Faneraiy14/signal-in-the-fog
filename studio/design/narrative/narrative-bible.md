# Signal in the Fog — Narrative Bible

> Durable story source for the three-chapter mobile horror game.
> Last Updated: 2026-04-29

## 1. Premise

In 1998, a mountain emergency relay station stopped answering after a storm. Twenty-seven years later, emergency technician Mara Voss receives a transmission from the station using her dead brother Elias's call sign. She climbs to the station to retrieve the relay archive, but the voice on the radio knows things only Elias could know—and something in the fog is using the signal to find her.

## 2. World Rules

- The relay station was built to route rescue traffic through a valley where fog can persist for weeks. This justifies the three relay chapters, analog consoles, and remote isolation.
- The old equipment can only transmit one narrow-band emergency signal at a time. This creates the radio-tuning interaction and makes signal use a deliberate choice.
- The Fog Listener is not a conventional ghost; it is a pattern formed by years of recorded distress calls and the people who died waiting for rescue. It can imitate voices but cannot invent a new memory.
- Warm amber light belongs to human systems. Blue-green static belongs to the Listener. This rule constrains lighting, VFX, and threat readability.
- The station’s doors, fuses, and relay cabinets are ordinary physical systems. The supernatural changes information and orientation, not every physical rule.

## 3. Factions / Forces

- **Mara Voss:** player character; practical emergency technician who wants proof before belief.
- **The Mountain Service:** absent institution whose archived procedures teach the player how to operate the station.
- **The Caller:** the voice on the radio; may be Elias, an imitation, or a composite of trapped voices depending on the ending.
- **The Fog Listener:** antagonist force; follows active signals, distorts distance, and pressures the player into hiding.

## 4. Key Characters

### Mara Voss
- Position: Player character / reluctant investigator.
- Personality: Methodical, self-controlled, emotionally avoidant.
- Gameplay role: Movement, flashlight, tuning, repair, hiding, and final choice.
- Visual anchor: Yellow storm jacket sleeve and a rugged handheld meter visible during interactions.

### Elias Voss
- Position: Absent brother / emotional anchor.
- Personality: Warm, patient, and increasingly uncertain in the recordings.
- Gameplay role: Radio voice, tape clues, and the moral ambiguity of answering.
- Visual anchor: Red service tag and a handwritten frequency notation.

### Dispatcher Vale
- Position: Archived training voice / unreliable guide.
- Personality: Calm procedural language that becomes subtly wrong.
- Gameplay role: Teaches controls through diegetic instructions and signals chapter transitions.
- Visual anchor: Green maintenance stamps and numbered relay cards.

### The Fog Listener
- Position: Antagonist / emergent signal entity.
- Personality: Mimics intimacy, becomes less human when ignored.
- Gameplay role: Patrol pressure, proximity audio, visual distortion, forced hiding.
- Visual anchor: Too-tall silhouette, reflective wet surface, waveform-like head movement.

## 5. Tone and Themes

- Overall tone: quiet grief becoming active dread.
- Themes: whether evidence can replace mourning; what we owe voices that ask to be heard; technology as both comfort and witness.
- Forbidden drift: no comedic monster banter, no gore spectacle, no lore encyclopedia, no villain monologue that fully explains the Listener.

## 6. Story Beats

1. **Arrival — Gatehouse:** Mara reaches the locked station, hears Elias's call sign, finds a manual, and restores Relay 01. The first anomaly is a voice from inside an empty room.
2. **Recognition — Relay Hall:** The second tape contains a memory only Mara and Elias shared. The radio briefly shows a second waveform moving behind her.
3. **Rule Reveal — Service Tunnels:** Dispatcher Vale’s procedure says to shut off the signal when footsteps reverse direction. The player learns the Listener tracks broadcasts, not light.
4. **Loss of Control — Flooded Maintenance:** Relay 02 restoration changes the tunnel layout. The player must trust landmarks rather than the apparent corridor length.
5. **Confrontation — Summit Array:** Elias asks Mara to complete the final transmission. The Listener uses multiple voices; only one repeats a true memory.
6. **Ending A — Sever:** Mara destroys the transmission coil, escapes into dawn fog, and leaves the station silent. The final radio click is unanswered.
7. **Ending B — Answer:** Mara completes the transmission. The screen remains on the station frequency as a new voice says, “Now we can hear you.”

## 7. Ludonarrative Alignment

The story values listening carefully and refusing false certainty. The core loop rewards patient signal use but makes it dangerous, so the player embodies Mara’s conflict rather than simply hearing exposition. The game never rewards random aggression; the antagonist is survived through attention, restraint, and route knowledge.

## 8. Implementation Notes

- All story text is short, subtitle-ready, and readable without audio.
- Tapes are optional but each gives a mechanical clue, not only lore.
- Chapter transitions are driven by the `RelayRepaired` event. The authored narrative beat that follows is a presentation gate, not a second quest/objective layer.
- The ending choice is presented through a physical console interaction and a confirmation prompt, not an abstract menu. `Answer` is eligible at three or more recovered clues; `Sever` is always eligible.
