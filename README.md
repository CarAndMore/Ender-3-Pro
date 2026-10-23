# Marlin 2.0.9.1 – Custom Firmware für den Creality Ender 3 Pro

Dieses Repository enthält eine angepasste **Marlin 2.0.9.1** Firmware für den **Creality Ender 3 Pro** mit **v4.2.2 Mainboard (GD32F303)**, CR-Touch und BMG-Extruder konfiguriert.

Die ursprüngliche Basis dieser Konfiguration stammt aus dem Repository von [Christopher Kurtin](https://github.com/criskurtin/Marlin).

---

## 🛠️ Anpassungen & Features

Folgende Funktionen und Optimierungen sind bereits aktiviert bzw. vorkonfiguriert:

### ✅ CR-Touch / BLTouch aktiviert
Automatische Bettnivellierung (ABL) ist vollständig eingerichtet und einsatzbereit.

### ✅ BMG-Extruder vorkonfiguriert
Die Extruder-Schritte wurden auf **415 Steps/mm** angepasst (`DEFAULT_AXIS_STEPS_PER_UNIT`) und sind für Bondtech BMG Extruder sowie kompatible Klone ausgelegt.

### ✅ Reduzierte Extruder-Beschleunigung
Die maximale Extruder-Beschleunigung wurde auf **500 mm/s²** reduziert, um unnötige Belastungen von Filament, Extruder und Zahnradmechanik zu vermeiden.

### ✅ Filamentwechsel aktiviert
Unterstützung für automatischen und manuellen Filamentwechsel während des Drucks.

### ✅ PID-Autotuning aktiviert
PID-Werte für Hotend und Heizbett können direkt per G-Code neu eingemessen werden.

### ✅ Advanced Pause Feature aktiviert
Erweiterte Pausen-, Park- und Filamentwechsel-Funktionen (`ADVANCED_PAUSE_FEATURE`) sind aktiviert.

### ✅ Host Action Commands aktiviert
Verbesserte Kommunikation mit Host-Systemen wie **OctoPrint**. Unterstützt Status-, Pausen- und Fortsetzen-Meldungen direkt vom Drucker an den Host.

### ✅ Angepasste Druckbettgröße
Die nutzbare Druckfläche wurde auf **230 × 220 mm** eingestellt.

---

## 📦 Hardware-Voraussetzungen

- **Drucker:** Creality Ender 3 Pro
- **Mainboard:** Creality v4.2.2 (GD32F303)
- **Sensor:** CR-Touch oder BLTouch
- **Extruder:** BMG Dual-Drive Extruder (oder kompatibler Klon)

---

## 🚀 Installation (Fertige Firmware flashen)

Eine eigene Kompilierung ist nicht notwendig.

1. Öffne den Bereich **Releases** auf GitHub.
2. Lade die aktuelle Datei `firmware-xxxx.bin` herunter.
3. Verwende eine leere, mit **FAT32** formatierte MicroSD-Karte.
4. **Wichtig für GD32-Boards:** Benenne die Firmware-Datei vor dem Flashen um (z. B. `Marlin_BMG_v1.bin` oder `firmware_20261023.bin`). Bereits verwendete Dateinamen werden vom Bootloader teilweise ignoriert.
5. Kopiere die umbenannte Datei direkt in das Hauptverzeichnis der SD-Karte.
6. Schalte den Drucker aus.
7. Stecke die SD-Karte ein.
8. Schalte den Drucker wieder ein. Während des Flash-Vorgangs bleibt das Display für einige Sekunden leer. Anschließend startet der Drucker automatisch neu.

### EEPROM zurücksetzen (erforderlich)

Nach dem ersten Start sollten die neuen Standardwerte aus der Firmware ins EEPROM übernommen werden:

1. **Configuration → Restore Defaults**
2. **Configuration → Store Settings**

Dadurch werden alte Einstellungen entfernt und alle in der Firmware hinterlegten Werte übernommen.

### Z-Offset einstellen

1. Führe zunächst ein **Auto Home** aus.
2. Stelle anschließend unter **Configuration → Probe Z-Offset** den korrekten Düsenabstand ein.
3. Speichere den Wert mit **Store Settings** dauerhaft im EEPROM.

---

## 🔨 Firmware selbst kompilieren

Zum Kompilieren wird **Visual Studio Code** mit den Erweiterungen **PlatformIO** und **Auto Build Marlin** empfohlen.

1. Repository klonen oder als ZIP herunterladen.
2. Das Projekt in Visual Studio Code öffnen.
3. Gewünschte Anpassungen in `Configuration.h` und `Configuration_adv.h` vornehmen.
4. Die Firmware über **Auto Build Marlin** oder **PlatformIO** erstellen.
5. Die erzeugte `.bin`-Datei aus `.pio/build/...` auf eine FAT32-formatierte MicroSD-Karte kopieren.
6. Die Datei vor dem Flashen umbenennen (siehe Hinweis zu GD32-Boards).
7. Die Firmware wie oben beschrieben flashen.

### Nach dem Flashen

#### EEPROM zurücksetzen

1. **Configuration → Restore Defaults**
2. **Configuration → Store Settings**

Dadurch werden die in der Firmware hinterlegten Standardwerte übernommen.

#### Z-Offset einstellen

1. **Auto Home** ausführen.
2. **Probe Z-Offset** einstellen.
3. Mit **Store Settings** speichern.

---

## 💡 Nützliche G-Code-Befehle

### PID-Autotuning

#### Hotend (200 °C)

```gcode
M303 E0 S200 C8 U1
```

#### Heizbett (70 °C)

```gcode
M303 E-1 S70 C8 U1
```

Anschließend die ermittelten Werte dauerhaft speichern:

```gcode
M500
```

---

## 🎛️ Advanced Pause Feature

| Funktion | G-Code |
|-----------|---------|
| Filamentwechsel | `M600` |
| Filament laden | `M701` |
| Filament entladen | `M702` |
| Druck pausieren und Druckkopf parken | `M125` |
| Pause abbrechen / fortsetzen | `M108` |

---

## 📋 Wichtige Firmware-Werte

| Einstellung | Wert |
|------------|------|
| Druckbett X | 230 mm |
| Druckbett Y | 220 mm |
| Extruder Steps/mm | 415 |
| Extruder Max Acceleration | 500 mm/s² |
| Auto Bed Leveling | Aktiv |
| Advanced Pause | Aktiv |
| Host Action Commands | Aktiv |
| PID Autotune | Aktiv |

---

## 📜 Credits

- Originales Marlin-Projekt: https://github.com/MarlinFirmware/Marlin
- Basis-Konfiguration: https://github.com/criskurtin/Marlin

---

## ⚠️ Haftungsausschluss

Die Nutzung dieser Firmware erfolgt auf eigene Verantwortung.

Vor dem ersten Homing sollten folgende Punkte überprüft werden:

- Achsenrichtungen
- Endstop-Funktion
- CR-Touch-Funktion
- Z-Offset

Für Schäden an Hardware, Druckobjekten oder Folgeschäden wird keine Haftung übernommen.
