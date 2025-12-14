# Changelog

Alle wesentlichen Änderungen an diesem Projekt werden in dieser Datei dokumentiert.

Das Format basiert auf [Keep a Changelog](https://keepachangelog.com/de/1.0.0/),
und dieses Projekt folgt [Semantic Versioning](https://semver.org/lang/de/).

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [0.1.1] - 2025-12-14

### 🇩🇪 Deutsch

####
- ✅ Sprachfehler behoben

### 🇬🇧 English

####
- ✅ Fixed language errors

---

## [0.1.0] - 2025-12-14

### 🇩🇪 Deutsch

#### Hinzugefügt
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

#### Features im Detail

**Smart Activity Switching:**
- Analysiert welche Geräte in beiden Aktivitäten verwendet werden
- Hält gemeinsame Geräte eingeschaltet
- Aktualisiert nur Input-Source und Lautstärke
- Reduziert Wechselzeit von 20-30 Sekunden auf 2-3 Sekunden

**Services:**
- `av_scenes.start_activity` - Aktivität starten
- `av_scenes.stop_activity` - Aktivität stoppen
- `av_scenes.reload` - Konfiguration neu laden

**Dokumentation:**
- README mit Beispielen
- SMART_SWITCHING.md - Technische Dokumentation
- TRANSLATIONS.md - Übersetzungs-Anleitung

---

### 🇬🇧 English

#### Added
- 🎉 Initial release
- ✅ Multi-room support with independent control
- ✅ Activity-based scenes for AV equipment
- ✅ **Smart Activity Switching** - Devices stay on during transitions
- ✅ Automatic volume control per activity
- ✅ Power sequencing with configurable delays
- ✅ Input source management with dropdown selection
- ✅ UI-based configuration (no YAML required)
- ✅ Full German translation
- ✅ English translation
- ✅ Home Assistant area integration
- ✅ Media player picklists
- ✅ Source picklists (automatically loaded from device)
- ✅ Automatic scene generation
- ✅ Activity status switches per room
- ✅ CRUD functionality for rooms, activities and devices
- ✅ Auto-save on configuration changes
- ✅ Auto-reload after config changes

#### Features in Detail

**Smart Activity Switching:**
- Analyzes which devices are used in both activities
- Keeps shared devices powered on
- Only updates input source and volume
- Reduces transition time from 20-30 seconds to 2-3 seconds

**Services:**
- `av_scenes.start_activity` - Start activity
- `av_scenes.stop_activity` - Stop activity
- `av_scenes.reload` - Reload configuration

**Documentation:**
- README with examples
- SMART_SWITCHING.md - Technical documentation
- TRANSLATIONS.md - Translation guide

---

## Roadmap

### 🇩🇪 Deutsch

#### [0.2.0] - Geplant
- Integration weiterer Gerätetypen (Lichter, Rolladen, etc.)
- Erweiterte Bedingungen für Aktivitäten
- Makro-Unterstützung

---

### 🇬🇧 English

#### [0.2.0] - Planned
- Integration of additional device types (lights, covers, etc.)
- Advanced conditions for activities
- Macro support

---

[0.1.0]: https://github.com/mkshb/ha_av_scenes/releases/tag/v0.1.0