# Widgets System - Complete Specification

> This document details all interactive widgets that appear in Leo's chat interface and throughout the app, with specifications for each widget type.

---

## Table of Contents
1. [Widget Architecture](#widget-architecture)
2. [Core Widgets](#core-widgets)
3. [Financial Widgets](#financial-widgets)
4. [Educational Widgets](#educational-widgets)
5. [Action Widgets](#action-widgets)
6. [Future Widget Ideas](#future-widget-ideas)
7. [Technical Implementation](#technical-implementation)

---

## Widget Architecture

### Widget Types

Widgets in LEO serve four purposes:
1. **Display Information**: Show data in visual format (charts, cards)
2. **Enable Actions**: Quick transactions without leaving chat
3. **Educate Users**: Interactive learning components
4. **Celebrate Achievements**: Gamification feedback

### Widget Rendering

```typescript
interface Widget {
  type: WidgetType;
  data: WidgetData;
  actions?: WidgetAction[];
  interactive: boolean;
  size: 'small' | 'medium' | 'large';
}

type WidgetType = 
  | 'stock'
  | 'transfer'
  | 'quiz'
  | 'quiz_question'
  | 'achievement'
  | 'savings_goal'
  | 'spending_chart'
  | 'portfolio_summary'
  | 'news_card'
  | 'comparison_table'
  | 'budget_tracker'
  | 'subscription_card'
  | 'tip_card'
  | 'countdown_timer'
  | 'poll'
  | 'calendar_event'
  | 'document_preview'
  | 'voice_player'
  | 'image_carousel';
```

---

## Core Widgets

### 1. Stock Widget

**Purpose**: Display stock information inline in chat

```
┌─────────────────────────────────────┐
│ ┌────┐  AAPL                       │
│ │ 📈 │  Apple Inc.                  │
│ └────┘                              │
│                                     │
│ €178.50        ▲ +2.3% (+€4.02)    │
│                                     │
│ ┌─────────────────────────────┐    │
│ │ [Sparkline chart - 7 days]   │    │
│ └─────────────────────────────┘    │
│                                     │
│ Leo: "Starke Woche für Apple.      │
│ Das iPhone 15 verkauft sich gut."  │
│                                     │
│ [Kaufen]  [Zur Watchlist]          │
└─────────────────────────────────────┘
```

**Props:**
```typescript
interface StockWidgetProps {
  symbol: string;
  name: string;
  price: number;
  change: number;
  changePercent: number;
  chartData?: number[];
  leoAnalysis?: string;
  actions: ('buy' | 'sell' | 'watchlist')[];
}
```

**Variants:**
- **Compact**: Just price and change
- **Standard**: With chart and analysis
- **Detailed**: Full metrics grid included

---

### 2. Transfer Widget

**Purpose**: Quick money transfer directly from chat

```
┌─────────────────────────────────────┐
│ 💸 Überweisung                      │
│                                     │
│ ┌────┐  Max Mustermann             │
│ │ 👤 │  DE89 3704 •••• 0130 00     │
│ └────┘                              │
│                                     │
│           €800.00                   │
│       ─────────────────            │
│       Verwendungszweck:             │
│       Miete Dezember 🏠             │
│                                     │
│ ┌─────────────────────────────┐    │
│ │    ══════ Senden ══════►    │    │
│ └─────────────────────────────┘    │
│                                     │
│ [Betrag ändern]  [Abbrechen]       │
└─────────────────────────────────────┘
```

**After Successful Transfer:**
```
┌─────────────────────────────────────┐
│           ✅ Gesendet!              │
│                                     │
│        €800.00 an Max              │
│     Miete Dezember                  │
│                                     │
│  Leo: "Erledigt! Soll ich dich     │
│  nächsten Monat wieder erinnern?"   │
│                                     │
│  [Ja, monatlich erinnern]          │
│  [Nein danke]                       │
└─────────────────────────────────────┘
```

**Props:**
```typescript
interface TransferWidgetProps {
  recipient: {
    name: string;
    iban: string;
    avatar?: string;
  };
  amount: number;
  reference?: string;
  isRecurring?: boolean;
  status: 'pending' | 'sent' | 'failed';
  onConfirm: () => void;
  onCancel: () => void;
}
```

---

### 3. Quiz Widget (Preview Card)

**Purpose**: Show quiz invitation before starting

```
┌─────────────────────────────────────┐
│  ⚡ Quiz Challenge                  │
│                                     │
│  🎯 ETFs verstehen                  │
│                                     │
│  • 5 Fragen                         │
│  • ~3 Minuten                       │
│  • Schwierigkeit: Mittel            │
│                                     │
│  ┌─────────────────────────────┐   │
│  │  +75 XP möglich 🏆          │   │
│  └─────────────────────────────┘   │
│                                     │
│  [Quiz starten]                     │
│                                     │
│  Leo: "ETFs sind super für den     │
│  Einstieg. Bereit zu lernen?"      │
└─────────────────────────────────────┘
```

---

### 4. Quiz Question Widget (Active Quiz)

**Purpose**: Display interactive quiz question

```
┌─────────────────────────────────────┐
│  ETFs verstehen         Frage 2/5  │
│  ████████░░░░░░░░░░░░░░    40%    │
│                                     │
│  ⏱️ 0:15                           │
│                                     │
│  Was ist ein Vorteil von ETFs      │
│  gegenüber Einzelaktien?           │
│                                     │
│  ┌─────────────────────────────┐   │
│  │ A) Höhere Rendite garantiert │   │
│  └─────────────────────────────┘   │
│                                     │
│  ┌─────────────────────────────┐   │
│  │ B) Automatische Streuung    │   │ ← selected
│  └─────────────────────────────┘   │
│                                     │
│  ┌─────────────────────────────┐   │
│  │ C) Keine Gebühren           │   │
│  └─────────────────────────────┘   │
│                                     │
│  ┌─────────────────────────────┐   │
│  │ D) Immer steuerfrei         │   │
│  └─────────────────────────────┘   │
│                                     │
│  🏆 Aktuell: 15 Punkte             │
└─────────────────────────────────────┘
```

**Answer Feedback:**
```
┌─────────────────────────────────────┐
│  ✅ Richtig!            +20 Punkte │
│                                     │
│  B) Automatische Streuung          │
│                                     │
│  Leo erklärt:                       │
│  "Genau! ETFs investieren in viele │
│  verschiedene Aktien auf einmal.   │
│  Das reduziert dein Risiko, weil   │
│  nicht alles von einer Firma       │
│  abhängt."                          │
│                                     │
│  [Weiter →]                         │
└─────────────────────────────────────┘
```

---

### 5. Achievement Widget

**Purpose**: Celebrate badge unlocks and milestones

```
┌─────────────────────────────────────┐
│         🎉 BADGE FREIGESCHALTET!   │
│                                     │
│           ┌─────────┐              │
│           │   💎    │              │
│           │ Diamond │              │
│           │  Hands  │              │
│           └─────────┘              │
│                                     │
│  Du hast durch einen 20% Rückgang  │
│  gehalten! Das zeigt echte         │
│  Investoren-Mentalität.            │
│                                     │
│         +300 XP erhalten           │
│                                     │
│  [Badge ausrüsten]  [Später]       │
└─────────────────────────────────────┘
```

---

## Financial Widgets

### 6. Portfolio Summary Widget

**Purpose**: Quick portfolio overview in chat

```
┌─────────────────────────────────────┐
│  📊 Dein Portfolio                  │
│                                     │
│  Gesamtwert:     €12,450.67        │
│  Heute:          +€234.50 (+1.9%)  │
│  Diese Woche:    +€567.80 (+4.7%)  │
│                                     │
│  ┌─────────────────────────────┐   │
│  │ [Pie chart of allocation]   │   │
│  │  Tech: 45% ████████░░       │   │
│  │  ETFs: 30% ██████░░░░       │   │
│  │  Bank: 15% ███░░░░░░░       │   │
│  │  Andere: 10% ██░░░░░░░      │   │
│  └─────────────────────────────┘   │
│                                     │
│  Top Performer: AAPL (+5.2%)       │
│  Schlechtester: TSLA (-2.1%)       │
│                                     │
│  [Portfolio öffnen]                │
└─────────────────────────────────────┘
```

---

### 7. Spending Chart Widget

**Purpose**: Show spending analysis visually

```
┌─────────────────────────────────────┐
│  💳 Ausgabenanalyse                 │
│  November 2025                      │
│                                     │
│  Gesamt: €2,145.67                 │
│  vs. Oktober: ▼ -€234 (-9.8%)      │
│                                     │
│  ┌─────────────────────────────┐   │
│  │ [Horizontal bar chart]      │   │
│  │                             │   │
│  │ Wohnen  ████████████ €850  │   │
│  │ Essen   ██████░░░░░ €420   │   │
│  │ Transport ████░░░░░ €280   │   │
│  │ Freizeit ███░░░░░░ €230    │   │
│  │ Shopping ██░░░░░░░ €180    │   │
│  │ Sonstiges █░░░░░░░ €185    │   │
│  └─────────────────────────────┘   │
│                                     │
│  Leo: "Du hast €67 weniger für     │
│  Essen ausgegeben als letzten      │
│  Monat. Weiter so! 🎉"             │
│                                     │
│  [Details ansehen]                  │
└─────────────────────────────────────┘
```

---

### 8. Savings Goal Widget

**Purpose**: Show progress toward a savings goal

```
┌─────────────────────────────────────┐
│  🎯 Sparziel: Urlaub 2026          │
│                                     │
│  ┌─────────────────────────────┐   │
│  │ 🏖️ [Goal image]             │   │
│  └─────────────────────────────┘   │
│                                     │
│  €850 / €2,000                     │
│  ████████░░░░░░░░░░░░░░░   42.5%  │
│                                     │
│  📅 Zieldatum: August 2026         │
│  💰 Empfohlen: €115/Monat          │
│  📈 Aktuell sparst du: €100/Monat  │
│                                     │
│  Leo: "Du brauchst €15 mehr pro    │
│  Monat um dein Ziel zu erreichen.  │
│  Soll ich dir Spartipps zeigen?"   │
│                                     │
│  [Sparrate erhöhen]  [Tipps]       │
└─────────────────────────────────────┘
```

---

### 9. Subscription Card Widget

**Purpose**: Display subscription with AI analysis

```
┌─────────────────────────────────────┐
│  🔴 Abo-Warnung                     │
│                                     │
│  ┌────┐  Netflix                   │
│  │ 🎬 │  Premium                    │
│  └────┘  €17.99/Monat              │
│                                     │
│  ⚠️ Nicht genutzt seit 45 Tagen   │
│                                     │
│  Bisherige Kosten: €215.88         │
│  Bei Kündigung sparst du:          │
│  €215.88/Jahr                       │
│                                     │
│  Leo: "Du zahlst für Netflix, aber │
│  schaust nichts. Soll ich für dich │
│  kündigen?"                         │
│                                     │
│  [Jetzt kündigen]  [Behalten]      │
└─────────────────────────────────────┘
```

---

### 10. Budget Tracker Widget

**Purpose**: Real-time budget status

```
┌─────────────────────────────────────┐
│  📊 Wochenbudget                    │
│                                     │
│  Essen & Trinken                    │
│  ████████████░░░░░░░░  €67 / €100 │
│  ▲ 67% verbraucht                   │
│                                     │
│  Shopping                           │
│  ████████████████████  €150 / €150│
│  ⚠️ Budget erreicht!               │
│                                     │
│  Freizeit                           │
│  ████████░░░░░░░░░░░░  €40 / €100 │
│  ✓ Im Rahmen                        │
│                                     │
│  Leo: "Dein Shopping-Budget ist    │
│  aufgebraucht. Noch 3 Tage bis     │
│  zur nächsten Woche!"              │
│                                     │
│  [Budgets anpassen]                 │
└─────────────────────────────────────┘
```

---

## Educational Widgets

### 11. Tip Card Widget

**Purpose**: Show financial tips and explanations

```
┌─────────────────────────────────────┐
│  💡 Leo's Tipp                      │
│                                     │
│  Wusstest du?                       │
│                                     │
│  Die 72er-Regel hilft dir zu       │
│  berechnen, wann sich dein Geld    │
│  verdoppelt:                        │
│                                     │
│  72 ÷ Zinssatz = Jahre             │
│                                     │
│  Bei 3% Zinsen:                     │
│  72 ÷ 3 = 24 Jahre                 │
│                                     │
│  [Das verstehe ich ✓]              │
│  [Mehr erklären]                    │
│  [Quiz dazu +25 XP]                │
└─────────────────────────────────────┘
```

---

### 12. Comparison Table Widget

**Purpose**: Compare financial products

```
┌─────────────────────────────────────┐
│  📋 Vergleich: ETFs vs Aktien      │
│                                     │
│          │ ETF     │ Einzelaktie  │
│  ────────┼─────────┼──────────────│
│  Risiko  │ ⚠️ Mittel│ ⚠️⚠️ Höher   │
│  Kosten  │ 💰 Gering│ 💰💰 Höher   │
│  Streuung│ ✅ Ja    │ ❌ Nein      │
│  Aufwand │ 📉 Gering│ 📈 Mehr      │
│  Rendite │ 📊 Markt │ 📊 Variabel │
│                                     │
│  Leo's Empfehlung für Anfänger:    │
│  "Starte mit einem ETF auf den     │
│  MSCI World. Das ist wie ein       │
│  Obstkorb statt nur ein Apfel!"    │
│                                     │
│  [ETFs erkunden]  [Mehr lernen]    │
└─────────────────────────────────────┘
```

---

## Action Widgets

### 13. Poll Widget

**Purpose**: Quick user feedback in chat

```
┌─────────────────────────────────────┐
│  📊 Kurze Frage                     │
│                                     │
│  Wie viel sparst du monatlich?     │
│                                     │
│  [  ] Unter €50                    │
│  [✓] €50 - €200                    │ ← selected
│  [  ] €200 - €500                  │
│  [  ] Über €500                    │
│  [  ] Ich spare (noch) nicht       │
│                                     │
│  12.847 haben abgestimmt           │
│                                     │
│  [Ergebnisse anzeigen]             │
└─────────────────────────────────────┘
```

**After Voting:**
```
┌─────────────────────────────────────┐
│  📊 Ergebnisse                      │
│                                     │
│  Unter €50    ████░░░░░░  18%     │
│  €50-200      █████████░  42% ←Du │
│  €200-500     █████░░░░░  28%     │
│  Über €500    █░░░░░░░░░   7%     │
│  Nichts       █░░░░░░░░░   5%     │
│                                     │
│  Leo: "Du bist im Durchschnitt!    │
│  Mit €150/Monat könntest du in     │
│  10 Jahren €25.000 haben."         │
│                                     │
│  [Rechner öffnen]                   │
└─────────────────────────────────────┘
```

---

### 14. Calendar Event Widget

**Purpose**: Schedule financial reminders

```
┌─────────────────────────────────────┐
│  📅 Erinnerung erstellt            │
│                                     │
│  🏠 Mietüberweisung                │
│                                     │
│  Datum: Jeden 1. des Monats        │
│  Zeit: 9:00 Uhr                    │
│  Betrag: €800                       │
│  An: Max Mustermann                 │
│                                     │
│  Nächste: 1. Dezember 2025         │
│                                     │
│  [Bearbeiten]  [Löschen]           │
└─────────────────────────────────────┘
```

---

### 15. Document Preview Widget

**Purpose**: Show scanned/uploaded document analysis

```
┌─────────────────────────────────────┐
│  📄 Dokument analysiert            │
│                                     │
│  ┌─────────────────────────────┐   │
│  │ [Document thumbnail]         │   │
│  │ Stromrechnung_Nov.pdf       │   │
│  └─────────────────────────────┘   │
│                                     │
│  Erkannt: Stromrechnung            │
│  Anbieter: Stadtwerke München      │
│  Betrag: €127.50                    │
│  Fällig: 15.12.2025                │
│                                     │
│  Leo: "€127.50 ist 15% mehr als    │
│  letzten Monat. Heizung an? ❄️"    │
│                                     │
│  [Überweisung vorbereiten]         │
│  [Anbieter vergleichen]            │
│  [Dokument speichern]              │
└─────────────────────────────────────┘
```

---

## Future Widget Ideas

### 16. Voice Player Widget (Future)
```
┌─────────────────────────────────────┐
│  🔊 Leo spricht...                  │
│                                     │
│  ▶️ ═══════════●══════════ 1:24   │
│                                     │
│  [Transkript anzeigen]             │
└─────────────────────────────────────┘
```

### 17. AR Portfolio Widget (Future)
```
Concept: Augmented Reality view of portfolio
- Point phone at table
- See 3D pie chart of holdings
- Tap stocks for details
```

### 18. Social Comparison Widget (Future - with consent)
```
┌─────────────────────────────────────┐
│  👥 Vergleich (anonym)             │
│                                     │
│  Du sparst mehr als 65% der        │
│  Nutzer in deinem Alter!           │
│                                     │
│  [█████████████████░░░] 65%       │
│                                     │
│  Du investierst mehr als 78%!      │
│  [████████████████████░] 78%      │
│                                     │
│  Leo: "Super Arbeit! Du bist       │
│  deinen Altersgenossen voraus."    │
└─────────────────────────────────────┘
```

### 19. Bill Splitting Widget (Future)
```
┌─────────────────────────────────────┐
│  🧾 Rechnung teilen                │
│                                     │
│  Restaurant Le Petit               │
│  Gesamt: €120.00                   │
│                                     │
│  Teilen mit:                        │
│  ┌──────────────────────────┐      │
│  │ 👤 Du        €40.00     │      │
│  │ 👤 Anna      €40.00     │      │
│  │ 👤 Max       €40.00     │      │
│  └──────────────────────────┘      │
│                                     │
│  [Anfrage senden]                   │
└─────────────────────────────────────┘
```

### 20. Crypto Price Widget (Future - if ING adds crypto)
```
┌─────────────────────────────────────┐
│  ₿ Bitcoin                          │
│                                     │
│  €41,234.56     ▲ +3.2%            │
│                                     │
│  ⚠️ Krypto ist sehr volatil!       │
│                                     │
│  Leo: "Investiere nur Geld, das    │
│  du zu verlieren bereit bist."     │
│                                     │
│  [Mehr über Krypto lernen]         │
└─────────────────────────────────────┘
```

---

## Technical Implementation

### Widget Component Structure

```typescript
// Base widget wrapper
interface WidgetProps {
  type: WidgetType;
  data: any;
  size: 'small' | 'medium' | 'large';
  onAction?: (action: string, data?: any) => void;
}

// Widget registry
const WIDGET_COMPONENTS: Record<WidgetType, React.ComponentType> = {
  stock: StockWidget,
  transfer: TransferWidget,
  quiz: QuizWidget,
  quiz_question: QuizQuestionWidget,
  achievement: AchievementWidget,
  savings_goal: SavingsGoalWidget,
  spending_chart: SpendingChartWidget,
  portfolio_summary: PortfolioSummaryWidget,
  news_card: NewsCardWidget,
  comparison_table: ComparisonTableWidget,
  budget_tracker: BudgetTrackerWidget,
  subscription_card: SubscriptionCardWidget,
  tip_card: TipCardWidget,
  countdown_timer: CountdownTimerWidget,
  poll: PollWidget,
  calendar_event: CalendarEventWidget,
  document_preview: DocumentPreviewWidget,
  voice_player: VoicePlayerWidget,
  image_carousel: ImageCarouselWidget,
};

// Render widget from AI response
function renderWidget(widget: Widget): React.ReactNode {
  const Component = WIDGET_COMPONENTS[widget.type];
  if (!Component) return null;
  
  return (
    <WidgetWrapper size={widget.size}>
      <Component {...widget.data} onAction={widget.onAction} />
    </WidgetWrapper>
  );
}
```

### AI Widget Generation

GPT-4 can generate widgets based on conversation context:

```typescript
// System prompt for widget generation
const WIDGET_SYSTEM_PROMPT = `
You are Leo, a financial AI assistant. When appropriate, you can display 
interactive widgets in your responses.

Available widgets:
- stock: Show stock price and info
- transfer: Quick money transfer
- quiz: Start a financial quiz
- achievement: Celebrate unlocked badge
- savings_goal: Show progress toward goal
- spending_chart: Visualize spending
- portfolio_summary: Show portfolio overview
- tip_card: Display financial tip

To include a widget, add a JSON block:
\`\`\`widget
{
  "type": "stock",
  "data": {
    "symbol": "AAPL",
    "price": 178.50,
    "change": 2.3
  }
}
\`\`\`

Only show widgets when they add value to the conversation.
`;
```

### Widget Animation System

```typescript
// Framer Motion variants for widget animations
const widgetVariants = {
  initial: { opacity: 0, y: 20, scale: 0.95 },
  animate: { 
    opacity: 1, 
    y: 0, 
    scale: 1,
    transition: { type: "spring", damping: 20, stiffness: 300 }
  },
  exit: { 
    opacity: 0, 
    scale: 0.9,
    transition: { duration: 0.2 }
  }
};

// Achievement celebration animation
const celebrationVariants = {
  initial: { scale: 0, rotate: -180 },
  animate: { 
    scale: [0, 1.2, 1], 
    rotate: 0,
    transition: { 
      type: "spring",
      damping: 10,
      stiffness: 200
    }
  }
};
```

---

*Last Updated: November 2025*
