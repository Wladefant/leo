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

```
┌─────────────────────────────────────────────────────────────┐
│                    News-Verarbeitungs-Pipeline              │
├─────────────────────────────────────────────────────────────┤
│  1. RSS/API Aggregation                                     │
│     ↓ (alle 15 Min)                                         │
│  2. Duplikat-Erkennung (ähnliche Artikel gruppieren)        │
│     ↓                                                       │
│  3. Relevanz-Scoring (basierend auf Portfolio/Watchlist)    │
│     ↓                                                       │
│  4. GPT-4 Zusammenfassung (profilabhängig)                  │
│     ↓                                                       │
│  5. Quiz-Potential prüfen (für Juniors)                     │
│     ↓                                                       │
│  6. Auslieferung an Feed / Push-Notification                │
└─────────────────────────────────────────────────────────────┘
```

### GPT Prompt für Zusammenfassung

```
System: Du bist Leo, ein freundlicher Finanz-Assistent für die ING Banking App.
Fasse Finanznachrichten zusammen für {PROFIL}-Nutzer.

Regeln:
- Maximal 3 Sätze für Zusammenfassung
- Keine Anlageempfehlungen
- Keine Fachbegriffe ohne Erklärung
- Erkläre WARUM die News relevant sein könnte
- Bei {PROFIL} = "Junior": Besonders einfache Sprache, nutze Analogien

Eingabe-Artikel: {ARTIKEL_TEXT}
Portfolio-Kontext: {USER_PORTFOLIO}
Watchlist: {USER_WATCHLIST}

Ausgabe als JSON:
{
  "summary": "...",
  "relevance_reason": "...",
  "learning_opportunity": true/false,
  "suggested_quiz_topic": "..." (optional)
}
```

### Zusammenfassungs-Level nach Profil

**Junior Profil:**
```
Originalnachricht: "Die EZB hat heute den Leitzins um 25 Basispunkte 
auf 4,25% angehoben, was Analysten als Reaktion auf die anhaltende 
Inflation im Euroraum interpretieren."

Leo-Zusammenfassung: "Die Zentralbank in Europa hat die Zinsen 
etwas erhöht 📈 Das bedeutet: Sparen lohnt sich mehr, aber Kredite 
werden teurer. Stell dir vor, die Bank gibt dir mehr Taschengeld 
fürs Sparen! Möchtest du mehr über Zinsen lernen? [Quiz starten]"
```

**Adult Profil:**
```
Originalnachricht: "Die EZB hat heute den Leitzins um 25 Basispunkte 
auf 4,25% angehoben, was Analysten als Reaktion auf die anhaltende 
Inflation im Euroraum interpretieren."

Leo-Zusammenfassung: "Die EZB erhöht den Leitzins auf 4,25%. 
Für dich relevant: Dein Tagesgeld könnte bald mehr Zinsen bringen, 
aber dein variabler Kredit wird teurer. Soll ich deine Konten 
darauf prüfen?"
```


---

## Für Dich Seite

### Perplexity-Style Design

Die "Für Dich" Seite aggregiert und präsentiert News wie Perplexitys Discover Feature:

```
┌─────────────────────────────────────┐
│  Für Dich                     🔔    │
├─────────────────────────────────────┤
│  ┌────────────────────────────────┐ │
│  │ 🔴 WICHTIG                     │ │
│  │ Apple fällt 5% nach iPhone-   │ │
│  │ Verkaufsprognose             │ │
│  │                               │ │
│  │ Betrifft dein Portfolio:      │ │
│  │ 3 AAPL Aktien (-€26,70)      │ │
│  │                               │ │
│  │ [Leo fragen] [Details]        │ │
│  └────────────────────────────────┘ │
│                                     │
│  📈 Deine Aktien                    │
│  ├─ Microsoft übertrifft Erwartungen│
│  ├─ NVIDIA stellt neuen Chip vor   │
│  └─ [Mehr anzeigen]                │
│                                     │
│  👀 Deine Watchlist                 │
│  ├─ Tesla beginnt Auslieferung...  │
│  └─ Amazon expandiert nach...      │
│                                     │
│  📚 Für dich zum Lernen            │
│  ├─ Was sind ETFs? [Quiz] 🎯       │
│  └─ Wie funktionieren Dividenden?  │
└─────────────────────────────────────┘
```



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

