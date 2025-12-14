# Changelog

Alle wesentlichen Änderungen an diesem Projekt werden in dieser Datei dokumentiert.

Das Format basiert auf [Keep a Changelog](https://keepachangelog.com/de/1.0.0/),
und dieses Projekt folgt [Semantic Versioning](https://semver.org/lang/de/).

## [1.0.0] - 2025-12-14

### Hinzugefügt
- 🎉 Initiales Release
- ✅ Multiroom-Unterstützung mit unabhängiger Steuerung
- ✅ Aktivitätsbasierte Szenen für AV-Geräte
- ✅ **Smart Activity Switching** - Geräte bleiben eingeschaltet beim Wechsel
- ✅ Automatische Lautstärkeregelung pro Aktivität
- ✅ Power Sequencing mit konfigurierbaren Verzögerungen
- ✅ Input Source Management mit Dropdown-Auswahl
- ✅ UI-basierte Konfiguration (kein YAML erforderlich)
- ✅ Vollständige deutsche Übersetzung
- ✅ Englische Übersetzung
- ✅ Home Assistant Area Integration
- ✅ Media Player Picklists
- ✅ Source Picklists (automatisch vom Gerät geladen)
- ✅ Automatische Szenen-Generierung
- ✅ Activity-Status-Switches pro Raum
- ✅ CRUD-Funktionalität für Räume, Aktivitäten und Geräte
- ✅ Auto-Save bei Konfigurationsänderungen
- ✅ Auto-Reload nach Config-Änderungen

### Features im Detail

#### Smart Activity Switching
- Analysiert welche Geräte in beiden Aktivitäten verwendet werden
- Hält gemeinsame Geräte eingeschaltet
- Aktualisiert nur Input-Source und Lautstärke
- Reduziert Wechselzeit von 20-30 Sekunden auf 2-3 Sekunden

#### Services
- `av_scenes.start_activity` - Aktivität starten
- `av_scenes.stop_activity` - Aktivität stoppen
- `av_scenes.reload` - Konfiguration neu laden

### Dokumentation
- README mit Beispielen
- SMART_SWITCHING.md - Technische Dokumentation
- TRANSLATIONS.md - Übersetzungs-Anleitung

## Roadmap

### [1.1.0] - Geplant
- Integration weiterer Aktivitäten (Beispiel: Lichtstimmung, Rolladen, etc.)

[1.0.0]: https://github.com/YOURUSERNAME/av-scenes/releases/tag/v1.0.0