# Marlin 2.0.9.1 – Custom Firmware für Creality Ender 3 Pro

Diese Repository enthält eine angepasste **Marlin 2.0.9.1** Firmware, die speziell für den **Creality Ender 3 Pro** mit dem **v4.2.2 Mainboard** optimiert wurde. 

Die Basis für diese Konfiguration stammt aus dem Repository von [Christopher Kurtin](https://github.com/criskurtin/Marlin).

---

## 🛠️ Anpassungen & Features

Folgende Änderungen und Erweiterungen wurden in dieser Firmware aktiviert und konfiguriert:

*   **Creality BLTouch aktiviert:** Automatische Bettnivellierung (ABL) ist vollständig eingerichtet und einsatzbereit.
*   **BMG Extruder-Setup:** Die Extruder-Schritte wurden standardmäßig auf **415 mm/step** für den Bondtech BMG (oder kompatible Klone) angepasst (`DEFAULT_AXIS_STEPS_PER_UNIT`).
*   **Reduzierte Extruder-Beschleunigung:** Der Wert für `DEFAULT_MAX_ACCELERATION` des Extruders wurde auf **500** gesenkt, um das Filament-Fehlverhalten und Riemen-/Zahnradbelastungen zu minimieren.
*   **Filament-Wechsel aktiviert:** Unterstützt den automatischen oder manuellen Filamentwechsel während des Druckvorgangs.
*   **Advanced Pause Feature aktiviert:** Schaltet erweiterte Park- und Pausenfunktionen frei (`ADVANCED_PAUSE_FEATURE`), was unter anderem für den Filamentwechsel benötigt wird.
*   **Host Action Commands aktiv:** Ermöglicht eine bessere Kommunikation mit Host-Systemen wie **OctoPrint** oder **Klipper/Moonraker** (z. B. Pause/Fortsetzen-Meldungen direkt vom Drucker an den Server).
*   **Angepasste Bettgröße:** Die nutzbaren Druckbett-Dimensionen wurden präzise auf **X = 230 mm** und **Y = 220 mm** eingestellt (`X_BED_SIZE` / `Y_BED_SIZE`).

---

## 📦 Hardware-Voraussetzungen

*   **Drucker:** Creality Ender 3 Pro
*   **Mainboard:** Creality v4.2.2 (GD32F303)
*   **Sensor:** Creality CR-Touch
*   **Extruder:** BMG Dual-Drive Extruder (oder baugleich)

---

## 🚀 Installation (Fertige Firmware flashen)

Du musst die Firmware nicht selbst kompilieren. Die fertige Datei steht bereit:

1. Gehe rechts auf der GitHub-Seite auf den Reiter **Releases**.
2. Lade dir dort die aktuellste **`firmware.bin`** herunter.
3. Nimm eine leere, im Format **FAT32** formatierte MicroSD-Karte.
4. Kopiere die heruntergeladene `firmware.bin` direkt auf die Karte (in keinen Unterordner!).
5. Schalte deinen Ender 3 Pro aus.
6. Stecke die MicroSD-Karte in den Drucker.
7. Schalte den Drucker ein. Der Bildschirm bleibt für einige Sekunden dunkel, während das Board die Firmware flasht. Danach startet der Drucker wie gewohnt mit der neuen Firmware.

---

## 🚀 Kompilieren und Installieren

Zum Kompilieren dieser Firmware wird **Visual Studio Code** mit der Erweiterung **PlatformIO** empfohlen.

1. Lade dieses Repository als ZIP herunter oder klone es via Git:
   ```bash
   git clone https://github.com
   ```
2. Öffne den Ordner in VS Code.
3. Wähle die passende Umgebung für das v4.2.2 Board aus (z. B. `STM32F103RET6_creality` oder die für deinen Chip entsprechende Umgebung).
4. Klicke auf **Build**, um die `firmware.bin` zu erstellen.
5. Kopiere die generierte `firmware.bin` auf eine leere, FAT32-formatierte MicroSD-Karte.
6. Stecke die Karte in den ausgeschalteten Drucker und schalte ihn ein. Der Flash-Vorgang startet automatisch.

---

## 📜 Credits
*   Original Marlin-Projekt: [MarlinFirmware](https://github.com)
*   Basis-Konfiguration: [criskurtin/Marlin](https://github.com/criskurtin/Marlin)

---
*Hinweis: Die Nutzung dieser Firmware erfolgt auf eigene Gefahr. Bitte überprüfe vor dem ersten Homing die Achsenrichtungen und den Abstand des BLTouch-Sensors zur Düse (Z-Offset).*