```
┌─────────────────────────────────────┐
│  Apple Inc. (AAPL)                  │
│  $178,50  +1,2% 📈                  │
├─────────────────────────────────────┤
│  [Chart] [Details] [News] [Leo]    │
├─────────────────────────────────────┤
│  📰 Aktuelle News zu Apple         │
│                                     │
│  ┌────────────────────────────────┐ │
│  │ vor 2 Std. • Handelsblatt     │ │
│  │ Apple kündigt Vision Pro       │ │
│  │ Deutschland-Start an          │ │
│  │                               │ │
│  │ Leo: "Das neue VR-Headset     │ │
│  │ könnte Umsatz steigern, aber  │ │
│  │ der Preis (€3.500) limitiert  │ │
│  │ die Zielgruppe. Langfristig   │ │
│  │ interessant."                  │ │
│  │                               │ │
│  │ [Vollständigen Artikel lesen] │ │
│  └────────────────────────────────┘ │
│                                     │
│  vor 5 Std. • Reuters              │
│  iPhone 16 Vorbestellungen stark   │
│                                     │
│  vor 1 Tag • Der Aktionär          │
│  Analysten erhöhen Kursziel        │
└─────────────────────────────────────┘
```



---

##### Watchlist-basierte Micro-News (1-Satz-News)

Leo überwacht die persönliche Watchlist der Nutzer:innen und liefert extrem kurze,
leicht konsumierbare News-Updates zu relevanten Assets.

- Quellen ausschließlich große, vertrauenswürdige Medien
- Sehr aktuelle Meldungen (Minuten–Stunden alt)
- Jede News wird auf einen Satz reduziert
- Präsentation als dezente Push-Benachrichtigung oder Insight-Card
- Keine Empfehlungen, nur faktenbasierte Information

**Beispiele**
• "Apple kündigt neues Produkt an – Aktie reagiert leicht positiv."  
• "EZB signalisiert mögliche Zinssenkung – Bankensektor steigt."  
• "Tesla meldet Lieferengpass bei Batterien – betrifft mehrere Zulieferer."

##### News → Lernmodul (Micro-Learning Fusion)

Wenn Leo eine News zusammenfasst, bietet er optional eine passende
Lerneinheit an, damit Nutzer:innen den Kontext besser verstehen.

**Beispiele**
• News: "Tech-Aktien fallen heute stark."  
  Lernmodul: "Warum reagiert der Markt stark auf Zinsänderungen? (2 Minuten)"

• News: "Pharmaunternehmen A genehmigt neues Medikament."  
  Lernmodul: "Wie funktionieren regulatorische Freigaben?"

• News: "Halbleiter-Lieferketten unter Druck."  
  Lernmodul: "Was sind die wichtigsten Rohstoffe für Chips?"


##### Branchen- & Lieferketten-Kontext (kein Investment-Ratschlag)

Leo erklärt wirtschaftliche Zusammenhänge, ohne Empfehlungen auszusprechen.
Wenn eine Firma ein neues Produkt, Medikament oder einen Chip entwickelt,
erklärt Leo, welche Branchen typischerweise davon beeinflusst werden könnten.

Beispiele:
• "Unternehmen X hat einen neuen KI-Chip vorgestellt. Solche Chips benötigen
  seltene Metalle wie Y oder Z. Deshalb reagieren oft auch Unternehmen aus der
  Rohstoff- oder Halbleiter-Lieferkette."
• "Ein neues Medikament von Firma A könnte die Nachfrage nach bestimmten
  Chemikalien oder Biotech-Zulieferern erhöhen."
• "Wenn Autohersteller verstärkt auf Batterien setzen, profitieren oft
  Lithium- oder Recycling-Unternehmen in der Lieferkette."

Wichtig:
Leo erklärt nur Zusammenhänge.  
Er macht *keine* Kauf- oder Verkaufsvorschläge.
Er bietet Lernmodule oder Erklärungen an, damit Nutzer:innen verstehen,
wie Märkte miteinander verknüpft sind.

##### Sentiment-basierte Marktstimmung (neutral & erklärend)

Leo liefert eine kurze, faktenbasierte Einordnung der Marktstimmung,
ohne Empfehlungen oder Interpretationen für Anlageentscheidungen.

