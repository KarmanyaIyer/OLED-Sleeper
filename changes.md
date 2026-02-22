# OLED Sleeper Changes Document

## Safety Check
The repository contains script files (`.ahk` and `.ps1`) which interact with provided execution tools for monitors natively, without internet connections or suspicious file interactions. Thus, it was determined safe to modify and use.

## Changes Made
1. **Idle Timer Input (Minutes to Milliseconds)**: Modifed `src/Configure.ps1` to accept user input in milliseconds directly, removing the minute-to-millisecond conversion.
2. **Dimming and Brightening Speed-up**: Updated `src/OLED-Sleeper.ahk` to execute brightness adjustments via the external tool `ControlMyMonitor.exe` using `Run` instead of `RunWait`. This avoids the script pausing its execution to await the external tool's return, making sequential adjustments or applying blackout overlays near instantaneous. 
3. **Sleeper Toggle Hotkey**: Implemented a global toggle hotkey (`Ctrl+Alt+S` using `^!s::`) inside `src/OLED-Sleeper.ahk`. When paused, it signals a pause, unhides the blackout overlay if present, and restores original brightness, acting as though activity was encountered. Upon resume, it resets the active times and restarts monitoring.

## Possible Edge Cases Addressed
- The hotkey toggle properly handles states for **both** the dim and blackout functions.
- The use of `Run` does not block monitor activity checks, ensuring faster responses but leaving brightness processes to handle themselves asynchronously.
- The AHK check `if isPaused` early-returns from the loop smoothly without polluting internal state.
