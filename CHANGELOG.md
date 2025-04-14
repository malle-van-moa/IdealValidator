# Changelog

Alle wichtigen Änderungen am Projekt werden in dieser Datei dokumentiert.

Das Format basiert auf [Keep a Changelog](https://keepachangelog.com/de/1.0.0/),
und dieses Projekt folgt [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added
- Initiale Projektstruktur nach Clean Architecture Prinzipien
- README.md mit Projektbeschreibung und -zielen
- CHANGELOG.md für die Dokumentation von Änderungen
- Verzeichnisstruktur für Frontend (React/Next.js) und Backend
- Dokumentationsverzeichnis für Architekturdiagramme

## Richtlinien zur Pflege des Changelogs

### Einträge Format
- Jede Version sollte folgende Kategorien enthalten (wenn zutreffend):
  - `Added` für neue Features
  - `Changed` für Änderungen an bestehender Funktionalität
  - `Deprecated` für Features, die in zukünftigen Versionen entfernt werden
  - `Removed` für Features, die in dieser Version entfernt wurden
  - `Fixed` für Bugfixes
  - `Security` für Sicherheitsupdates

### Wann Aktualisieren
- Bei jedem Pull Request muss der Changelog aktualisiert werden
- Bei direkten Commits in den Hauptbranch muss der Changelog aktualisiert werden
- Kleinere Dokumentationsänderungen erfordern keinen Changelog-Eintrag

### Versioning
- Major Version (x.0.0): Inkompatible API-Änderungen
- Minor Version (0.x.0): Funktionalität hinzugefügt, die abwärtskompatibel ist
- Patch Version (0.0.x): Abwärtskompatible Bugfixes

### Prozess
1. Füge Änderungen im Abschnitt [Unreleased] hinzu
2. Bei einem Release, benenne [Unreleased] in die neue Versionsnummer um
3. Füge ein neues [Unreleased] für zukünftige Änderungen hinzu 