- „Markt heute überwiegend negativ aufgrund Makro-Daten.“
- „Tech-Sektor zeigt leichte Erholung nach gestrigen Verlusten.“
- „Banken stabil, da EZB keine Änderungen signalisiert.“

Jeder Satz erklärt **nur**, was gerade passiert – nicht, was Nutzer:innen tun sollen.

---

##### Risk-Signals (reine Kontextwarnungen, keine Handlungsempfehlungen)

Leo weist auf potenziell erhöhte Marktbewegungen hin,
wenn relevante News auf der Watchlist oder im Portfolio erscheinen.

- „Hohe Volatilität möglich: Unternehmen X veröffentlicht heute Quartalszahlen.“
- „Chip-Lieferkette unter Druck – kurzfristige Preisschwankungen üblich.“
- „Branchenrotation wahrscheinlich: Inflation höher als erwartet.“

Wichtig:  
Diese Hinweise dienen ausschließlich der Orientierung,
nicht der Ableitung von Anlage-Strategien.

---

##### Event-getriebene Alerts (faktenbasiert)

Leo erkennt wichtige Markttermine und liefert kurze Ein-Satz-Updates:

- **Earnings:** „Apple veröffentlicht heute Ergebnisse – Markt erwartet hohe Spannung.“  
- **Dividenden:** „Firma Y erhöht die Dividende um 4 %.“  
- **Zinsentscheidungen:** „EZB gibt Zinsentscheidung um 14:30 Uhr bekannt.“  
- **Makro-Daten:** „US-Inflationsrate steigt leicht – Markt reagiert gemischt.“

Alles wird neutral erklärt, ohne Bewertung oder Empfehlung.

---

##### Beginner-Modus Erklärungen („Was bedeutet das?“)

Für Nutzer:innen mit wenig Finanzwissen erklärt Leo
komplexe Begriffe in einfacher Sprache.

Beispiele:
- „Zinsentscheidung: Die Zentralbank entscheidet, wie teuer Kredite werden.“
- „Earnings: Quartalsberichte, die zeigen, wie viel eine Firma verdient hat.“
- „Volatilität: Wenn Kurse schnell steigen oder fallen.“

Leo bietet optional ein **2-Minuten-Lernmodul** an.

---

##### Smart Ranking & Noise Reduction

Der News-Feed nutzt ein KI-basiertes Relevanzmodell, das:

- unwichtige Artikel herausfiltert  
- dubiose Quellen ignoriert  
- Trends erkennt, die für das Portfolio relevant sein *könnten*  
- Meldungen priorisiert, die Kontext, Risiko oder Bildung fördern

Ziel: **Nur wirklich relevante News. Keine Informationsüberflutung.**

---

##### Deep-Dive Erklärungen („Erklär mir warum das wichtig ist“)

Auf Wunsch liefert Leo eine kurze, neutrale Tiefenanalyse:

- „Warum könnte diese News Auswirkungen auf Lieferketten haben?“  
- „Welche typischen Reaktionen zeigt der Markt bei solchen Ereignissen?“  
- „Welche Branchen sind normalerweise betroffen?“

Das ist reine Bildung – **keine Handlungsempfehlung**.


**Beispiel - Echtzeit-Ausgabenalarm:**
```
[Nutzer hat gerade €45 in einem Restaurant bezahlt]

Leo erscheint dezent am unteren Bildschirmrand:
"Essen gehen diese Woche: €127 💸
Das sind 40% mehr als üblich.

Soll ich das genauer verfolgen?
[Ja, Alarm setzen] [Nein, genieße das Leben!]"
```

## Benachrichtigungssystem

### News Benachrichtigungstypen

#### 1. Eilmeldung (Sofort)

**Wann**: Wichtige News die Portfolio betrifft (Score > 80)
```
┌─────────────────────────────────────┐
│  🔴 LEO • Eilmeldung                │
│                                     │
│  Apple fällt 8% nach Gewinnwarnung │
│                                     │
│  Du besitzt 3 AAPL (-€42,60)       │
│                                     │
│  [Details ansehen]                  │
└─────────────────────────────────────┘
```

#### 2. Portfolio-Alert (Hohe Priorität)

