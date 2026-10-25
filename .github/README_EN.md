# Marlin 2.0.9.1 – Custom Firmware for the Creality Ender 3 Pro

 🇩🇪 👉 Für die deutsche Version, bitte die [README.md](../README.md) anzeigen.
 
 🇬🇧 **This is the English documentation.**
 
This repository contains a customized **Marlin 2.0.9.1** firmware for the **Creality Ender 3 Pro** featuring a **v4.2.2 mainboard (GD32F303-RET6)**, CR-Touch, and BMG extruder.

The original foundation of this configuration comes from the repository by [Christopher Kurtin](https://github.com).

<img src="img/mainboard.png" width="45%" alt="Creality V4.2.2 Mainboard" />
---

## 🛠️ Customizations & Features

The following functions and optimizations are already enabled or preconfigured:


### ✅ CR-Touch / BLTouch Enabled
Automatic Bed Leveling (ABL) is fully set up and ready to use.

<br>

### ✅ Bed Screws Wizard Enabled
The **ASSISTED_TRAMMING_WIZARD** assists with manual bed leveling. In combination with the BLTouch, the positions directly above the bed screws are automatically approached and measured. The wizard then displays the exact adjustments needed to tram the print bed perfectly.

<br>

### ✅ BMG Extruder Preconfigured
The extruder steps have been adjusted to **415 steps/mm** (`DEFAULT_AXIS_STEPS_PER_UNIT`) and are tailored for Bondtech BMG extruders as well as compatible clones.

<br>

### ✅ Linear Advance Enabled
**Linear Advance** (`LIN_ADVANCE`) is enabled and can be easily configured using the G-code `M900`. This ensures much more precise control over the material flow, especially during acceleration and direction changes.

<br>

### ✅ Reduced Extruder Acceleration
The maximum extruder acceleration has been reduced to **500 mm/s²** to prevent unnecessary stress on the filament, extruder, and gear mechanism.

<br>

### ✅ Filament Change Enabled
Support for automatic and manual filament changes during printing, or directly via the LCD menu while idling.

<br>

### ✅ PID Autotuning Enabled
PID values for both the hotend and heated bed can be recalibrated directly via G-code or through the LCD menu.

<br>

### ✅ Advanced Pause Feature Enabled
Extended pause, park, and filament change functionalities (`ADVANCED_PAUSE_FEATURE`) are fully enabled.

<br>

### ✅ Host Action Commands Enabled
Improved communication with host systems such as **OctoPrint**. Supports status, pause, and resume messages sent directly from the printer to the host.

<br>

### ✅ Remaining Time Display & Progress Bar Enabled
The LCD screen displays a progress bar and the remaining print time during a print job. This allows you to monitor the current print progress directly on the printer at any time.

<br>

### ✅ Optimized Preheat Profiles
The outdated **ABS** preheat profile has been replaced with **PETG**.

Preconfigured temperatures:

| Material | Nozzle | Heated Bed |
|-----------|-----------|-----------|
| PLA | 195°C | 60°C |
| PETG | 220°C | 75°C |

<br>

### ✅ Adjusted Print Bed Size
The usable print area has been set to **230 × 220 mm**.

---

## 📦 Hardware Requirements

- **Printer:** Creality Ender 3 Pro
- **Mainboard:** Creality v4.2.2 (GD32F303-RET6) with A4988 stepper motor drivers
- **LCD:** Original Creality LCD with Japanese charset
- **Sensor:** Creality CR-Touch or BLTouch
- **Extruder:** BMG Dual-Drive Extruder (or compatible clone)

---

## 🚀 Installation (Flashing Pre-compiled Firmware)

Compiling the code yourself is not required.

1. Open the **Releases** section on GitHub.
2. Download the latest `firmware-xxxx.bin` file.
3. Use an empty MicroSD card formatted to **FAT32**.
4. **Important for GD32 boards:** Rename the firmware file before flashing (e.g., `Marlin_BMG_v1.bin` or `firmware_20261023.bin`). Previously used filenames are sometimes ignored by the bootloader.
5. Copy the renamed file directly into the root directory of the SD card.
6. Turn off the printer.
7. Insert the MicroSD card.
8. Turn the printer back on. The display will remain blank for a few seconds during the flashing process. After that, the printer will automatically restart.

### Resetting the EEPROM (Required)

After the first boot, the new default values from the firmware must be saved to the EEPROM:

1. **Configuration → Restore Defaults**
2. **Configuration → Store Settings**

This removes old configurations and applies all default values stored in the firmware.

### Setting the Z-Offset

1. First, perform an **Auto Home**.
2. Next, adjust the correct nozzle distance under **Configuration → Probe Z-Offset**.
3. Permanently save the value to the EEPROM using **Store Settings**.

---

## 🔨 Compiling Firmware Yourself

For compiling, **Visual Studio Code** with the extensions **PlatformIO** and **Auto Build Marlin** is highly recommended.

1. Clone the repository or download it as a ZIP file.
2. Open the project folder in Visual Studio Code.
3. Make your desired adjustments in `Configuration.h` and `Configuration_adv.h`.
4. Build the firmware using **Auto Build Marlin** or **PlatformIO**.
5. Copy the generated `.bin` file from `.pio/build/...` onto a FAT32-formatted MicroSD card.
6. Rename the file before flashing (see the note regarding GD32 boards).
7. Flash the firmware as described in the installation steps above.

### After Flashing

#### Resetting the EEPROM

1. **Configuration → Restore Defaults**
2. **Configuration → Store Settings**

This applies the default values configured within the firmware.

#### Setting the Z-Offset

1. Run an **Auto Home**.
2. Adjust your **Probe Z-Offset**.
3. Save your changes with **Store Settings**.

---

## 💡 Useful G-Code Commands

|> The following commands can be sent directly to the printer via OctoPrint, Pronterface, Repetier-Host, or any other terminal console.

| Function | Command | Example | Description |
|-----------|---------|---------|---------|
| Auto Home | `G28` | `G28` | Homes all axes (X, Y, Z) and sets the current position as the reference point. |
| Automatic Bed Leveling (ABL) | `G29` | `G29` | Starts automatic bed leveling using the BLTouch/CR-Touch. |
| Bed Screws Wizard (Bed Tramming) | `G35` | `G35` | Measures positions above the bed screws and indicates how far to turn each screw. |
| Set Nozzle Temperature | `M104` | `M104 S200` | Heats the nozzle to 200°C without waiting for the temperature to be reached. |
| Set Nozzle Temp and Wait | `M109` | `M109 S200` | Heats the nozzle to 200°C and pauses execution until the target temperature is reached. |
| Set Bed Temperature | `M140` | `M140 S60` | Heats the heated bed to 60°C without waiting. |
| Set Bed Temp and Wait | `M190` | `M190 S60` | Heats the heated bed to 60°C and pauses execution until the target temperature is reached. |
| Turn On Part Cooling Fan | `M106` | `M106 S255` | Turns on the part cooling fan. Value range: 0–255. |
| Turn Off Part Cooling Fan | `M107` | `M107` | Completely turns off the part cooling fan. |
| Filament Change | `M600` | `M600` | Pauses the print and initiates the filament change wizard. |
| Load Filament | `M701` | `M701` | Automatically loads filament into the extruder. |
| Unload Filament | `M702` | `M702` | Automatically unloads filament from the extruder. |
| Pause Print and Park | `M125` | `M125` | Pauses the print job and moves the print head to a designated park position. |
| Resume from Pause | `M108` | `M108` | Cancels certain wait states or resumes paused processes. |
| Set Steps/mm | `M92` | `M92 E415.0` | Sets the steps per millimeter for axes or the extruder. |
| Set Z-Offset | `M851` | `M851 Z-1.45` | Defines the distance between the nozzle and the Z probe. |
| Linear Advance K-Factor | `M900` | `M900 K0.22` | Sets the Linear Advance value for a more precise material flow. Running `M900` without parameters displays the current value. |
| PID Autotune Hotend | `M303` | `M303 E0 S200 C8 U1` | Runs an automatic PID calibration of the hotend at 200°C. |
| PID Autotune Heated Bed | `M303` | `M303 E-1 S70 C8 U1` | Runs an automatic PID calibration of the heated bed at 70°C. |
| Save Settings | `M500` | `M500` | Saves all current configuration settings permanently to the EEPROM. |
| Load Settings | `M501` | `M501` | Loads the saved EEPROM configurations back into RAM. |
| Restore Factory Defaults | `M502` | `M502` | Loads the factory default values from the firmware into RAM. Use `M500` afterwards if you want to save them permanently. |
| Report Settings | `M503` | `M503` | Outputs all currently active configuration settings to the terminal. |
| Validate EEPROM | `M504` | `M504` | Tests the EEPROM for accessibility and a correct checksum. |


- Always save your changes with M500 after modifying M92, M851, M900, or PID values.
- Verify that your values were successfully applied by running M503 afterwards.
- After running M502, the firmware defaults are only loaded into RAM. You must run M500 to write them permanently to the EEPROM.

---

## 📋 Key Firmware Values

| Setting | Value |
|------------|------|
| Print Bed X | 230 mm |
| Print Bed Y | 220 mm |
| Extruder Steps/mm | 415 |
| Extruder Max Acceleration | 500 mm/s² |
| Auto Bed Leveling (BLTouch / CR-Touch) | Enabled |
| Assisted Tramming Wizard | Enabled |
| Linear Advance | Enabled |
| Advanced Pause | Enabled |
| Host Action Commands | Enabled |
| PID Autotune | Enabled |
| Progress Bar | Enabled |
| Remaining Time Display | Enabled |
| Filament Change (M600) | Enabled |
| LCD Menu Load / Unload Filament | Enabled |
| Preheat Profile ABS | Replaced with PETG |
| Preheat Profile PLA | 195 °C / 60 °C |
| Preheat Profile PETG | 220 °C / 75 °C |

---

## 📜 Credits

- Original Marlin Project: https://github.com
- Base Configuration: https://github.com

---

## ⚠️ Disclaimer

Using this firmware is done entirely at your own risk.

Before performing the first homing routine, please verify the following points:

- Axis movement directions
- Endstop functionality
- CR-Touch functionality
- Z-Offset

No liability is accepted for any damage to hardware, printed objects, or subsequent damages.
