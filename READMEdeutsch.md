# Sovol-SV04-Klipper
Dieses Repository enthält alle notwendigen Konfigurationsdateien, damit der SV04 mit den 
Spiegel- und Kopiermodi von Klipper funktioniert.

![KlipperSV04](docs/img/sv04klipper.png)


# Spenden

[![Donate with PayPal](https://raw.githubusercontent.com/stefan-niedermann/paypal-donate-button/master/paypal-donate-button.png)](https://www.paypal.com/donate/?hosted_button_id=L85ULXXQKALP6)

# Neu
Hier klicken für [Discord](https://discord.gg/xBbKEvxRNq)

# Einleitung

Diese Anleitung beschreibt, wie du deinen SV04, inklusive der COPY und MIRROR Modi, mit 
Klipper ausrüsten kannst.

Der SV04 wurde mit verschiedenen Mainboards ausgeliefert, entweder mit einem STM32 oder 
einem Giga Device GD32. Für beide Boards sind die Konfigurationen in der Datei 
"printer.cfg", du musst nur den richtigen Abschnitt aktivieren. 
Als erstes solltet du überprüfen, welchen Chip du hast. Entweder du öffnest die 
Elekronikbox und schaut was auf deinem Chip steht oder du aktiviert eine Konfiguration, 
wenn es die falsche ist, gibt es eine Fehlermeldung beim z-Tilt.

# Update
Achtung, die Configs haben sich mit dem neuen Update geändert. Bitte füge IDEX_mode.cfg, 
Macros.cfg und Start-End-Macro.cfg erneut ein. 
Wenn das Display benötigt wird, befinden sich diese im Ordner 
[config/SV04-with-display](https://github.com/Bully85/Sovol-SV04-Klipper/tree/main/config/SV04-with-display)

Andernfalls kann bei installiertem Original-Klipper auch 
[config/SV04-works-with-orign-klipper](https://github.com/Bully85/Sovol-SV04-Klipper/tree/main/config/Sv04-works-with%20origin-klipper)
verwendet werden, jedoch ohne das Original-Display

Wechsle des Startcode im Slicer 
* [Cura](https://github.com/Bully85/Sovol-SV04-Klipper/tree/main/Cura%20Profile) 
* [Prusa_Slicer](https://github.com/Bully85/Sovol-SV04-Klipper/tree/main/Prusaslicer%20Profile)

# In Arbeit..
Momentan wird Cura 5.3 nicht untersützt ! wir arbeiten aber dran... 

# Was funktioniert alles?!!!

- Copy-Modus (unterstützt verschiedene Temperaturen, aber nicht die firstlayer Einstellungen für den rechten Extruder)
- Mirror-Modus (unterstützt verschiedene Temperaturen, aber nicht die firstlayer Einstellungen für den rechten Extruder)
- Dual Mode
- Single Mode
- Bed Mesh Levelling
- Input Shaper
- Das Display geht
- uvm.

# Benötigt
- Raspberry Pi mit W-Lan
    - Pi Zero funktioniert nicht
    - Pi2 kann funktionieren, oder auch nicht, deshalb nicht empfohlen
- Optional aber empfohlen: Original 7“ Touchscreen
- Optional: Kamera
- SSH; Zum Beispiel:
    - Powershell und Windows Terminal haben SSH integriert
    - alternativ Putty oder ein anderes SSH-Programm (https://putty.org/)
- SFTP oder SCP; Zum Beispiel:
    - FileZilla (https://filezilla-project.org/)
    - WinScp (https://winscp.net)
- Pi Imager (https://www.raspberrypi.com/software/)
- Die von mir erstellten Config Dateien
- MicroSD-Karte für den Raspi (mindestens 8GB, die komplette Installation beträgt etwa 5,5GB)
- SD-Karte zum Flashen des SV04 (maximal 8GB, formatiert in Fat32 4096)

# Installation

## Installation auf einem neuen Mainsail OS

Installiere mit dem Raspi Imager das Mainsail OS aus 'Other specific-purpose OS' -> 
'3D printing' -> 'Mainsail OS'.

Folge den Installationsschritten von  [Mainsail](https://docs-os.mainsail.xyz)

Die printer.cfg Datei findest du 
[hier](https://github.com/Bully85/Sovol-SV04-Klipper/tree/main/config/Sv04-works-with%20origin-klipper). 
Bevor die Datei hochgeladen wird, muss diese erst bearbeitet werden. Abhängig von deinem 
Mainboard müssen im Abschnitt "#   Z Stepper Settings" die richtigen Zeilen aktiviert werden. 

Das Hochladen kann einfach über die Klipper-Weboberfläche passieren. 
Neben printer.cfg müssen die folgenden Dateien auch in config Verzeichnis hochgeladen werden. 
* macros.cfg
* IDEX_mode.cfg
* misc.cfg
* Start_End_Macro.cfg

Als nächstes muss die Software auf dem Printer Mainboard ersetzt werden. 

Dazu die Datei firmware.bin auf eine Speicherkarte kopieren welche im Drucker eingesteckt 
werden kann. 
* den Drucker ausschalten
* die Speicherkarte einstecken
* den Drucker einschalten. Das Display zeigt den normalen Fortschrittsbalken, der aber 
nicht bewegt. Zwei Minuten warten, den Drucker wieder ausschalten. 
* Wenn die Datei auf der Specherkarte in firmware.CUR umbenannt worden ist, ist das das 
Zeichen dass die Firmware korrekt geladen wurde. 

Jetzt kann der Raspberry mit dem Drucker verbunden werden. Nach einem Restart von Klipper 
sollte alles funktionieren. 

## Alternative Installationsmöglichkeiten (mit älteren Versionen)

### Installation mit einem bereits vorkonfigurierten Betriebssystem-Image

Das Betriebssystem für den Raspberry findet ihr im Verzeichniss "[image Raspberry PI 3_4](https://drive.google.com/drive/folders/1rZepxzwUR5QTXRXcv5EBYin_gFiMcKVD)". 
Dieses wird mit Hilfe des [Raspberry Pi Imagers](https://www.raspberrypi.com/software/) auf die MicroSD-Karte gespielt. 
Achtet darauf gleich eure Wifi-Einstellungen anzupassen (diese findet ihr wenn ihr unten rechts auf das Zahnrad klickt). 

Die firmware.bin im Verzeichnis "Firmware bin" kommt auf die (große)SD-Karte und wird mit ausgestecktem original Display (wird vorerst nicht mehr benötigt, da es nicht mehr funktioniert) auf den Drucker geflasht. 
Die Dateien aus dem "config" verzeichniss werden dann, [wie unten beschrieben](#dateiübertragung) oder direkt im Mainsail Interface, auf den Raspberry übertragen. Sobald der Pi gestartet ist, kann das Interface per IP oder Hostname erreicht werden.
- der Hostname kann bei den WiFi Settings im Pi Imager eingestellt werden
- the IP kann via Router Oberfläche herausgefunden werden
- 

### Installation auf einem neuen OS

#### Ohne Kiauh

Beschreibung folgt .....

#### Solltet ihr Kiauh nutzen
Folgt zuerst den [Kiauh](https://github.com/th33xitus/kiauh) Anweisungen und kommt dann zurück.

- Meldet euch per ssh beim Raspi an und gebt folgenden befehl ein:
```sh
sudo nano kiauh/klipper_repos.txt.example
```

- Dort fügt ihr am Ende der Datei die folgende Zeile ein (siehe Bild):
```sh
https://github.com/Bully85/klipper
```
![KiauhSV04](docs/img/klipper_repos.txt.PNG)

- Speichert die Datei mit Ctrl+X -> Y
- Löscht das '.example' vom Ende des Dateinamens
- und öffnet Kiauh mit dem Befehl
```sh
./kiauh/kiauh.sh
```
- Hier wählen wir [6] Settings
- Dann [1] Set custom Klipper repository
- Dann [4] Bully85/klipper
- Und alles mit [ y ] bestätigen.

Fertig mit SSH

# Benutzung von SSH 
Ihr könnt SSH über eine [grafische Oberfläche](#benötigt) verwenden, oder über das Terminal.
Wenn ihr Putty benutzt, folgt deren Anweisungen.
Das Terminal ist schon installiert und normalerweise schneller.

- öffnet das Windows-Terminal (es heißt Terminal, nicht das alte CMD) oder Powershell
- verbindet euch mit 'ssh benutzername@hostname' und gebt Passwort ein
    - Benutzername und Hostname sind die, die ihr [oben](#installation-auf-einem-bestehenden-os) eingerichtet habt
    - wenn ihr auf ein bestehendes OS installiert, kennt ihr euren Benutzer- und Hostnamen hoffentlich schon/noch
- macht zeugs...
- zum Beenden Ctrl+D drücken


# Dateiübertragung 

Nun müssen die Dateien und Ordner aus dem "config"-Verzeichnis auf den Raspberry Pi kopiert werden. Standardmäßig in "printer_data".
Sollte dies bei euch nicht der Fall, passt bitte die Pfade in den Config- und .sh-Dateien an.

Am einfachsten geht das über ein SFTP- oder SCP-Programm, wie z.B. [FileZilla oder WinScp](#benötigt)


# Behebung der 'ungültig' Anzeige in Mainsail

meldet euch per SSH bei Klipper an und führt den folgenden Befehl aus:
```sh
sudo nano ~/printer_data/systemd/moonraker.env
```
![moonraker.env1](docs/img/moonraker.env1.JPG)

Fügt "-g" am Ende der "MOONRAKER_ARGS"-Zeile an:
![moonraker.env2](docs/img/moonraker.env2.JPG)

Speichern und Datei schließen.
Dann ein Neustart


In Mainsail klickt auf 'ungültig' und führt eine Soft Repair durch. 

fertig!!!!!