**Wann**: Aktie in Portfolio bewegt sich > 5% oder News erwähnt eigene Aktien
```
┌─────────────────────────────────────┐
│  📈 LEO • Portfolio-Update          │
│                                     │
│  NVIDIA steigt 6% nach Quartalszahl│
│                                     │
│  Dein Portfolio heute: +€156,80    │
│                                     │
│  [Portfolio öffnen]                 │
└─────────────────────────────────────┘
```

#### 3. Tageszusammenfassung (Geplant)

**Wann**: Jeden Abend um 19:00 oder morgens um 8:00 (einstellbar)
```
┌─────────────────────────────────────┐
│  📊 LEO • Dein Tag in 30 Sekunden   │
│                                     │
│  3 News für dich heute:            │
│  • Apple: Neues iPhone angekündigt │
│  • DAX schließt 0,8% im Plus      │
│  • EZB Entscheidung morgen         │
│                                     │
│  Portfolio: +€23,40 (+0,5%)        │
│                                     │
│  [Zusammenfassung lesen]           │
└─────────────────────────────────────┘
```

#### 4. Lernmöglichkeit (Kontextuell)

**Wann**: Nach relevanter News, wenn Lernmodul verfügbar
```
┌─────────────────────────────────────┐
│  📚 LEO • Lernchance                │
│                                     │
│  Du hast über Zinsentscheidungen   │
│  gelesen. Möchtest du verstehen    │
│  wie Zinsen Aktien beeinflussen?   │
│                                     │
│  [2-Min Quiz starten] [Später]     │
└─────────────────────────────────────┘
```


---

## User Stories für Demo

### Story 1: Watchlist-basiertes Micro-News Alert
Trigger: Nutzer hat eine Aktie in der Watchlist (z. B. NVIDIA)

Ablauf:
1. Leo erkennt relevante News aus vertrauenswürdigen Quellen.
2. Push: „TSMC meldet höhere Chip-Nachfrage – betrifft mehrere KI-Zulieferer.“
3. Nutzer öffnet die App → Leo zeigt neutralen Kontext.
4. Optionaler Button: „Lerne in 2 Minuten, wie Chip-Lieferketten funktionieren.“

Demonstriert:
• 1-Satz-News  
• Watchlist-Personalisierung  
• Micro-Learning Fusion  
• Keine Handlungsempfehlungen  
---

### Story 2: Event-getriebener Alert (Earnings Day)
Trigger: Heute Quartalszahlen für eine Aktie im Portfolio (z. B. Apple)

Ablauf:
1. 08:00 — Leo sendet Hinweis:
   „⚠️ Apple veröffentlicht heute Quartalszahlen. Marktbewegungen möglich.“
2. Nutzer öffnet die App.
3. Leo erklärt:
   „Earnings sind Quartalsberichte, die zeigen, wie viel eine Firma verdient hat.“
4. Optional: „Willst du verstehen, warum Earnings den Markt bewegen? (2 Minuten Modul)“

Demonstriert:
• Risk Signals  
• Earnings-Events  
• Beginner-Erklärungen  
---

### Story 3: Daily News Zusammenfassung (Für-Dich Feed)
Trigger: Abends um 19:00

Ablauf:
1. Leo erstellt eine personalisierte Tageszusammenfassung:
   • „Tech-Sektor zeigt leichte Erholung.“
   • „EZB signalisiert stabile Zinsen.“
   • „Deine Watchlist: Tesla +1,2 % nach Batterienews.“
2. Nutzer kann auswählen:
   [Mehr lesen] [Warum ist das relevant?] [2-Minuten-Modul starten]

Demonstriert:
• Sentiment-basierte Marktstimmung  
• Aggregierte News („Für Dich“-Seite)  
• Noise Reduction / Smart Ranking  
---

### Story 4: Lernmodul aus News heraus („Was bedeutet das?“)
Trigger: Nutzer sieht News, versteht sie aber nicht

Ablauf:
1. Nutzer tippt auf „Was bedeutet das?“
2. Leo erklärt:
   „Volatilität bedeutet, dass Kurse sich schnell bewegen.“
3. Optional:
   „Willst du ein 2-Minuten-Lernmodul darüber?“

Demonstriert:
• Beginner-Modus  
• Micro-Learning Fusion  
• Konversationelle Erklärungen  

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
