# Future Vision & Roadmap

> This document outlines features planned for future releases, technical considerations, and the long-term vision for LEO.

---

## Table of Contents
1. [Implementation Phases](#implementation-phases)
2. [Future Features](#future-features)
3. [Technical Considerations](#technical-considerations)
4. [Personalized UI Vision](#personalized-ui-vision)
5. [API & Integration Roadmap](#api--integration-roadmap)

---

## Implementation Phases

### Phase 1: MVP (Month 0-6)
**Focus**: Core functionality and basic AI chat

| Feature | Priority | Status |
|---------|----------|--------|
| Leo Chat Interface | High | 🟡 Partial |
| Basic Quiz System | High | 🟡 Partial |
| Junior Dashboard | High | 🟡 Partial |
| Adult Dashboard | High | 🟡 Partial |
| Profile Switching | High | ✅ Done |
| Transaction Display | High | ✅ Done |
| Stock View | Medium | ✅ Done |
| Demo Sidebar | Medium | ✅ Done |

### Phase 2: Enhanced Learning (Month 6-12)
**Focus**: AI-powered education and gamification

| Feature | Priority | Status |
|---------|----------|--------|
| AI-Generated Quizzes | High | 🔴 Not started |
| Adaptive Difficulty | High | 🔴 Not started |
| Kahoot-Style Challenges | High | 🔴 Not started |
| Leaderboards | Medium | 🟡 Partial |
| Achievement System | Medium | 🟡 Partial |
| Points & XP Tracking | Medium | 🔴 Not started |
| School Registration | Low | 🔴 Not started |

### Phase 3: Smart Finance (Month 12-18)
**Focus**: Intelligent financial assistance

| Feature | Priority | Status |
|---------|----------|--------|
| Smart Notifications | High | 🔴 Not started |
| Spending Analysis | High | 🟡 Partial |
| Subscription Detection | Medium | 🟡 Partial |
| Document Scanning | Medium | 🔴 Not started |
| Budget Tracking | Medium | 🔴 Not started |
| Bill Negotiation Tips | Low | 🔴 Not started |

### Phase 4: Advanced Features (Month 18-24)
**Focus**: Premium features and polish

| Feature | Priority | Status |
|---------|----------|--------|
| Voice Mode | Medium | 🔴 Not started |
| Parent Dashboard | Medium | 🔴 Not started |
| Buy/Sell Flow | High | 🔴 Not started |
| Personalized UI | Low | 🔴 Not started |
| Offline Mode | Low | 🔴 Not started |
| Third-Party API | Low | 🔴 Not started |

---

## Future Features

### Voice Mode (Phase 4)

**Description**: Full voice interaction with Leo

**Components**:
- Speech-to-text (user speaks)
- Text-to-speech (Leo responds audibly)
- Voice commands for navigation
- Voice-activated transfers (with PIN confirmation)

**Technical Requirements**:
- Whisper API for speech recognition
- ElevenLabs or Google TTS for voice output
- WebSpeech API as fallback
- Audio processing on device for privacy

**UI Concept**:
```
┌─────────────────────────────────────┐
│                                     │
│        🔊 Leo hört zu...           │
│                                     │
│           ┌─────────┐              │
│           │  ○○○○○  │              │
│           │ ○○○○○○○ │ ← Voice wave │
│           │  ○○○○○  │              │
│           └─────────┘              │
│                                     │
│     "Wie viel habe ich für..."     │
│                                     │
│        [Tippen statt sprechen]      │
└─────────────────────────────────────┘
```

**Junior-Specific**:
- "Hey Leo, quiz mich!"
- "Was sind ETFs?"
- Fun facts in response

**Adult-Specific**:
- "Sende €50 an Mama"
- "Wie war meine Woche?"
- Quick balance check

---

### Parent Dashboard (Phase 4)

**Description**: Dedicated view for parents of Junior users

**Features**:
- Real-time balance view
- Transaction alerts
- Learning progress tracking
- Spending limit controls
- Weekly reports

**What Parents Can See**:
- ✅ Real money balance
- ✅ Real transactions
- ✅ Virtual portfolio overview
- ✅ Quiz completion rates
- ✅ XP and level progress
- ❌ Chat conversations (privacy)
- ❌ Individual virtual trades

**UI Concept**:
```
┌─────────────────────────────────────┐
│  👨‍👩‍👧 Eltern-Dashboard             │
│                                     │
│  Kind: Max (15)                     │
│                                     │
│  ┌─────────────────────────────┐   │
│  │ Echtes Geld: €45.20         │   │
│  │ Diese Woche: -€32.50        │   │
│  └─────────────────────────────┘   │
│                                     │
│  ┌─────────────────────────────┐   │
│  │ Lernfortschritt            │   │
│  │ Level 7 | 12,345 XP        │   │
│  │ Diese Woche: 4 Quizzes      │   │
│  │ ████████████░░░ 78%        │   │
│  └─────────────────────────────┘   │
│                                     │
│  [Taschengeld senden]              │
│  [Limits anpassen]                  │
│  [Wochenbericht ansehen]           │
└─────────────────────────────────────┘
```

---

### Smart Subscription Tracking (Phase 3)

**Description**: AI-powered subscription detection and optimization

**Detection Method**:
- Pattern recognition in transactions
- Regular amounts at regular intervals
- Merchant category codes (MCC)
- Known subscription services database

**Features**:
- Auto-detect new subscriptions
- Track unused subscriptions (via transaction absence)
- Price increase alerts
- Cancellation assistance
- Alternative suggestions

**UI Concept**:
```
┌─────────────────────────────────────┐
│  📺 Netflix - WARNUNG               │
│                                     │
│  Letzte Nutzung: vor 45 Tagen      │
│  Monatliche Kosten: €17.99         │
│  Bisher bezahlt: €215.88           │
│                                     │
│  Leo: "Du zahlst, aber schaust     │
│  nicht. Soll ich kündigen?"        │
│                                     │
│  [Kündigen] [Pausieren] [Behalten] │
└─────────────────────────────────────┘
```

**Tracking Limitations**:
- Cannot track external app usage (gym visits, etc.)
- Can only see payments, not actual usage
- Cookie-based tracking NOT recommended (privacy)

**What CAN Be Tracked**:
- Subscription payments
- Last payment date
- Payment increases
- Duplicate services (Spotify + Apple Music)

---

### Document Intelligence (Phase 3)

**Description**: Scan and understand financial documents

**Supported Documents**:
- Bills (electricity, water, internet)
- Insurance contracts
- Bank statements
- Tax documents
- Payslips

**Processing Pipeline**:
```
Camera/Upload → OCR → Text Extraction → GPT Analysis → User Explanation
```

**Features**:
- Auto-categorize document type
- Extract key amounts and dates
- Explain terms in simple language
- Compare to market rates
- Suggest actions

**UI Flow**:
```
1. User: "Ich habe einen Brief von meiner Versicherung"
2. Leo: "Lade ihn hoch, ich erkläre ihn dir!"
3. [Camera opens with document frame]
4. [Processing animation]
5. Leo: "Das ist deine jährliche Beitragsanpassung..."
```

---

### Bill Negotiation Assistant (Future)

**Description**: Help users negotiate better rates

**How It Works**:
1. Identify bills that could be reduced
2. Research competitive rates
3. Generate negotiation scripts
4. Track negotiation outcomes

**Example Flow**:
```
Leo: "Deine Stromrechnung ist €127.50 - 15% über Durchschnitt.

Ich habe 3 günstigere Anbieter gefunden:
• Grünstrom: €108/Monat (-15%)
• EcoEnergy: €112/Monat (-12%)
• Stadtwerke Alt: €115/Monat (-10%)

Möchtest du:
[Anbieter wechseln]
[Nachverhandeln - ich schreibe dir ein Skript]
[Aktuellen Vertrag behalten]"
```

**Negotiation Script Generator**:
```
Leo: "Hier ist ein Skript für deinen Anruf:

'Guten Tag, ich bin Kunde seit [2 Jahren] und mein 
aktueller Tarif ist [0.35€/kWh]. Ich habe Angebote 
von [Grünstrom] für [0.29€/kWh] gesehen. Können 
Sie mir ein besseres Angebot machen?'

Tipps:
• Ruf morgens an (weniger Wartezeit)
• Sei freundlich aber bestimmt
• Frag nach dem Teamleiter wenn nötig

[Script kopieren]"
```

---

## Personalized UI Vision

### Long-Term Goal (2-3 Years)

The ultimate AI-first experience adapts not just content but the UI itself.

### Personalization Levels

| Level | What Adapts | Timeline |
|-------|-------------|----------|
| 1. Content | Tips, quizzes, news | Now |
| 2. Widgets | Order, priority, visibility | 6 months |
| 3. Shortcuts | Quick actions based on habits | 12 months |
| 4. Layout | Button positions, information density | 18 months |
| 5. Full UI | Colors, fonts, structure | 24 months |

### How It Would Work

**Learning Phase (2-4 weeks)**:
- Track which features user accesses most
- Note time-of-day patterns
- Observe navigation paths
- Record ignored vs. used features

**Adaptation Phase**:
- Gradually move frequently used items to prominent positions
- Reduce visibility of unused features
- Adjust information density to user preference
- Personalize color accents (within ING guidelines)

### User Control Requirements

**Essential for Trust**:
- User must consent to personalization
- Changes happen gradually (no sudden shifts)
- "Reset to default" always available
- Preview changes before applying
- Explain why each change was made

**Example Control Panel**:
```
┌─────────────────────────────────────┐
│  🎨 Personalisierung                │
│                                     │
│  Leo passt die App an dich an.     │
│                                     │
│  Aktive Anpassungen:                │
│  ✅ Quick Actions neu geordnet     │
│  ✅ Statistik-Widget prominent     │
│  ✅ Investment-Tab zuerst          │
│                                     │
│  [Alle Änderungen ansehen]         │
│  [Auf Standard zurücksetzen]       │
│                                     │
│  Personalisierung: [████████░░] An │
│                                     │
│  ℹ️ Deine Nutzungsdaten bleiben    │
│  auf deinem Gerät.                  │
└─────────────────────────────────────┘
```

### Personalization Ideas

**Based on User Type**:

| Pattern Detected | Adaptation |
|------------------|------------|
| Checks balance daily | Balance widget always visible |
| Never uses Orders tab | Hide or minimize Orders |
| Frequent transfers to same person | Create quick-send shortcut |
| Always opens Investment at market open | Investment notification at 9:00 |
| Prefers dark mode in evening | Auto-switch at sunset |

---

## API & Integration Roadmap

### Current APIs Used

| Service | Purpose | Status |
|---------|---------|--------|
| OpenAI GPT-4 | Chat, explanations | ✅ Integrated |
| ING Core Banking (mock) | Account data | 🟡 Mocked |
| Stock Data (mock) | Prices, charts | 🟡 Mocked |

### Required API Integrations

#### Phase 2: Learning Features

| API | Purpose | Estimated Cost |
|-----|---------|----------------|
| OpenAI GPT-4 (more) | Quiz generation | ~€500/month |
| DALL-E 3 | Quiz images | ~€200/month |
| Financial Education API | Verified content | License fee |

#### Phase 3: Smart Finance

| API | Purpose | Estimated Cost |
|-----|---------|----------------|
| Azure Form Recognizer | Document OCR | ~€300/month |
| News Aggregation API | Personalized news | ~€100/month |
| Real Stock Data API | Live prices | ~€500/month |

#### Phase 4: Advanced

| API | Purpose | Estimated Cost |
|-----|---------|----------------|
| Whisper API | Voice recognition | ~€200/month |
| ElevenLabs | Voice synthesis | ~€300/month |
| Push Notification | Alerts | ~€100/month |

### Data Sources for AI

| Data Type | Source | Sensitivity |
|-----------|--------|-------------|
| Transaction history | ING Core | High |
| Balance | ING Core | High |
| User preferences | Local storage | Medium |
| Quiz performance | Leo database | Low |
| Stock prices | Market API | Public |
| News articles | News API | Public |

### Privacy Considerations

| Data | Stored Where | Shared With |
|------|--------------|-------------|
| Chat history | User device | OpenAI (processing) |
| Transactions | ING servers | Leo AI (analysis) |
| Personal info | ING servers | Never to AI |
| Quiz scores | Leo database | Anonymized for leaderboards |
| Preferences | User device | Not shared |

---

## Technical Debt & Improvements

### Code Quality Tasks

| Task | Priority | Effort |
|------|----------|--------|
| Add TypeScript strict mode | High | Medium |
| Create component tests | High | High |
| Implement error boundaries | Medium | Low |
| Add logging/analytics | Medium | Medium |
| Create API error handling | High | Medium |
| Document components | Medium | Low |

### Performance Improvements

| Task | Priority | Effort |
|------|----------|--------|
| Lazy load screens | Medium | Medium |
| Image optimization | Low | Low |
| API response caching | Medium | Medium |
| Virtual list for transactions | Medium | Medium |
| Reduce bundle size | Low | Medium |

### UX Improvements

| Task | Priority | Effort |
|------|----------|--------|
| Add loading skeletons | Medium | Low |
| Improve transitions | Low | Medium |
| Add haptic feedback | Low | Low |
| Accessibility audit | High | Medium |
| Dark mode polish | Low | Medium |

---

## Timeline Summary

```
     2024                    2025                    2026
       │                       │                       │
       │   ┌─────────────────┐ │   ┌─────────────────┐ │
       │   │ Phase 1: MVP    │ │   │ Phase 3: Smart  │ │
       │   │ Basic features  │ │   │ Finance         │ │
       │   │ AI Chat         │ │   │ Notifications   │ │
       │   │ Quiz basics     │ │   │ Documents       │ │
       │   └─────────────────┘ │   │ Budgets         │ │
       │                       │   └─────────────────┘ │
       │   ┌─────────────────┐ │                       │
       │   │ Phase 2:        │ │   ┌─────────────────┐ │
       │   │ Enhanced        │ │   │ Phase 4:        │ │
       │   │ Learning        │ │   │ Advanced        │ │
       │   │ AI Quizzes      │ │   │ Voice mode      │ │
       │   │ Kahoot          │ │   │ Parent dash     │ │
       │   │ Leaderboards    │ │   │ Personal UI     │ │
       │   └─────────────────┘ │   └─────────────────┘ │
       │                       │                       │
```

---

*Last Updated: November 2025*
