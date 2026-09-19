# MIDNOX Visualizer Studio – Changelog

Alle wichtigen Änderungen und Versionsschritte des MIDNOX Visualizer Studios und der dazugehörigen GPU-Render-Engine.

---

## [1.7.0] – September 2026 (Aktuell)
### Neu hinzugefügt & Verbessert
- **Social-Media „Safe-Zones“ Einblendung (TikTok & Instagram Reels):**
  - **Interaktives Sicherheits-Overlay:** Neuer Toggle-Button `🛡️ Safe-Zone` im 9:16 Vertikal-Modus.
  - **Präzise UI-Schutzzonen:** Zeigt die durch Social-Media-Apps verdeckten Bereiche an:
    - ⚠️ *Kopfbereich (0–180px):* Profilname, Suchleiste und Gerätestatus.
    - ⚠️ *Fußbereich (1540–1920px):* Songtitel, Caption/Untertitel und Navigationsleiste.
    - ⚠️ *Rechter Interaktionsbereich (940–1080px):* Like-, Kommentar-, Share- und Sound-Buttons.
    - 🛡️ *Grüner Content-Sicherheitsbereich:* Garantiert, dass Artwork, Visualizer-Balken, Typografie und Badge stets voll sichtbar bleiben.
  - **Export-Sicherheit:** Das Overlay ist ausschließlich in der Vorschau aktiv und wird beim finalen MP4-Video niemals eingebrannt.
- **Typografie-Freiheit (Unabhängige Offsets & Skalierung für Titel & Künstler):**
  - **Format-getrennte Steuerung:** Individuelle X/Y-Verschiebungen und Schriftgrößen-Skalierung (70%–150%) für 16:9 Widescreen und 9:16 Vertikal.
  - **Getrennte Künstler- & Songtitel-Justierung:** Künstlername und Track-Titel können völlig unabhängig voneinander verschoben und skaliert werden.
  - **Volle GPU-Parität:** Alle typografischen Offsets und Skalierungen werden 1:1 in `render_specterr_visualizer.py` mit hardwarebeschleunigter Text-Gradienten-Generierung gerendert.
- **Automatische Drop- & Kick-Erkennung (Timeline-Marker):**
  - **Intelligente Audio-Energieanalyse:** Berechnet beim Laden eines Audios (WAV/MP3) automatisch 50ms RMS-Energiekurven und erkennt markante Energieanstiege (Bass-Drops, Kicks, Hooklines).
  - **Leuchtende Diamant-Marker auf der Timeline:** Visuelle Positionierung der wichtigsten Song-Höhepunkte auf der Zeitleiste.
  - **1-Klick-Anspringen & Snippet-Sync:** Ein Klick auf den Marker springt sofort an die entsprechende Stelle im Track und synchronisiert auf Wunsch den Snippet-Startpunkt.
- **Design-Presets speichern & laden:**
  - **5 kuratierte Werkspresets:** 1-Klick-Styles für gängige Musikgenres:
    - 🌌 *Cyberpunk Neon* (Cyan & Magenta, Specterr-Balken, Theme-Ambilight, Pulsing)
    - 🌅 *Sunset Deep House* (Gold, Warm-Orange & Rot, Wave-Visualizer, Sunset-Badge)
    - ⚡ *Acid Toxic Hardstyle* (Giftgrün & Cyan, starker Camera-Shake, intensiver Beat-Pulse)
    - 💎 *Clean Luxury Minimal* (Weiß & Eisblau, Radial-Visualizer, Glassmorphism-Badge)
    - 🍇 *Purple Haze Pop* (Violett, Indigo & Cyan, moderater Beat-Pulse, Neon-Pill)
  - **Eigene User-Presets:** Speichern, Laden und Löschen eigener Favoriten-Styles im lokalen Browser-Speicher (`localStorage`).
  - **JSON Export & Import:** Portabler Austausch eigener Preset-Sammlungen per Download/Upload.
