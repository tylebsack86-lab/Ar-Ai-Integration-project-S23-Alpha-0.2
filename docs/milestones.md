# Alpha milestones

| Milestone | Deliverable | Acceptance check |
| --- | --- | --- |
| 0. Architecture | Hardware choice, boundaries, contracts | Each component and open decision is documented |
| 1. Hardware loop | Flutter host connects and displays a status card | Connect, reconnect and taps verified on Halo |
| 2. Voice loop | Tap, bounded capture, transcription and text | Question reaches HUD; cancel and errors recover |
| 3. Session controls | Opt-in record and delete on phone | Off by default; deletion verified; raw audio not saved |
| 4. Optional modalities | Spoken response and explicit camera question | Each works independently with clear capture state |

First implementation task: create the Flutter app with a mock `HaloDevicePort`, then implement the official SDK adapter after checking current examples on the chosen phone and firmware. Record SDK and firmware versions in hardware test notes.
