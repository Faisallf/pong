Pong Game für Zynq-7010 (Verilog)

Dieses Projekt implementiert das klassische Pong-Spiel vollständig in Verilog und läuft auf einem Zynq-7010 SoC Board (z. B. Zybo/ZedBoard).
Die Ausgabe erfolgt über VGA, inklusive Punkteanzeige, Labels und grundlegender Spielphysik.

⭐ Features

Pong-Spiel komplett in FPGA-Logik (kein ARM-Core notwendig)

VGA-Ausgabe (640×480 @ 60 Hz)

Ball-Physik + Kollisionen

Paddle-Physik für Spieler und NPC

Punkteanzeige (0–9), Doppelpunkte, Labels („PLAYER“, „BOT“, „WON“)

UI-Overlay als kombinierte Rendering-Stufe

Speicherdateien (.mem) für Ziffern und Labels

📁 Projektstruktur
constrs_1/
  new/
    const.xdc               → Pin- und Taktspezifikation

sources_1/
  new/
    ball_physik.v           → Ballbewegung & Kollision
    paddle_physik.v         → Paddle-Physik für Spieler
    paddle_npc.v            → Paddle-KI / NPC
    Punktestand_logik.v     → Inkrementierung & Reset der Punktzahl
    score_display.v         → Anzeige der Punktzahl aus .mem-Fonts
    ui_overlay.v            → Kombiniert Spielfläche + UI-Elemente
    vga.v                   → VGA-Timing (640×480 @ 60 Hz)
    vga_pong.v              → Haupt-VGA-Rendering für Spielfläche
    simplevga_top.v         → Top-Level-Modul des Projekts

  

utils_1/
imports/
synth_1/
  simplevga_top.dcp         → Synthese-Checkpoint

🛠 Voraussetzungen

Zynq-7010 SoC Board (z. B. Zybo, Cora, Arty Z7-10)

Vivado (getestet mit Version XX.X)

VGA-Monitor

25 MHz Pixeltakt (aus MMCM/PLL generiert)

▶️ Build & Ausführung

Projekt in Vivado importieren

simplevga_top.v als Top-Modul setzen

const.xdc einbinden (Pins + Takt definieren)

Synthese → Implementierung → Bitstream generieren

Bitstream auf das Board laden

VGA-Monitor anschließen

🎮 Steuerung

Spielerpaddle: über Buttons / Switches des Boards

NPC: automatische Paddle-Logik (paddle_npc.v)

Reset: dedizierter Reset-Button

Start: automatisch nach Reset

🖥 VGA-Signal

Das System erzeugt ein VGA-Timing mit:

Auflösung: 640×480 @ 60 Hz

Pixeltakt: 25.175 MHz (im Projekt auf 25 MHz gerundet)

HSYNC/VSYNC aus vga.v

RGB-Farbwerte aus UI-Overlay und Spiellogik

📘 Hinweise & Erweiterungen

Alle Spielfunktionen laufen in dedizierter Logik ohne Software.

Die .mem-Dateien definieren Pixelmaps für Ziffern und Labels.

Erweiterbar um Sound, Animationen, Menü oder SPI-Controller für externe Eingabegeräte.
