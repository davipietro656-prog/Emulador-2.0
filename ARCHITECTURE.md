# Architecture Overview

> **Status:** This is a conceptual architecture for Emulador-2.0, not a description of implemented modules. The repository currently contains only a README, so the components below are a proposed starting point.

```mermaid
flowchart TD
    User[User] --> UI[Frontend / Controls]
    UI -->|load ROM and configure| Loader[ROM & Configuration Loader]
    UI -->|start, pause, reset, input| Runtime[Emulation Runtime]

    Loader --> Runtime
    Runtime --> Core[Emulation Core]

    subgraph CoreComponents[Emulation Core]
        CPU[CPU / Instruction Interpreter]
        Bus[System Bus]
        Memory[Memory / Address Space]
        Devices[Peripheral Devices]
        Clock[Timing & Scheduler]

        CPU <--> Bus
        Bus <--> Memory
        Bus <--> Devices
        Clock --> CPU
        Clock --> Devices
    end

    Core --> Video[Video / Frame Output]
    Core --> Audio[Audio Output]
    Video --> UI
    Audio --> UI
    Runtime --> State[Save States & Diagnostics]
    State --> Runtime
```

## Component responsibilities

- **Frontend / Controls:** Presents the user interface and forwards control and input events.
- **ROM & Configuration Loader:** Validates and prepares program images and emulator settings.
- **Emulation Runtime:** Coordinates lifecycle operations such as starting, pausing, resetting, and stepping execution.
- **Emulation Core:** Implements CPU execution, memory and bus behavior, peripheral devices, and timing.
- **Video / Audio Output:** Converts emulated device output into frames and audio for the frontend.
- **Save States & Diagnostics:** Provides a conceptual place for state snapshots and runtime inspection.
