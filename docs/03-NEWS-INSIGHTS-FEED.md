# News & Insights Feed - Vollständige Spezifikation

> Dieses Dokument beschreibt das personalisierte News-Feed-System mit Perplexity-ähnlicher KI-Zusammenfassung, aktienspezifischen Nachrichten und "Für Dich" Seite.

---

## Inhaltsverzeichnis
1. [Übersicht](#übersicht)
2. [News-Quellen & Integration](#news-quellen--integration)
3. [KI-Zusammenfassung](#ki-zusammenfassung)
4. [Für Dich Seite](#für-dich-seite)
5. [Aktien-spezifische News](#aktien-spezifische-news)
6. [Benachrichtigungssystem](#benachrichtigungssystem)
7. [UI Spezifikationen](#ui-spezifikationen)
8. [User Stories für Demo](#user-stories-für-demo)

---

## Übersicht

Das LEO News-System liefert personalisierte Finanznachrichten die:
- **Relevant sind**: Gefiltert basierend auf Portfolio und Watchlist
- **Verständlich sind**: KI-zusammengefasst in einfacher Sprache
- **Handlungsfähig sind**: Verbunden mit tatsächlichen Investments des Nutzers
- **Aktuell sind**: Echtzeit-Alerts für Portfolio-beeinflussende News

### Kernprinzipien

1. **Kein Rauschen**: Nur News zeigen die für den Nutzer wichtig sind
2. **Kontext zuerst**: Erklären WARUM diese News für sie relevant ist
3. **Leo erklärt**: Jeder Artikel kann mit Leos Analyse erweitert werden
4. **Handlungsorientiert**: Klare nächste Schritte wenn relevant

---

## News-Quellen & Integration

### Empfohlene News APIs

| Anbieter | Vorteile | Nachteile | Kosten |
|----------|----------|-----------|--------|
| **NewsAPI** | Breite Abdeckung, einfache Integration | Rate Limits | Kostenlose Stufe + kostenpflichtig |
| **Alpha Vantage** | Finanzfokus, Aktien-Daten enthalten | Begrenzte Artikel | Kostenlose Stufe |
| **Bloomberg API** | Premium-Inhalte, maßgeblich | Teuer | Enterprise |
| **Reuters API** | Echtzeit, vertrauenswürdig | Teuer | Enterprise |
| **Yahoo Finance** | Kostenlos, gute Aktienabdeckung | Weniger Premium-Inhalte | Kostenlos |

### Deutsche Nachrichtenquellen zum Aggregieren

| Quelle | Typ | RSS/API |
|--------|-----|---------|
| Handelsblatt | Wirtschaftsnachrichten | RSS |
| Börsen-Zeitung | Aktienmarkt | RSS |
| Finanznachrichten | Finanzen | RSS |
| Der Aktionär | Aktientipps | RSS |
| Wirtschaftswoche | Wirtschaft | RSS |
| FAZ Finanzen | Finanzbereich | RSS |
| Manager Magazin | Wirtschaft | RSS |
| finanztreff.de | Marktnews | RSS |

---

## KI-Zusammenfassung

### Zusammenfassungs-Pipeline



### GPT Prompt für Zusammenfassung



### Zusammenfassungs-Level nach Profil

**Junior Profil:**


**Adult Profil:**


---

## Für Dich Seite

### Perplexity-Style Design

Die "Für Dich" Seite aggregiert und präsentiert News wie Perplexitys Discover Feature:



### Für Dich Feed Kategorien

| Kategorie | Icon | Kriterien |
|-----------|------|-----------|
| **Wichtig für Dich** | 🔴 | Score > 80, betrifft Portfolio |
| **Deine Aktien** | 📈 | Erwähnt besessene Aktien |
| **Deine Watchlist** | 👀 | Erwähnt Watchlist-Aktien |
| **Marktnews** | 📊 | Allgemeine Markt-Updates |
| **Lernen** | 📚 | Bildungsinhalte |
| **Quiz verfügbar** | 🎯 | Hat angehängtes Quiz |

---

## Aktien-spezifische News

### News auf Aktien-Detailseite

Beim Ansehen einer Aktie zeige dedizierte News-Sektion:



---

## Benachrichtigungssystem

### News Benachrichtigungstypen

#### 1. Eilmeldung (Sofort)


#### 2. Portfolio-Alert (Hohe Priorität)


#### 3. Tageszusammenfassung (Geplant)


#### 4. Lernmöglichkeit (Kontextuell)


---

## User Stories für Demo

### Story 1: Portfolio-relevanter News Alert


### Story 2: Tägliche News Zusammenfassung


### Story 3: Aus News lernen


---

## Tracking-Limitierungen

### Was KANN verfolgt werden:
- Abonnement-Zahlungen
- Letztes Zahlungsdatum
- Preiserhöhungen
- Doppelte Dienste (Spotify + Apple Music)

### Was NICHT verfolgt werden kann:
- Externe App-Nutzung (Fitnessstudio-Besuche)
- Tatsächlicher Verbrauch (Netflix Schauzeit)
- Cookie-basiertes Tracking (nicht empfohlen - Datenschutz)

### Workaround für "ungenutzte" Erkennung:
Nur zahlungsbasierte Erkennung ist möglich. Für Fitnessstudio: Wenn Nutzer €50 monatlich an "Fitness Studio" zahlt aber keine anderen fitnessbezogenen Käufe (Protein, Nahrungsergänzung, etc.), kann Leo vorschlagen, die Mitgliedschaft zu überprüfen.

---

*Zuletzt aktualisiert: November 2025*
