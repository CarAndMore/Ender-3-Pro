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
2. Lade dir dort die aktuellste **`firmware-xxxx.bin`**-Datei herunter.
3. Nimm eine leere, im Format **FAT32** formatierte MicroSD-Karte.
4. **WICHTIG FÜR DAS GD-BOARD:** Benenne die heruntergeladene Datei auf der Karte um (z. B. in `Marlin_BMG_v1.bin` oder füge das aktuelle Datum hinzu wie `firmware_241026.bin`). Das Creality-Board mit GD-Chip merkt sich alte Dateinamen und ignoriert das Update, wenn die Datei exakt so heißt wie beim letzten Flash-Vorgang! Kopiere die umbenannte Datei direkt auf die Karte (in keinen Unterordner!).
5. Schalte deinen Ender 3 Pro aus.
6. Stecke die MicroSD-Karte in den Drucker.
7. Schalte den Drucker ein. Der Bildschirm bleibt für einige Sekunden leer, während das Board die Firmware flasht. Danach startet der Drucker mit der neuen Firmware.
8. **ZVINGEND ERFORDERLICH – EEPROM BEREINIGEN:** Da alle perfekten BMG-Schritte, Filamentwege (300mm) und PLA/PETG-Temperaturen fest im Quellcode eingebacken sind, musst du nach dem ersten Start einmalig das EEPROM löschen. Das wirft alte „Werte-Leichen“ und falsche Einstellungen aus dem Speicher und lädt dein neues, sauberes Fundament. Gehe am Display auf **Configuration** -> **Restore Defaults** und klicke direkt danach auf **Store Settings**. Ab jetzt musst du die Filament- und Temperaturwerte nie wieder von Hand nachdrehen!
9. **Z-OFFSET EINSTELLEN:** Führe zuerst ein Homing (Auto Home) durch. Stelle danach deinen individuellen Düsenabstand im Display unter **Configuration** -> **Probe Z-Offset** ein und klicke anschließend erneut auf **Store Settings**, um den Wert dauerhaft zu sichern.

## 🚀 Kompilieren und Installieren

Zum Kompilieren dieser Firmware wird **Visual Studio Code** mit den Erweiterungen **PlatformIO** und **Auto Build Marlin** empfohlen.

1. Lade dieses Repository als ZIP herunter oder klone es via Git.
2. Öffne den heruntergeladenen Projektordner in **VS Code**. Stellen sicher, dass die Plugins *PlatformIO* und *Auto Build Marlin* aktiv sind.
3. Nimm deine gewünschten Anpassungen in den Dateien `Configuration.h` und `Configuration_adv.h` vor.
4. Klicke im *Auto Build Marlin*-Plugin (oder in PlatformIO) auf **Build**, um die Firmware zu erstellen.
5. Besorge eine leere MicroSD-Karte, die im Format **FAT32** formatiert ist.
6. Such auf deiner Festplatte im Projektordner unter `.pio/build/...` nach der frisch generierten `.bin`-Datei und kopiere sie direkt auf die MicroSD-Karte (in keinen Unterordner!).
7. **WICHTIG FÜR DAS GD-BOARD:** Benenne die Datei auf der Karte zwingend um (z. B. in `Marlin_BMG_v1.bin` oder füge das aktuelle Datum hinzu wie `firmware_2026_10.bin`). Das Creality-Board mit GD-Chip merkt sich bereits geflashte Dateinamen und ignoriert das Update komplett, wenn die Datei exakt so heißt wie beim letzten Mal!
8. Schalte deinen Ender 3 Pro aus und stecke die MicroSD-Karte in den Drucker.
9. Schalte den Drucker ein. Der Bildschirm bleibt für einige Sekunden leer, während das Board die Firmware flasht. Danach startet der Drucker mit der neuen Firmware.
10. **ZWINGEND ERFORDERLICH – EEPROM BEREINIGEN:** Da alle optimierten BMG-Schritte, Filamentwege (300mm) und PLA/PETG-Temperaturen fest im Quellcode eingebacken sind, musst du nach dem ersten Start einmalig das EEPROM löschen. Das wirft alte Einstellungs-Leichen aus dem Speicher und lädt dein neues, sauberes Fundament. Gehe am Display auf **Configuration** -> **Restore Defaults** und klicke direkt danach auf **Store Settings**. Ab jetzt musst du die Filament- und Temperaturwerte nie wieder von Hand nachdrehen!
11. **Z-OFFSET EINSTELLEN:** Führe am Drucker zuerst ein Homing (**Auto Home**) durch. Stelle danach deinen individuellen Düsenabstand im Display unter **Configuration** -> **Probe Z-Offset** ein und klicke anschließend erneut auf **Store Settings**, um den Wert dauerhaft im EEPROM zu sichern.

---

## 📜 Credits
*   Original Marlin-Projekt: [MarlinFirmware](https://github.com)
*   Basis-Konfiguration: [criskurtin/Marlin](https://github.com/criskurtin/Marlin)

---
*Hinweis: Die Nutzung dieser Firmware erfolgt auf eigene Gefahr. Bitte überprüfe vor dem ersten Homing die Achsenrichtungen und den Abstand des BLTouch-Sensors zur Düse (Z-Offset).*
