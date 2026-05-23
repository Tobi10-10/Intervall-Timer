# Intervall-Timer

Eigenständige PWA (Progressive Web App) für Intervall-Training. Funktioniert offline, hat keine Abhängigkeiten und lässt sich auf dem iPhone wie eine native App installieren.

## Deployment auf GitHub Pages

1. Neues Repository auf GitHub anlegen (z. B. `intervall-timer`)
2. Alle Dateien aus diesem Ordner ins Repo-Root hochladen:
   - `index.html`
   - `sw.js`
   - `manifest.webmanifest`
   - `apple-touch-icon.png`
   - `icon-512.png`
3. Im Repository: **Settings → Pages → Source: `Deploy from a branch` → Branch: `main` / `(root)`** → speichern
4. Nach 1–2 Minuten ist die App unter `https://<username>.github.io/<repo-name>/` erreichbar

## Auf dem iPhone installieren

1. URL in **Safari** öffnen (nicht Chrome – die iOS-PWA-Installation funktioniert nur über Safari)
2. Teilen-Symbol (Quadrat mit Pfeil) antippen
3. **„Zum Home-Bildschirm hinzufügen"** wählen
4. Beim ersten Start in Safari registriert sich der Service Worker im Hintergrund. Danach funktioniert die App vollständig offline.

## Funktionen

- Konfigurierbare Belastungs- und Pausenzeiten (1–600 Sekunden)
- 1–99 Wiederholungen
- Drei Voreinstellungen: Tabata (20/10 · 8x), 30/15 · 10x, 45/15 · 8x
- Akustische Signale: Countdown in den letzten 3 Sekunden, unterschiedliche Töne für Belastung/Pause-Wechsel, Abschluss-Akkord
- Pause / Fortsetzen / Stopp / Überspringen
- Einstellungen werden automatisch gespeichert
- Wake Lock hält den Bildschirm während des Trainings an

## Bekannte Einschränkungen unter iOS

- **Stummschalter beachten**: Der seitliche Mute-Schalter des iPhones überschreibt Web-Audio. Bei fehlendem Ton zuerst diesen Schalter prüfen.
- **Wake Lock**: Funktioniert ab iOS 16.4+ über HTTPS (GitHub Pages ist HTTPS).
- **Erster Tap**: Audio wird erst nach dem ersten Tap (Start-Button) freigeschaltet – das ist eine iOS-Sicherheitsrichtlinie, die kein Programm umgehen kann.

## Update veröffentlichen

1. Datei lokal ändern und ins Repo pushen
2. In `sw.js` die Variable `CACHE_VERSION` erhöhen (z. B. `v1` → `v2`) – dadurch löscht der Service Worker den alten Cache automatisch
3. Auf dem iPhone: Safari öffnen, Seite per Pull-down aktualisieren. Beim nächsten Home-Screen-Start ist die neue Version aktiv.

## Architektur

| Datei | Zweck |
|-------|-------|
| `index.html` | Komplette App inkl. CSS und JS (~26 KB) |
| `sw.js` | Service Worker: Cache-First-Strategie für Offline-Betrieb |
| `manifest.webmanifest` | PWA-Manifest (für Android/Chrome) |
| `apple-touch-icon.png` | 180×180 Home-Screen-Icon (iOS) |
| `icon-512.png` | 512×512 Icon (Android/Manifest) |

Keine externen Abhängigkeiten, kein Build-Schritt, kein npm.
