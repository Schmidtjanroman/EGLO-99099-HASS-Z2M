# EGLO 99099 Remote - Zigbee2MQTT RGB-CCT Blueprint

Mit diesem Blueprint lässt sich die EGLO 99099 Fernbedienung (via Zigbee2MQTT) mühelos in Home Assistant integrieren, um RGB-CCT Leuchtmittel zu steuern.

## Voraussetzungen
* Home Assistant (aktuelle Version, getestet mit Core 2026.9.1)
* Zigbee2MQTT (Z2M) eingerichtet  (https://www.zigbee2mqtt.io/devices/99099.html)
* EGLO 99099 Fernbedienung (verbunden via Z2M)
* Kompatibles RGB-CCT Leuchtmittel (Entität `light.*`)

## Installation in Home Assistant

Öffne das Terminal (SSH) in Home Assistant und lade das Blueprint mit folgendem Befehl direkt in dein System herunter:

```bash
curl -o /config/blueprints/automation/eglo_99099_rgbcct.yaml [https://raw.githubusercontent.com/Schmidtjanroman/ELGO-99099-HASS-Z2M/main/eglo_99099_rgbcct.yaml](https://raw.githubusercontent.com/Schmidtjanroman/ELGO-99099-HASS-Z2M/main/eglo_99099_rgbcct.yaml)
<img width="192" height="150" alt="Eglo_99099" src="https://github.com/user-attachments/assets/af3b9015-7c52-4354-805d-c19b941e13b6" />
````

## Konfiguration (Schritt-für-Schritt)
*Gehe in Home Assistant zu Einstellungen -> Automatisierungen & Szenen -> Blueprints.
*Wähle das Blueprint EGLO 99099 Remote - Zigbee2MQTT RGB-CCT Steuerung und klicke auf Automatisierung erstellen.
*Fülle die Felder entsprechend deiner Geräte aus:
*Zigbee2MQTT Base Topic: Trage hier den genauen Namen deiner Fernbedienung ein, wie er in Zigbee2MQTT steht (z. B. zigbee2mqtt/Paula Remote).
*Zu steuernde Gruppe: Wähle die Taste auf der Fernbedienung (1, 2, 3 oder Alle), auf die die Lampe reagieren soll.
*LED-Streifen: Wähle die Entität deines Lichts aus (z. B. light.hochbett).
*(Optional) Passe deine Lieblingsfarben (Favorit 1 & 2) sowie die Schrittweiten für Helligkeit und Farbtemperatur nach Belieben an.
*Speichere die Automatisierung.
<img width="602" height="653" alt="image" src="https://github.com/user-attachments/assets/1c701e8d-4fd3-4d39-8176-f474650c2aee" />


## Belegung
<img src="./Eglo_99099.svg">