- **Akustisches & Visuelles Fertigstellungs-Signal:**
  - **Web Audio Chime:** Wohlklingendes 4-Ton-Synthesizer-Arpeggio (E-Dur: E5, G#5, B5, E6) mit exponentieller Hüllkurve direkt im Browser.
  - **Desktop-Benachrichtigung:** HTML5 Notification API benachrichtigt sofort über die Fertigstellung – auch bei minimiertem Browserfenster.
  - **Server-Konsolen-Signalton:** Windows-Konsolen-Doppelpiepen (`winsound.Beep`) informiert auch beim Blick auf das Terminal.

---

## [1.6.0] – September 2026
### Neu hinzugefügt & Verbessert
- **Format-getrennte Badge-Positionierung (Widescreen 16:9 vs. Vertikal 9:16):**
  - **Unabhängige X/Y-Offsets:** Horizontale und vertikale Videos besitzen nun getrennte Offset-Werte (`offsetXWide`/`offsetYWide` und `offsetXVert`/`offsetYVert`).
  - **Format-Umschalter im Studio:** Neuer Segmented-Control-Button direkt über den Badge-Schiebereglern ermöglicht das Umschalten zwischen *Widescreen (16:9)* und *Vertikal (9:16)*. Beim Wechsel des Layout-Formats schaltet auch der Badge-Editor automatisch mit.
  - **100% Abwärtskompatibilität:** Ältere Releases und Job-Dateien mit gemeinsamen `offsetX`/`offsetY` werden nahtlos als Fallback geladen.
- **Selektiver Kamera-Shake (Bass-Drop Erschütterung):**
  - **Getrennte Layer-Steuerung:** Es wackelt nicht mehr die gesamte Komposition unkontrolliert durcheinander. Vier dedizierte Checkboxen erlauben die gezielte Auswahl:
    - 🏞️ *Hintergrund* (bewegt sich auf Bass-Peaks)
    - 🖼️ *Cover Artwork & Rahmen* (kann separat abgewählt werden – der Cover-Rahmen im Vertikal-Video bleibt auf Wunsch **100% still und wackelfrei**!)
    - 📊 *Visualizer-Balken & Typografie* (Balken und Track-Titel vibrieren auf Wunsch zum Beat)
    - 🏷️ *Logo / Wasserzeichen* (Logo kann ruhig in der Ecke stehen oder mitvibrieren)
  - **Artefaktfreies Overscan-Rendering:** Die GPU-Render-Engine berechnet den Hintergrund mit Randpuffer ohne qualitätsmindernden nachträglichen Frame-Crop.
- **Selektiver Beat-Pulse (Bass-Pumpen):**
  - **Gezielte Beat-Reaktivität:** Wähle flexibel aus, welche visuellen Elemente zum Kick-Bass pumpen:
    - 🖼️ *Cover / Vinyl* (pulsierende Cover-Größe)
    - 📊 *Visualizer-Balken aufblähen* (Balken wachsen dynamisch zusätzlich in die Höhe bei druckvollen Bass-Kicks)
    - 🏷️ *Logo / Wasserzeichen* (subtiles Mitschwingen der Logo-Größe)
- **Volle GPU- & Canvas-Parität:** Alle neuen Steuerungen und Layer-Berechnungen greifen identisch in der interaktiven HTML5-Studio-Vorschau und im NVENC-Renderer (`render_specterr_visualizer.py`).

---

## [1.5.0] – September 2026
### Neu hinzugefügt & Verbessert
- **1-Click In-Browser Auto-Updater (`midnox.de/Studio/`):**
  - **Automatische Versionserkennung:** Beim Start prüft das Studio im Hintergrund, ob auf dem Webserver (`midnox.de/Studio/version.json`) ein neues Update bereitsteht.
  - **Update-Benachrichtigung:** Bei neuer Version erscheint ein pulsierendes grünes Update-Badge in der Kopfzeile („🚀 Update verfügbar!“).
  - **In-Browser Update-Modal:** Detailansicht der installierten vs. neuesten Version, Auflistung aller Neuerungen aus dem Remote-Changelog und 1-Klick-Aktualisierung.
  - **Automatisches Sicherheits-Backup & Safe-Extraction:** Vor dem Extrahieren werden alle Kernskripte automatisch als ZIP-Archiv im Ordner `_backup/` gesichert. Benutzerdefinierte Ordner wie `Releases/`, persönliche MP3s/WAVs und Covers werden streng geschützt und niemals überschrieben. Nach erfolgreichem Update lädt der Browser die Anwendung automatisch neu.
  - **Manueller Update-Check:** Über die Versionshistorie (Changelog-Dialog) kann jederzeit per Klick auf „🔄 Nach Updates suchen“ eine Prüfung forciert werden.
- **Interaktive Audio-Timeline & Scrubber:**
  - **Echtzeit-Zeitanzeige:** Exakte Darstellung der aktuellen Position und Gesamtdauer (`00:00 / 00:00 min`).
  - **Interaktive Zeitleiste:** Klick- und ziehbare Timeline zum sekundengenauen Vor- und Zurückspulen während des Abspielens.
  - **5s-Schnellsprungtasten:** Schnelles Springen im Track via `⏪ -5s` und `⏩ +5s`.
  - **1-Klick-Snippet-Sync:** Übernahme der aktuellen Abspielzeit als Startpunkt für den Social-Media-Clip („🎯 Zeit übernehmen“).
- **Release Cockpit & Dashboard 2.0:**
  - **Nahtlose Tab-Integration:** Umschalten zwischen Studio und Cockpit direkt über die Kopfleiste ohne Fensterwechsel.
  - **Releases-Auflistung:** Schnelle Anzeige aller 114+ Tracks mit Suche und Genre-Filtern.
- **Render-Stabilität & Lock-Entkopplung:**
  - Beseitigung des Rendering-Hängers bei 97–100% durch reentrante Thread-Locks (`threading.RLock`) und strikte Trennung von I/O-Logging.

---

## [1.4.0] – September 2026
### Neu hinzugefügt & Verbessert
- **Release Cockpit & Dashboard 2.0 (`dashboard.html`):**
  - **Live-Metadaten-Editor:** Nachträgliches Eintragen und Bearbeiten von Songtitel, Interpret, Genre, BPM, Songtexten (Lyrics), Suno AI-Prompts und Beschreibungen per Klick auf „✏️ Bearbeiten“.
  - **Automatische ID3-Tag & Dateisynchronisation:** Beim Speichern werden nicht nur die Textdateien (`Songtext.txt`, `Suno_Prompt.txt`, `press_text.txt`) und `release_job.json` aktualisiert, sondern alle Tags (`USLT` Lyrics, `TCON` Genre, `TBPM` Tempo, `TPE1` Interpret, `TIT2` Titel) direkt in die jeweilige `.mp3`-Audiodatei eingebettet.
  - **Fertige Facebook- & Social-Media-Werbetexte:** Vollautomatisches Erstellen werbewirksamer Posts mit Track-Infos, Emojis, Hashtags und `midnox.de`-Hinweis inkl. 1-Klick-Kopieren.
  - **Nahtlose Video-Upload-Integration:** Neuer Button „📁 Video-Ordner öffnen“ im Werbetext-Tab für sofortiges Drag & Drop des MP4-Videos in Facebook oder Instagram.
  - **Render-Pipeline & Server-Stabilität:**
    - Behebung des Pipe-Deadlocks in der Render-Engine (Entfernung von `-shortest` und Hinzufügen von Broken-Pipe-Handling).
    - Windows-Konsole: Automatisches Deaktivieren des QuickEdit-Modus (`disable_quick_edit`) gegen versehentliches Pausieren durch Mausklicks.
    - Umstellung des Studio-Servers auf `ThreadingHTTPServer` für unterbrechungsfreie parallele Datei-Downloads und Dashboard-Abfragen.

---

## [1.3.0] – September 2026
- **Release-Badge & Sticker 2.0:**
  - **Stufenlose Größenanpassung:** Schieberegler von 60% bis 180% mit gestochen scharfer Vektor-Skalierung (Schriftgröße, Innenabstände, Pill-Radien und Glow).
  - **Wahlweise Bass-Vibration / Beat-Pulse (+16% Kick-Bounce):** Das Badge reagiert auf Wunsch dynamisch auf druckvolle Kicks und Bass-Drops mit lebendiger Mikrovibration um seinen eigenen Mittelpunkt.
  - **Entkoppelte Stillstand-Garantie:** Bei Deaktivierung der Checkbox *„Mit Bass mitvibrieren / pulsieren“* steht das Badge zu 100% ruhig und felsenfest – es wird vollständig von der globalen Kamera-Erschütterung (*Camera-Shake*) isoliert.
  - **Kurierte Neon-Gradients:** Auswahl aus *Cyber Neon* (Cyan/Magenta), *Sunset Fire* (Gold/Orange), *Acid Toxic* (Grün/Cyan), *Crimson Flare* (Rot/Pink), *Purple Haze* (Violett/Blau), *Monochrom* (Weiß) sowie dynamischem Track-*Farbschema*.
  - **Freie Farbwahl & Custom 2-Color Gradients:** Integrierte Color-Picker mit Live-Hex-Vorschau zur freien Kombination zweier Verlaufsfarben oder einheitlicher Volltonfarbe.
  - **Volle GPU-Parität:** Synchrone Unterstützung im HTML5-Canvas-Studio und in der NVIDIA NVENC Render-Engine (`render_specterr_visualizer.py`).

---

## [1.2.0] – September 2026
### Neu hinzugefügt
- **Akkordeon-System für Seitenleiste:** Alle Einstellungsgruppen sind platzsparend einklappbar, inklusive Live-Status-Badges und Toolbar zum Auf-/Zuklappen aller Bereiche.
- **Ambient-Aura (Ambilight Cover-Glow):** Musiksynchrone, leuchtende Aura hinter dem Album-Cover mit dynamischer Bass-Atmung und einstellbaren Farbmodi.
- **Bass-Drop Kamera-Shake:** Kinoreifer Mikrojitter bei harten Bass-Drops (ab 62% Bass-Energie) mit 20px Overscan-Padding gegen Randrauschen.
- **Release-Badge Basisversion:** Erste Einführung des Promo-Stickers am Album-Cover mit Eck-Auswahl und Positions-Offset-Reglern.

---

## [1.1.0] – September 2026
### Neu hinzugefügt
- **Audio-Snippet & Cutter:** Integrierter Trimmer für Social-Media-Clips (15s Story, 30s TikTok/Shorts, 60s Reel oder voller Track) mit interaktivem Startzeit-Slider und sekundengenauem GPU-Schnitt.
- **Beat-Pulse & Cover-Pumpen:** Dynamisches Mitpulsieren des Covers und der Vinyl-Disc im Takt der Kick-Frequenzen mit frei wählbarer Intensität.
- **Schwebende Partikel & Staub-Effekt:** Sanft aufsteigende Bokeh- und Lichtpartikel im Hintergrund für visuelle Tiefe.

---

## [1.0.1] – September 2026
### Verbesserungen & Fehlerbehebungen
- **Wasserzeichen & Logo-Offsets:** Freie Verschiebung auf X- und Y-Achse (-400px bis +400px) inkl. 1-Klick-Reset.
- **Eigenes Bild-Logo:** Upload eigener Logos (PNG mit Alpha / JPG) mit nativer Farbwiedergabe ohne Farbverfälschung.
- **Unabhängiger Blur & Dim:** Weichzeichnung und Abdunklung für 16:9 Widescreen und 9:16 Vertical getrennt konfigurierbar.
- **Live-Renderfortschritt:** Prozentanzeige, Frame-Zähler, FPS und dynamische Restzeitschätzung während des GPU-Rendering.

---

## [1.0.0] – September 2026
### Initiales Release
- **Autarkes Standalone-Paket:** 100% portables Windows-Paket mit integriertem Python 3.14 und FFmpeg ohne externe Abhängigkeiten.
- **NVIDIA NVENC High-Speed Engine:** Hardware-beschleunigtes Rendering für 1080p Widescreen (1920×1080) und Vertical (1080×1920).
- **4 Visualizer-Stile:** Specterr, Vinyl, Radial und Wave mit anpassbaren Farbverläufen und Typografie.
- **Interaktive HTML-Bedienungsanleitung (`anleitung.html`).**
