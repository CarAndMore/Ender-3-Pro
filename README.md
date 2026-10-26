# Marlin 2.0.9.1 – Custom Firmware für den Creality Ender 3 Pro 

 🇩🇪 **Dies ist die deutsche Dokumentation.** 
 
 🇬🇧 👉 For the English version, please view the [README_EN.md](.github/README_EN.md).
 
Dieses Repository enthält eine angepasste **Marlin 2.0.9.1** Firmware für den **Creality Ender 3 Pro** mit **v4.2.2 Mainboard (GigaDevice GD32F303-RET6)**, CR-Touch und BMG-Extruder.

Die ursprüngliche Basis dieser Konfiguration stammt aus dem Repository von [Christopher Kurtin](https://github.com/criskurtin/Marlin).

<p>
<img src=".github/img/mainboard.png" width="40%" alt="Creality V4.2.2 Mainboard" />
<img src=".github/img/gd_cpu.png" width="34%" alt="GigaDevice CPU" />
</p>
---

## 🛠️ Anpassungen & Features

Folgende Funktionen und Optimierungen sind bereits aktiviert bzw. vorkonfiguriert:


### ✅ CR-Touch / BLTouch aktiviert
Automatische Bettnivellierung (ABL) ist vollständig eingerichtet und einsatzbereit.

<br>

### ✅ Bett-Schrauben-Assistent aktiviert
Der **ASSISTED_TRAMMING_WIZARD** unterstützt das manuelle Ausrichten des Druckbetts. In Verbindung mit dem BLTouch werden die Positionen über den Bettschrauben automatisch angefahren und vermessen. Der Assistent zeigt anschließend die notwendigen Korrekturen zum exakten Trammen des Druckbetts an.

<br>

### ✅ BMG-Extruder vorkonfiguriert
Die Extruder-Schritte wurden auf **415 Steps/mm** angepasst (`DEFAULT_AXIS_STEPS_PER_UNIT`) und sind für Bondtech BMG Extruder sowie kompatible Klone ausgelegt.

<br>

### ✅ Linear Advance aktiviert
**Linear Advance** (`LIN_ADVANCE`) ist aktiviert und kann bequem über den G-Code `M900` konfiguriert werden. Dadurch wird der Materialfluss insbesondere bei Beschleunigungs- und Richtungswechseln deutlich präziser geregelt.

<br>

### ✅ Reduzierte Extruder-Beschleunigung
Die maximale Extruder-Beschleunigung wurde auf **500 mm/s²** reduziert, um unnötige Belastungen von Filament, Extruder und Zahnradmechanik zu vermeiden.

<br>

### ✅ Filamentwechsel aktiviert
Unterstützung für automatischen und manuellen Filamentwechsel während des Drucks oder direkt über das LCD-Menü im Idle-Betrieb.

<br>

### ✅ PID-Autotuning aktiviert
PID-Werte für Hotend und Heizbett können direkt per G-Code oder im LCD-Menü neu eingemessen werden.

<br>

### ✅ SKEW_CORRECTION (Rechtwinkligkeits-Korrektur) aktiviert
Diese Funktion korrigiert geometrische Fehlstellungen (Schieflagen) zwischen den XY-Achsen Ihres 3D-Druckers. Wenn Ihre Achsen nicht perfekt im 90°-Winkel zueinander stehen, gleicht diese Software-Funktion das aus, damit Ihre Drucke trotzdem rechtwinklig werden.

<br>

### ✅ Advanced Pause Feature aktiviert
Erweiterte Pausen-, Park- und Filamentwechsel-Funktionen (`ADVANCED_PAUSE_FEATURE`) sind aktiviert.

<br>

### ✅ Host Action Commands aktiviert
Verbesserte Kommunikation mit Host-Systemen wie **OctoPrint**. Unterstützt Status-, Pausen- und Fortsetzen-Meldungen direkt vom Drucker an den Host.

<br>

### ✅ Restzeitanzeige & Fortschrittsbalken aktiviert
Die LCD-Anzeige zeigt während des Drucks einen Fortschrittsbalken sowie die verbleibende Druckzeit an. Dadurch lässt sich der aktuelle Druckfortschritt jederzeit direkt am Drucker überwachen.

<br>

### ✅ Optimierte Vorheizprofile
Der veraltete Vorheiz-Eintrag **ABS** wurde durch **PETG** ersetzt.

Vorkonfigurierte Temperaturen:

| Material | Düse | Heizbett |
|-----------|-----------|-----------|
| PLA | 195°C | 60°C |
| PETG | 220°C | 75°C |

---

## 📦 Hardware-Voraussetzungen

- **Drucker:** Creality Ender 3 Pro
- **Mainboard:** Creality v4.2.2 (GD32F303-RET6) mit A4988-Schrittmotortreibern
- **LCD:** Original Creality LCD mit japanischem Zeichensatz
- **Sensor:** Creality CR-Touch oder BLTouch
- **Extruder:** BMG Dual-Drive Extruder (oder kompatibler Klon)

---

## 📦 Meine OctoPrint – Plugin-Liste

 - Bed Visualizer
 - Classic Webcam
 - Custom Control Manager
 - Druckerbenachrichtigungen
 - Exclude Region
 - File Check
 - Firmware Check
 - MultiCam
 - Octolapse
 - PrintTimeGenius
 - Printerdialoge
 - Slicer Thumbnails
 - Tuya Smartplug
 - UI Customizer

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

## 📐 Achsen-Rechtwinkligkeit & Skew-Kompensation

Falls die X- und Y-Achse deines Druckers nicht perfekt im 90°-Winkel zueinander stehen, führt das zu verzerrten (parallelogrammförmigen) Drucken. Um das nicht mühsam mechanisch auszurichten, kannst du den Schiefstand über die Firmware korrigieren.

Marlin berechnet den Faktor im Hintergrund nach dieser mathematischen Formel:

```text
Compute_AB = SQRT( 2 * AC * AC + 2 * BD * BD - 4 * AD * AD ) / 2
XY_SKEW_FACTOR : TAN( PI / 2 - ACOS (( AC * AC - AB * AB - AD * AD ) / (2 * AB * AD )))
```

Da die Formel etwas unhandlich ist, gibt es dafür jetzt einen interaktiven Online-Rechner:

👉 **Zum interaktiven** [Skew-Faktor-Rechner](https://carandmore.github.io/Ender-3-Pro/index.html).
### Kurzanleitung:
1. Drucke ein Testquadrat und miss die Diagonalen (**AC** und **BD**) sowie die Unterkante (**AD**).
2. Trage die Werte in den Rechner ein und klicke auf **Faktor berechnen**.
3. Sende den ermittelten Wert einfach per G-Code-Terminal (z. B. in OctoPrint oder Pronterface) an deinen Drucker:
   ```gcode
   M852 I[DEIN_BERECHNETER_WERT] ; z.b. M852 I0.000165
   M500 ; Einstellungen dauerhaft im EEPROM speichern
   ```
---

## 💡 Nützliche G-Code-Befehle

|> Die folgenden Befehle können über OctoPrint, Pronterface, Repetier-Host oder ein anderes Terminal direkt an den Drucker gesendet werden.

| Funktion | Befehl | Beispiel | Beschreibung |
|-----------|---------|---------|---------|
| Auto Home | `G28` | `G28` | Fährt alle Achsen (X, Y, Z) an ihre Endstopps und setzt die aktuelle Position als Referenz. |
| Automatische Bettnivellierung (ABL) | `G29` | `G29` | Startet das automatische Bed-Leveling mittels BLTouch/CR-Touch. |
| Bett-Schrauben-Assistent (Bed Tramming) | `G35` | `G35` | Vermisst die Positionen über den Bettschrauben und zeigt an, welche Schraube wie weit gedreht werden muss. |
| Düsentemperatur setzen | `M104` | `M104 S200` | Heizt die Düse auf 200 °C, ohne auf das Erreichen der Temperatur zu warten. |
| Düsentemperatur setzen und warten | `M109` | `M109 S200` | Heizt die Düse auf 200 °C und wartet, bis die Zieltemperatur erreicht ist. |
| Betttemperatur setzen | `M140` | `M140 S60` | Heizt das Druckbett auf 60 °C, ohne zu warten. |
| Betttemperatur setzen und warten | `M190` | `M190 S60` | Heizt das Druckbett auf 60 °C und wartet auf die Zieltemperatur. |
| Bauteillüfter einschalten | `M106` | `M106 S255` | Schaltet den Bauteillüfter ein. Wertebereich: 0–255. |
| Bauteillüfter ausschalten | `M107` | `M107` | Schaltet den Bauteillüfter vollständig aus. |
| Filamentwechsel | `M600` | `M600` | Pausiert den Druck und startet den Filamentwechsel-Assistenten. |
| Filament laden | `M701` | `M701` | Lädt Filament automatisch in den Extruder. |
| Filament entladen | `M702` | `M702` | Entlädt Filament automatisch aus dem Extruder. |
| Druck pausieren und parken | `M125` | `M125` | Pausiert den Druck und fährt den Druckkopf in eine Parkposition. |
| Pause fortsetzen | `M108` | `M108` | Bricht bestimmte Wartezustände ab bzw. setzt pausierte Vorgänge fort. |
| Steps/mm einstellen | `M92` | `M92 E415.0` | Setzt die Schritte pro Millimeter für Achsen oder Extruder. |
| Z-Offset einstellen | `M851` | `M851 Z-1.45` | Legt den Abstand zwischen Düse und Z-Sonde fest. |
| Skew Correction | `M852` | `M852 I0.000165` | Korrektur der Rechtswirklichkeit (X,Y). |
| Linear Advance K-Faktor | `M900` | `M900 K0.22` | Setzt den Linear-Advance-Wert für einen präziseren Materialfluss. Mit `M900` ohne Parameter wird der aktuelle Wert angezeigt. |
| PID-Autotune Hotend | `M303` | `M303 E0 S200 C8 U1` | Führt eine automatische PID-Kalibrierung des Hotends bei 200 °C durch. |
| PID-Autotune Heizbett | `M303` | `M303 E-1 S70 C8 U1` | Führt eine automatische PID-Kalibrierung des Heizbetts bei 70 °C durch. |
| Einstellungen speichern | `M500` | `M500` | Speichert alle aktuellen Einstellungen dauerhaft im EEPROM. |
| Einstellungen laden | `M501` | `M501` | Lädt die gespeicherten EEPROM-Werte in den RAM. |
| Werkseinstellungen laden | `M502` | `M502` | Lädt die Standardwerte aus der Firmware in den RAM. Danach mit `M500` speichern, falls dauerhaft gewünscht. |
| Einstellungen anzeigen | `M503` | `M503` | Gibt alle aktuell aktiven Einstellungen im Terminal aus. |
| EEPROM prüfen | `M504` | `M504` | Prüft das EEPROM auf Erreichbarkeit und korrekte Prüfsumme. |


- Nach Änderungen an M92, M851, M852, M900 oder PID-Werten immer mit M500 speichern.
- Anschließend mit M503 kontrollieren, ob die Werte korrekt übernommen wurden.
- Nach M502 sind die Firmware-Standardwerte nur im RAM geladen. Erst M500 schreibt sie dauerhaft ins EEPROM.

---

## 📋 Wichtige Firmware-Änderungen

| Einstellung | Wert |
|------------|------|
| Extruder Steps/mm | 415 |
| Extruder Max Acceleration | 500 mm/s² |
| Auto Bed Leveling (BLTouch / CR-Touch) | Aktiv |
| Sensor-Versatz (X, Y) | X: -43, Y: -9 |
| Z Endstopp | Deaktivirt |
| Z Safe Homing | Aktivirt |
| Leveling-Messraster | 5 x 5 (25 Punkte) | 
| Assisted Tramming Wizard | Aktivirt |
| Linear Advance | Aktivirt |
| Advanced Pause | Aktivirt |
| Host Action Commands | Aktivirt |
| PID Autotune | Aktivirt |
| Skew Correction | Aktivirt |
| Fortschrittsbalken | Aktivirt |
| Restzeitanzeige | Aktivirt |
| Filamentwechsel (M600) | Aktivirt |
| LCD-Menü Filament laden / entladen | Aktivirt |
| Vorheizprofil ABS | Durch PETG ersetzt |
| Vorheizprofil PLA | 195 °C / 60 °C |
| Vorheizprofil PETG | 220 °C / 75 °C |

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
