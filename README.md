# Box Packaging Plant

An automated box packaging line built and simulated in **OpenPLC Editor**, using ladder logic to control the fill, verify, seal, and discharge process for boxes on a production line.

## Overview

The system is controlled through 5 ladder logic rungs, each handling a specific stage of the packaging process:

### 1. Start_Stop_System
A safety-interlocked start/stop circuit.
- `Emergency_Stop_Button` and `Stop_Button` can shut the system down instantly.
- `Start_Button` engages the system, with a seal-in/latching branch so it stays running after the button is released.
- A 3-second `TON` (Timer On Delay) confirms the machine has started before activating the `LED` status indicator.

### 2. Motor1_Signal
Once the system is running (`LED` active) and both `Filling_Process` and `Linear_actuator` are idle, `Motor_1` runs — driving the main conveyor that moves boxes into the filling station.

### 3. Proximity_Sensor_Triggering_for_Filling_Process
When `P_Sensor` detects a box in position, a 10-second pulse timer (`TP`) activates `Filling_Process` — the timed window during which the box is filled.

### 4. Camera_Sensor_To_Verify_Packaging
`C_Sensor` (camera) verifies the box is `Semi_Filled`, then triggers a 5-second pulse on the `Linear_actuator` — sealing or advancing the box to the next stage.

### 5. Motor2_Signal
Once the `Linear_actuator` fires, it triggers `Motor_2` via another pulse timer, moving the sealed box off the line to the output conveyor.

## Project Structure

```
Box Packaging Plant/
├── devices/       # Device configuration and pin mapping
├── pous/          # Program Organization Units (ladder logic)
├── media/         # Demo video of the working project
├── project.json   # Main OpenPLC project file
└── README.md
```

## Demo Video

A working demo of the full packaging cycle is available in the `media/` folder: `Box Packaging Plant.mp4`

## Tools Used

- [OpenPLC Editor](https://autonomylogic.com/) — used for PLC programming (ladder logic)

## How to Open

1. Install [OpenPLC Editor](https://autonomylogic.com/).
2. Clone this repository.
3. Open `project.json` in OpenPLC Editor to view and run the ladder logic.
