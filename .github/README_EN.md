# Marlin 2.0.9.1 – Custom Firmware for the Creality Ender 3 Pro

***
*Note: These information texts were created with the help of artificial intelligence (AI).*
***
 🇩🇪 👉 Für die deutsche Version, bitte die [README.md](../README.md) aufrufen.
 
 🇬🇧 **This is the English documentation.**
 
This repository contains a customized **Marlin 2.0.9.1** firmware for the **Creality Ender 3 Pro** with a **v4.2.2 Mainboard (GigaDevice GD32F303-RET6)**, CR-Touch, and BMG Extruder.

The original base of this configuration originates from the repository of [Christopher Kurtin](https://github.com/criskurtin/Marlin).

<p>
<img src="img/mainboard.png" width="40%" alt="Creality V4.2.2 Mainboard" />
<img src="img/gd_cpu.png" width="34%" alt="GigaDevice CPU" />
</p>
---

## 🛠️ Customizations & Features

The following functions and optimizations are already activated or preconfigured:

### ✅ CR-Touch / BLTouch Enabled
Automatic Bed Leveling (ABL) is fully set up and ready to use.

<br>

### ✅ Bed Tramming Wizard Enabled
The **ASSISTED_TRAMMING_WIZARD** supports the manual alignment of the print bed. In combination with the BLTouch, the positions above the bed screws are approached and measured automatically. The wizard then displays the necessary corrections for exact tramming of the print bed.

<br>

### ✅ BMG Extruder Preconfigured
The extruder steps have been adjusted to **415 Steps/mm** (`DEFAULT_AXIS_STEPS_PER_UNIT`) and are designed for Bondtech BMG Extruders as well as compatible clones.

<br>

### ✅ Linear Advance Enabled
**Linear Advance** (`LIN_ADVANCE`) is enabled and can be easily configured via G-code `M900`. This regulates the material flow much more precisely, especially during acceleration and direction changes.

<br>

### ✅ Reduced Extruder Acceleration
The maximum extruder acceleration has been reduced to **500 mm/s²** to prevent unnecessary stress on the filament, extruder, and gear mechanics.

<br>

### ✅ Filament Change Enabled
Support for automatic and manual filament changes during printing or directly via the LCD menu in idle mode.

<br>

### ✅ PID Autotuning Enabled
PID values for the hotend and heated bed can be re-measured directly via G-code or within the LCD menu.

<br>

### ✅ SKEW_CORRECTION (Squareness Correction) Enabled
This function corrects geometric misalignments (skew) between the XY axes of your 3D printer. If your axes are not at a perfect 90° angle to each other, this software function compensates for it so that your prints still turn out perfectly square.

<br>

### ✅ Advanced Pause Feature Enabled
Extended pause, park, and filament change functions (`ADVANCED_PAUSE_FEATURE`) are enabled.

<br>

### ✅ Host Action Commands Enabled
Improved communication with host systems like **OctoPrint**. Supports status, pause, and resume messages directly from the printer to the host.

<br>

### ✅ Remaining Time Display & Progress Bar Enabled
The LCD display shows a progress bar and the remaining print time during the print. This allows the current print progress to be monitored directly on the printer at any time.

<br>

### ✅ Optimized Preheat Profiles
The outdated preheat entry **ABS** has been replaced by **PETG**.

Preconfigured temperatures:

| Material | Nozzle | Heated Bed |
|-----------|-----------|-----------|
| PLA | 195°C | 60°C |
| PETG | 220°C | 75°C |

---

## 📦 Hardware Requirements

- **Printer:** Creality Ender 3 Pro
- **Mainboard:** Creality v4.2.2 (GD32F303-RET6) with A4988 stepper motor drivers
- **LCD:** Original Creality LCD with Japanese font set
- **Sensor:** Creality CR-Touch or BLTouch
- **Extruder:** BMG Dual-Drive Extruder (or compatible clone)

---

## 📦 My OctoPrint – Plugin List

 - Bed Visualizer
 - Classic Webcam
 - Custom Control Manager
 - Printer Notifications
 - Exclude Region
 - File Check
 - Firmware Check
 - MultiCam
 - Octolapse
 - PrintTimeGenius
 - Printer Dialogs
 - Slicer Thumbnails
 - Tuya Smartplug
 - UI Customizer

---

## 🚀 Installation (Flashing Precompiled Firmware)

Compiling it yourself is not necessary.

1. Open the **Releases** section on GitHub.
2. Download the current `firmware-xxxx.bin` file.
3. Use an empty MicroSD card formatted to **FAT32**.
4. **Important for GD32 boards:** Rename the firmware file before flashing (e.g., `Marlin_BMG_v1.bin` or `firmware_20261023.bin`). File names that have already been used are sometimes ignored by the bootloader.
5. Copy the renamed file directly into the root directory of the SD card.
6. Turn off the printer.
7. Insert the MicroSD card.
8. Turn the printer back on. During the flashing process, the display will remain blank for a few seconds. Afterwards, the printer restarts automatically.

### Reset EEPROM (Required)

After the first boot, the new default values from the firmware should be written to the EEPROM:

1. **Configuration → Restore Defaults**
2. **Configuration → Store Settings**

This removes old settings and applies all values stored in the firmware.

### Adjust Z-Offset

1. First, perform an **Auto Home**.
2. Then, set the correct nozzle distance under **Configuration → Probe Z-Offset**.
3. Save the value permanently in the EEPROM with **Store Settings**.

---

## 🔨 Compiling Firmware Yourself

For compiling, **Visual Studio Code** with the extensions **PlatformIO** and **Auto Build Marlin** is recommended.

1. Clone the repository or download it as a ZIP.
2. Open the project in Visual Studio Code.
3. Make the desired adjustments in `Configuration.h` and `Configuration_adv.h`.
4. Build the firmware via **Auto Build Marlin** or **PlatformIO**.
5. Copy the generated `.bin` file from `.pio/build/...` onto a FAT32-formatted MicroSD card.
6. Rename the file before flashing (see note regarding GD32 boards).
7. Flash the firmware as described above.

### After Flashing

#### Reset EEPROM

1. **Configuration → Restore Defaults**
2. **Configuration → Store Settings**

This ensures the default values stored in the firmware are applied.

#### Adjust Z-Offset

1. Execute **Auto Home**.
2. Adjust **Probe Z-Offset**.
3. Save with **Store Settings**.

---

## 📐 Axis Squareness & Skew Compensation

If the X and Y axes of your printer are not at a perfect 90° angle to each other, this leads to distorted (parallelogram-shaped) prints. To avoid having to realign this mechanically with great effort, you can correct the skew via the firmware.

Marlin calculates the factor in the background according to this mathematical formula:

```text
Compute_AB = SQRT( 2 * AC * AC + 2 * BD * BD - 4 * AD * AD ) / 2
XY_SKEW_FACTOR : TAN( PI / 2 - ACOS (( AC * AC - AB * AB - AD * AD ) / (2 * AB * AD )))
```

Since the formula is somewhat unwieldy, there is now an interactive online calculator for it:

👉 **To the interactive** [Skew Factor Calculator](https://carandmore.github.io/Ender-3-Pro/xy_calc.html).

### Quick Guide:
1. **Important before printing:** If a factor is already active, reset it in the terminal with `M852 I0` so that the test print shows the pure mechanical reality.
2. Print a test square and measure the diagonals (**AC** and **BD**) as well as the bottom edge (**AD**).
   e.g., [XY Skew Calibration Print](https://www.printables.com/model/535224-ultra-fast-printing-easy-measure-xy-skew-calibrati/files) by Maker64
3. Enter the values into the calculator and click **Calculate Factor**.
4. Simply send the determined value via a G-code terminal (e.g., in OctoPrint or Pronterface) to your printer:
   ```gcode
   M852 I[YOUR_CALCULATED_VALUE] ; e.g., M852 I0.000165
   M500 ; Permanently save settings in EEPROM
   ```
---

## 💡 Useful G-Code Commands

|> The following commands can be sent directly to the printer via OctoPrint, Pronterface, Repetier-Host, or any other terminal.

| Function | Command | Example | Description |
|-----------|---------|---------|-------------|
| Auto Home | `G28` | `G28` | Homes all axes (X, Y, Z) to their endstops and sets the current position as a reference. |
| Automatic Bed Leveling (ABL) | `G29` | `G29` | Starts automatic bed leveling using the BLTouch/CR-Touch. |
| Bed Tramming Wizard | `G35` | `G35` | Measures the positions above the bed screws and shows which screw needs to be turned and by how much. |
| Set Nozzle Temperature | `M104` | `M104 S200` | Heats the nozzle to 200°C without waiting for the temperature to be reached. |
| Set Nozzle Temp and Wait | `M109` | `M109 S200` | Heats the nozzle to 200°C and waits until the target temperature is reached. |
| Set Bed Temperature | `M140` | `M140 S60` | Heats the print bed to 60°C without waiting. |
| Set Bed Temp and Wait | `M190` | `M190 S60` | Heats the print bed to 60°C and waits for the target temperature. |
| Turn On Part Cooling Fan | `M106` | `M106 S255` | Turns on the part cooling fan. Value range: 0–255. |
| Turn Off Part Cooling Fan | `M107` | `M107` | Turns the part cooling fan completely off. |
| Filament Change | `M600` | `M600` | Pauses the print and starts the filament change assistant. |
| Load Filament | `M701` | `M701` | Automatically loads filament into the extruder. |
| Unload Filament | `M702` | `M702` | Automatically unloads filament from the extruder. |
| Pause Print and Park | `M125` | `M125` | Pauses the print and moves the print head to a parking position. |
| Resume Pause | `M108` | `M108` | Cancels certain wait states or resumes paused processes. |
| Set Steps/mm | `M92` | `M92 E415.0` | Sets the steps per millimeter for axes or the extruder. |
| Set Z-Offset | `M851` | `M851 Z-1.45` | Defines the distance between the nozzle and the Z-probe. |
| Skew Correction | `M852` | `M852 I0.000165` | Adjusts the squareness correction (X,Y). |
| Linear Advance K-Factor | `M900` | `M900 K0.22` | Sets the Linear Advance value for a more precise material flow. Running `M900` without parameters displays the current value. |
| PID Autotune Hotend | `M303` | `M303 E0 S200 C8 U1` | Performs an automatic PID calibration of the hotend at 200°C. |
| PID Autotune Heated Bed | `M303` | `M303 E-1 S70 C8 U1` | Performs an automatic PID calibration of the heated bed at 70°C. |
| Save Settings | `M500` | `M500` | Permanently saves all current settings in the EEPROM. |
| Load Settings | `M501` | `M501` | Loads the saved EEPROM values into RAM. |
| Restore Factory Defaults | `M502` | `M502` | Loads the default values from the firmware into RAM. Save with `M500` afterwards if desired permanently. |
| Display Settings | `M503` | `M503` | Outputs all currently active settings in the terminal. |
| Validate EEPROM | `M504` | `M504` | Checks the EEPROM for accessibility and a correct checksum. |

- Always save with `M500` after making changes to `M92`, `M851`, `M852`, `M900`, or PID values.
- Afterwards, verify with `M503` whether the values were correctly applied.
- After running `M502`, the firmware default values are only loaded into RAM. Only `M500` writes them permanently to the EEPROM.

---

## 📋 Important Firmware Configuration

| Setting | Value |
|------------|------|
| Extruder Steps/mm | 415 |
| Extruder Max Acceleration | 500 mm/s² |
| Auto Bed Leveling (BLTouch / CR-Touch) | Active |
| Sensor Offset (X, Y) | X: -43, Y: -9 |
| Z Endstop | Disabled |
| Z Safe Homing | Enabled |
| Leveling Grid | 5 x 5 (25 points) | 
| Assisted Tramming Wizard | Enabled |
| Linear Advance | Active |
| Advanced Pause | Active |
| Host Action Commands | Active |
| PID Autotune | Active |
| Skew Correction | Active |
| Progress Bar | Enabled |
| Remaining Time Display | Enabled |
| Filament Change (M600) | Active |
| LCD Menu Filament Load / Unload | Active |
| Preheat Profile ABS | Replaced by PETG |
| Preheat Profile PLA | 195 °C / 60 °C |
| Preheat Profile PETG | 220 °C / 75 °C |

---

## 📜 Credits

- Original Marlin Project: https://github.com/MarlinFirmware/Marlin
- Base Configuration: https://github.com/criskurtin/Marlin

---

## ⚠️ Disclaimer

The use of this firmware is at your own risk.

Before performing the first homing, the following points should be verified:

- Axis directions
- Endstop functionality
- CR-Touch / BLTouch functionality
- Z-Offset

No liability is assumed for damage to hardware, printed objects, or any consequential damages.

***

*Note: These information texts were created with the help of artificial intelligence (AI).*
