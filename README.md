# EGLO 99099 Remote - Zigbee2MQTT RGB-CCT Blueprint

Mit diesem Blueprint lässt sich die EGLO 99099 Fernbedienung (via Zigbee2MQTT) mühelos in Home Assistant integrieren, um RGB-CCT LED-Streifen zu steuern. Die Einrichtung ist speziell für Einsteiger optimiert.

## Voraussetzungen
* Home Assistant (aktuelle Version)
* Zigbee2MQTT (Z2M) eingerichtet
* EGLO 99099 Fernbedienung (verbunden via Z2M)
* Kompatibles RGB-CCT Leuchtmittel (Entität `light.*`)

## Installation in Home Assistant

Öffne das Terminal (SSH) in Home Assistant und lade das Blueprint mit folgendem Befehl direkt in dein System herunter:

```bash
curl -o /config/blueprints/automation/eglo_99099_rgbcct.yaml [https://raw.githubusercontent.com/Schmidtjanroman/ELGO-99099-HASS-Z2M/main/eglo_99099_rgbcct.yaml](https://raw.githubusercontent.com/Schmidtjanroman/ELGO-99099-HASS-Z2M/main/eglo_99099_rgbcct.yaml)
<img width="192" height="150" alt="Eglo_99099" src="https://github.com/user-attachments/assets/af3b9015-7c52-4354-805d-c19b941e13b6" />


<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 550 430" style="background:#1e1e1e; font-family: monospace;">
  <!-- Remote Gehäuse -->
  <rect x="40" y="10" width="200" height="410" rx="40" fill="#2c2c2e"/>
  <rect x="40" y="70" width="200" height="300" fill="#1c1c1e"/>

  <!-- 1. Off | 2. On -->
  <circle cx="90" cy="40" r="12" fill="none" stroke="#fff" stroke-width="2"/>
  <circle cx="190" cy="40" r="12" fill="none" stroke="#fff" stroke-width="2"/>
  <path d="M190,32 L190,48" stroke="#fff" stroke-width="2"/>
  
  <path d="M 90,28 L 90,25 L 280,25" fill="none" stroke="#00E5FF" stroke-width="1.5" />
  <circle cx="280" cy="25" r="3" fill="#00E5FF"/><text x="295" y="29" fill="#fff" font-size="14">1. Off (off)</text>

  <path d="M 202,40 L 280,40" fill="none" stroke="#00E5FF" stroke-width="1.5" />
  <circle cx="280" cy="40" r="3" fill="#00E5FF"/><text x="295" y="44" fill="#fff" font-size="14">2. On (on)</text>

  <!-- 3. Grün -->
  <circle cx="140" cy="100" r="10" fill="#32d74b"/>
  <path d="M 140,90 L 140,75 L 280,75" fill="none" stroke="#00E5FF" stroke-width="1.5" />
  <circle cx="280" cy="75" r="3" fill="#00E5FF"/><text x="295" y="79" fill="#fff" font-size="14">3. Grün Kanal +10</text>

  <!-- 4. Rot | 5. Zyklus | 6. Blau -->
  <circle cx="90" cy="140" r="10" fill="#ff453a"/>
  <path d="M 90,130 L 90,115 L 280,115" fill="none" stroke="#00E5FF" stroke-width="1.5" />
  <circle cx="280" cy="115" r="3" fill="#00E5FF"/><text x="295" y="119" fill="#fff" font-size="14">4. Rot Kanal +10</text>

  <circle cx="140" cy="140" r="10" fill="none" stroke="#fff" stroke-width="2"/>
  <path d="M 150,140 L 280,140" fill="none" stroke="#00E5FF" stroke-width="1.5" />
  <circle cx="280" cy="140" r="3" fill="#00E5FF"/><text x="295" y="144" fill="#fff" font-size="14">5. Farbzyklus (22.5°)</text>

  <circle cx="190" cy="140" r="10" fill="#0a84ff"/>
  <path d="M 190,150 L 190,165 L 280,165" fill="none" stroke="#00E5FF" stroke-width="1.5" />
  <circle cx="280" cy="165" r="3" fill="#00E5FF"/><text x="295" y="169" fill="#fff" font-size="14">6. Blau Kanal +10</text>

  <!-- 7. Refresh -->
  <path d="M 132,180 h16 v16 h-16 z" fill="none" stroke="#fff" stroke-width="1.5"/>
  <path d="M 150,188 L 280,188" fill="none" stroke="#00E5FF" stroke-width="1.5" />
  <circle cx="280" cy="188" r="3" fill="#00E5FF"/><text x="295" y="192" fill="#fff" font-size="14">7. Moduswechsel (CCT/RGB)</text>

  <!-- Grid Raster -->
  <line x1="40" y1="210" x2="240" y2="210" stroke="#3a3a3c" stroke-width="2"/>
  <line x1="40" y1="270" x2="240" y2="270" stroke="#3a3a3c" stroke-width="2"/>
  <line x1="40" y1="330" x2="240" y2="330" stroke="#3a3a3c" stroke-width="2"/>
  <line x1="106" y1="210" x2="106" y2="390" stroke="#3a3a3c" stroke-width="2"/>
  <line x1="173" y1="210" x2="173" y2="390" stroke="#3a3a3c" stroke-width="2"/>

  <!-- Reihe 1: B+ | Fav1 | CCT+ -->
  <circle cx="73" cy="240" r="6" fill="none" stroke="#fff" stroke-width="1.5"/> <!-- B+ Icon -->
  <path d="M 73,228 v-3 M 73,248 v3 M 61,240 h-3 M 81,240 h3 M 65,232 l-2,-2 M 81,248 l2,2 M 65,248 l-2,2 M 81,232 l2,-2" stroke="#fff" stroke-width="1.5"/>
  
  <text x="140" y="246" fill="#fff" font-size="16" text-anchor="middle">♡1</text>
  
  <circle cx="206" cy="240" r="5" fill="#fff"/> <!-- CCT+ Icon -->
  <path d="M 206,230 v-2 M 206,250 v2 M 196,240 h-2 M 216,240 h2 M 199,233 l-1.5,-1.5 M 213,247 l1.5,1.5 M 199,247 l-1.5,1.5 M 213,233 l1.5,-1.5" stroke="#fff" stroke-width="1.5"/>

  <!-- Lines R1 -->
  <path d="M 73,226 L 73,215 L 280,215" fill="none" stroke="#00E5FF" stroke-width="1.5" />
  <circle cx="280" cy="215" r="3" fill="#00E5FF"/><text x="295" y="219" fill="#fff" font-size="14">8. Helligkeit +</text>

  <path d="M 155,240 L 182,240 L 182,232 L 280,232" fill="none" stroke="#00E5FF" stroke-width="1.5" />
  <circle cx="280" cy="232" r="3" fill="#00E5FF"/><text x="295" y="236" fill="#fff" font-size="14">9. Favorit 1</text>

  <path d="M 206,252 L 206,260 L 280,260" fill="none" stroke="#00E5FF" stroke-width="1.5" />
  <circle cx="280" cy="260" r="3" fill="#00E5FF"/><text x="295" y="264" fill="#fff" font-size="14">10. Wärmer (CCT+)</text>


  <!-- Reihe 2: B- | Fav2 | CCT- -->
  <circle cx="73" cy="300" r="4" fill="none" stroke="#fff" stroke-width="1.5"/> <!-- B- Icon -->
  <path d="M 73,293 v-2 M 73,307 v2 M 66,300 h-2 M 80,300 h2 M 68,295 l-1.5,-1.5 M 78,305 l1.5,1.5 M 68,305 l-1.5,1.5 M 78,295 l1.5,-1.5" stroke="#fff" stroke-width="1.5"/>

  <text x="140" y="306" fill="#fff" font-size="16" text-anchor="middle">♡2</text>
  
  <path d="M 206,292 v16 M 198,300 h16 M 200,294 l12,12 M 200,306 l12,-12" stroke="#fff" stroke-width="1.5"/> <!-- CCT- Icon -->

  <!-- Lines R2 -->
  <path d="M 73,288 L 73,278 L 280,278" fill="none" stroke="#00E5FF" stroke-width="1.5" />
  <circle cx="280" cy="278" r="3" fill="#00E5FF"/><text x="295" y="282" fill="#fff" font-size="14">11. Helligkeit -</text>

  <path d="M 155,300 L 182,300 L 182,292 L 280,292" fill="none" stroke="#00E5FF" stroke-width="1.5" />
  <circle cx="280" cy="292" r="3" fill="#00E5FF"/><text x="295" y="296" fill="#fff" font-size="14">12. Favorit 2</text>

  <path d="M 206,312 L 206,320 L 280,320" fill="none" stroke="#00E5FF" stroke-width="1.5" />
  <circle cx="280" cy="320" r="3" fill="#00E5FF"/><text x="295" y="324" fill="#fff" font-size="14">13. Kälter (CCT-)</text>


  <!-- Reihe 3: G1 | G2 | G3 -->
  <text x="73" y="366" fill="#fff" font-size="18" text-anchor="middle" font-weight="bold">1</text>
  <text x="140" y="366" fill="#fff" font-size="18" text-anchor="middle" font-weight="bold">2</text>
  <text x="206" y="366" fill="#fff" font-size="18" text-anchor="middle" font-weight="bold">3</text>

  <!-- Lines R3 -->
  <path d="M 73,348 L 73,338 L 280,338" fill="none" stroke="#00E5FF" stroke-width="1.5" />
  <circle cx="280" cy="338" r="3" fill="#00E5FF"/><text x="295" y="342" fill="#fff" font-size="14">14. Gruppe 1</text>

  <path d="M 152,360 L 182,360 L 182,352 L 280,352" fill="none" stroke="#00E5FF" stroke-width="1.5" />
  <circle cx="280" cy="352" r="3" fill="#00E5FF"/><text x="295" y="356" fill="#fff" font-size="14">15. Gruppe 2</text>

  <path d="M 206,372 L 206,380 L 280,380" fill="none" stroke="#00E5FF" stroke-width="1.5" />
  <circle cx="280" cy="380" r="3" fill="#00E5FF"/><text x="295" y="384" fill="#fff" font-size="14">16. Gruppe 3</text>

</svg>
