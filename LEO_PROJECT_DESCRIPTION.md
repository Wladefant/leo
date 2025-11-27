# LEO - AI Financial Assistant for ING
## Comprehensive Project Documentation

---

## Table of Contents
1. [Executive Summary](#executive-summary)
2. [Project Context & Challenge](#project-context--challenge)
3. [Target User Profiles](#target-user-profiles)
4. [Core Features Overview](#core-features-overview)
5. [Detailed Screen Descriptions](#detailed-screen-descriptions)
6. [AI Agent "Leo" Specifications](#ai-agent-leo-specifications)
7. [Design System & UI Guidelines](#design-system--ui-guidelines)
8. [Legal & Compliance Considerations](#legal--compliance-considerations)
9. [Technical Architecture](#technical-architecture)
10. [Mockups & Visual References](#mockups--visual-references)
11. [Roadmap & Implementation Phases](#roadmap--implementation-phases)
12. [Issue References](#issue-references)

---

## Executive Summary

**LEO** is an AI-powered financial assistant designed to be integrated into the existing ING Germany banking app. The project aims to address financial literacy gaps among young users (ages 13-29) through personalized guidance, interactive learning experiences, and intelligent financial insights.

### Key Value Propositions
- **Personalized Financial Education**: AI-generated quizzes and learning paths adapted to individual user knowledge levels
- **Investment Simulator**: Virtual money trading with real market data for risk-free learning (ING Junior Profile)
- **Smart Financial Insights**: Transaction analysis, subscription optimization, and savings recommendations
- **Emotional Intelligence**: Empathetic AI that explains financial concepts in simple, non-judgmental terms
- **Seamless Integration**: Built on top of the existing ING app, not a standalone application

### Project Competition
This is a submission for the **DFC2025 (Digital Future Challenge)** competition, focusing on creating innovative digital solutions for banking.

---

## Project Context & Challenge

### The ING Assignment
Based on the [ING Assignment Document](./ING%20assignment%20english%20version.pdf), the challenge involves:
- Exploring how AI can appropriately address young target groups in the banking app
- Building financial education and asset-building capabilities
- Creating a realistic prototype that could be implemented within 1.5-2 years

### Evaluation Criteria
From the [Important Criteria Document](./important%20criteria.pdf):

| Criterion | Description |
|-----------|-------------|
| **Social Relevance** | How well does the solution address the described problem? |
| **Future Viability** | Does it account for technological trends and long-term effectiveness? |
| **Feasibility** | Based on realistic assumptions and achievable framework conditions |
| **Multi-perspectivity** | Technology, ethics, law, economics perspectives included |
| **Social Inclusion** | Accessibility, diversity, and fair distribution considered |
| **Overall Impression** | Clear, compelling, and responsible approach to digitalization |

### ING Context from Q&A Session
Key insights from the [ING Q&A Transcript](https://github.com/Wladefant/leo/issues/19#issuecomment-3547965718):
- ING is **risk-averse** with strict regulatory requirements
- No physical gifts for gamification; digital rewards preferred
- Solution must be **integrated into existing app**, not standalone
- ~5% of customers currently opt-in to data analysis features (growing trend)
- ~11% of customer base is aged 20-29
- All user data can be accessed by the AI for personalization (with proper privacy controls)

---

## Target User Profiles

### Primary Target: ING Junior Profile (Ages 13-17)
**Related Issues**: [#32](https://github.com/Wladefant/leo/issues/32), [#34](https://github.com/Wladefant/leo/issues/34), [#5](https://github.com/Wladefant/leo/issues/5)

| Attribute | Description |
|-----------|-------------|
| **Age Range** | 13-17 years old |
| **Account Type** | Girokonto Junior (requires parental consent) |
| **Key Features** | Investment simulator, financial quizzes, virtual money |
| **Access Model** | 1 month free trial → requires parent-approved card |
| **UI Treatment** | Simplified interface with gamified elements |

**Pain Points** ([Issue #30](https://github.com/Wladefant/leo/issues/30)):
- Lack of practical financial knowledge before entering workforce
- Anxiety about taxes, investments, insurance
- No safe environment to learn about money management
- Traditional financial education is boring and not engaging

### Secondary Target: Young Adults (Ages 18-29)
**Related Issues**: [#46](https://github.com/Wladefant/leo/issues/46), [#32](https://github.com/Wladefant/leo/issues/32)

| Attribute | Description |
|-----------|-------------|
| **Age Range** | 18-29 years old |
| **Account Type** | Full ING Girokonto + Depot |
| **Key Features** | Real investments, full AI assistant, transaction analysis |
| **Demographics** | Students, "Azubis" (apprentices), young professionals, young families |

**Pain Points**:
- First time dealing with taxes, salary deductions
- Overwhelmed by financial product choices (insurance, investments)
- Need guidance on budgeting and subscription management
- Desire for personalized, trustworthy financial advice

---

## Core Features Overview

### 1. Leo AI Agent Chatbot
**Issues**: [#44](https://github.com/Wladefant/leo/issues/44), [#45](https://github.com/Wladefant/leo/issues/45), [#28](https://github.com/Wladefant/leo/issues/28), [#35](https://github.com/Wladefant/leo/issues/35)

The central AI assistant that provides:
- **General Mode**: Financial Q&A, explanations, personalized insights
- **Quiz Mode**: Interactive learning with adaptive difficulty
- **Voice Mode**: Text-to-speech and speech-to-text capabilities
- **Document Analysis**: Camera/file upload for contract/document explanation

**Key Characteristics** (from [ING Leo Important Considerations](./ING%20Leo%20important%20considerations.pdf)):
- Friendly, non-judgmental, empathetic tone
- Accurate, objective, free from manipulation
- Aligned with user's best interests
- **Must be clearly labeled as AI** (EU AI Act requirement)
- **Strictly finance-related** - cannot discuss non-financial topics

### 2. Investment Simulator (ING Junior)
**Issues**: [#5](https://github.com/Wladefant/leo/issues/5), [#34](https://github.com/Wladefant/leo/issues/34), [#36](https://github.com/Wladefant/leo/issues/36)

"Beat the Market" - Learn investing by trading virtual money with real market data.

| Feature | Description |
|---------|-------------|
| **Virtual Salary** | Weekly simulated salary (no reset option) |
| **Tax Simulation** | Taxes deducted from salary to teach netto/brutto concepts |
| **Real Market Data** | Live stock prices for realistic experience |
| **Portfolio View** | Track virtual holdings and performance |
| **Cash Display** | Show uninvested funds available for trading |

### 3. Smart AI Statistics & Analytics
**Issues**: [#47](https://github.com/Wladefant/leo/issues/47), [#43](https://github.com/Wladefant/leo/issues/43)

Intelligent transaction analysis featuring:
- **Automatic Categorization**: Company/subscription detection
- **Natural Language Queries**: "How much money did I make the last 6 months?"
- **Spending Insights**: Visual pie charts and trend analysis
- **AI-Powered Summaries**: Personalized financial health overview

### 4. Subscription Optimization
**Issues**: [#42](https://github.com/Wladefant/leo/issues/42), [#6](https://github.com/Wladefant/leo/issues/6)

- **Kreisdiagramm (Pie Chart)**: Visual representation of subscriptions
- **Savings Calculator**: "You will have €X more if you cancel this subscription"
- **Usage Detection** (Optional): Cookie-based suggestion to cancel unused services

### 5. Savings Goal Planner
**Issue**: [#6](https://github.com/Wladefant/leo/issues/6)

AI-assisted goal setting and tracking:
- Set personalized savings targets
- Track progress with visual indicators
- Receive AI recommendations for achieving goals faster

### 6. Interactive Quizzes
**Issues**: [#33](https://github.com/Wladefant/leo/issues/33), [#39](https://github.com/Wladefant/leo/issues/39), [#9](https://github.com/Wladefant/leo/issues/9)

**Topics**:
- Investments & Stocks
- Insurance Scenarios
- Taxes & Salary Deductions

**Features**:
- Accessible from any screen via Leo button
- Two modes: General Mode and Quiz Mode
- AI-generated questions based on user performance ([#17](https://github.com/Wladefant/leo/issues/17), [#18](https://github.com/Wladefant/leo/issues/18))
- Adaptive difficulty algorithm
- On-the-fly image generation for scenarios

### 7. Gamification & Rewards System
**Issues**: [#15](https://github.com/Wladefant/leo/issues/15), [#37](https://github.com/Wladefant/leo/issues/37)

| Element | Description |
|---------|-------------|
| **Points** | Earned for completing quizzes, learning modules |
| **Achievements** | Duolingo-style badges (e.g., "5 Quizzes Starter") |
| **Leaderboard** | Weekly competitions between students/schools |
| **Weekly Prizes** | Cash prizes for leaderboard leaders |
| **Financial Benefits** | Interest rate bonuses when turning 18 |
| **School Championships** | Inter-school competitions with leaderboards |

**Important**: No physical merchandise (ING policy from Q&A)

### 8. Personalized News Feed
**Issue**: [#16](https://github.com/Wladefant/leo/issues/16)

- **Stock News**: Bottom of stock view with company-specific news
- **Daily Notifications**: Click to open summarized news in chat
- **For You Page**: Perplexity-style personalized news based on watchlist/portfolio
- **Link Integration**: Opens browser for full article access

### 9. Smart Action Transfers (Notifications)
**Issues**: [#52](https://github.com/Wladefant/leo/issues/52), [#53](https://github.com/Wladefant/leo/issues/53)

**Scenario Example**: "It's the first of the month. Rent is usually due today. Send €800 to Landlord?"

**Visual Design**:
- Slim, focused card interface
- Recipient avatar, name, pre-filled amount
- Single slide-to-confirm or large violet [Send €800 now] button
- Removes friction for recurring transactions

---

## Detailed Screen Descriptions

### 1. Login Screen
**Issue**: [#32](https://github.com/Wladefant/leo/issues/32)

| Element | Description |
|---------|-------------|
| **ING Deposit Users** | Standard login for adult accounts |
| **ING Kids Login** | Separate entry point for junior profiles |
| **UI Treatment** | If no Girokonto Junior, balance is greyed out |

### 2. General Account View (Konten)
**Issues**: [#47](https://github.com/Wladefant/leo/issues/47), [#54](https://github.com/Wladefant/leo/issues/54)

**Mockup Reference**: [`mockups/general_account_view.png`](./mockups/general_account_view.png)

**Elements**:
- Account balance display
- Recent transactions list
- Leo AI button (floating action button)
- Smart AI statistics widget integration
- Quick action buttons (Transfer, Cards, etc.)

### 3. Single Account View
**Mockup Reference**: [`mockups/single_account_view.png`](./mockups/single_account_view.png)

Detailed view of individual account with:
- Transaction history
- Category breakdown
- Leo integration for transaction queries

### 4. Leo Agent Chat View
**Issues**: [#44](https://github.com/Wladefant/leo/issues/44), [#45](https://github.com/Wladefant/leo/issues/45), [#28](https://github.com/Wladefant/leo/issues/28)

**Mockup Reference**: [`mockups/chat_view.png`](./mockups/chat_view.png)

**UI Elements**:
| Element | Description |
|---------|-------------|
| **Chat Interface** | Message bubbles with Leo responses |
| **Mode Toggle** | Switch between General/Quiz mode |
| **Input Bar** | Text input with file/camera/voice buttons |
| **Stock Widget** | Embedded stock charts in conversation |
| **Graph Widget** | Inline financial graphs |
| **Diagram Widget** | Pie charts and visualizations |
| **Settings Dialog** | Quick settings changes from chat |
| **Transaction Prompt** | Quick money transfer dialogs |

**Capabilities**:
- Voice reading of messages (accessibility)
- Automation: transactions, dark mode toggle, settings from chat
- Document analysis via camera/file upload

### 5. Stock View (Individual Stock)
**Issues**: [#36](https://github.com/Wladefant/leo/issues/36), [#51](https://github.com/Wladefant/leo/issues/51)

**Mockup References**: [`mockups/stock1.png`](./mockups/stock1.png), [`mockups/stock2.png`](./mockups/stock2.png)

**Elements**:
- Stock price chart (1D, 1W, 1M, 1Y, All time)
- Buy/Sell buttons
- Company news section at bottom
- Leo integration for stock explanations
- Analyst ratings and recommendations

**Leo Integration**: Chatbot overlay showing:
- Stock explanations
- Risk analysis
- "Do a quiz about this stock" speech bubble

### 6. Stock List View / Portfolio View
**Issue**: [#11](https://github.com/Wladefant/leo/issues/11)

- Search icon at top (Apple-style search UX)
- Portfolio and News tabs
- Watchlist integration
- Cash balance display (uninvested funds)

**ING Trading Features Reference**: See [`ING Trading Features/`](./ING%20Trading%20Features/) folder containing:
- Depot-Übersicht (Depot Overview)
- Watchlist
- Wertpapier-Portraits (Securities Portraits)
- Wertpapier-Suche (Securities Search) with filters

### 7. Investment Dashboard
**Related Files**: [`ING Trading Features/Investieren Dashboard/`](./ING%20Trading%20Features/Investieren%20Dashboard/)

Main investment screen with:
- Portfolio summary
- News and Stocks tabs at top
- Personalized summarized news (Perplexity-style)
- Same experience in Junior and ING app

### 8. Salary / Taxes View
**Issue**: [#40](https://github.com/Wladefant/leo/issues/40)

**Trigger**: Weekly salary arrival (first occurrence shows popup)

**UI Elements**:
- Receipt-style breakdown of gross to net salary
- Tax deduction itemization
- Leo speech bubble: "Do a quiz about taxes"
- Educational explanations of each deduction

### 9. Quizzes View
**Issue**: [#33](https://github.com/Wladefant/leo/issues/33)

**Access**: From any screen via Leo button

**UI Flow**:
1. Open Leo
2. Select: General Mode or Quiz Mode
3. Quiz Mode opens Duolingo-style interface
4. Topics: Investment, Insurance, Taxes

**Features**:
- Adaptive difficulty based on performance
- Progress tracking
- Points/achievement integration

### 10. Leaderboard View
**Issue**: [#37](https://github.com/Wladefant/leo/issues/37)

- Weekly point collection display
- School/user rankings
- Prize announcements
- Achievement badges

### 11. Statistics View
**Issue**: [#47](https://github.com/Wladefant/leo/issues/47)

**Mockup Reference**: [`mockups/statistics.png`](./mockups/statistics.png)

- Spending category breakdown
- Income vs. expenses visualization
- Trend analysis over time
- AI-generated insights

### 12. Savings Planner View
**Issue**: [#6](https://github.com/Wladefant/leo/issues/6)

**Mockup Reference**: [`mockups/savings_planner.png.png`](./mockups/savings_planner.png.png)

- Goal setting interface
- Progress visualization
- AI recommendations for savings optimization

### 13. Products / Insurance View
**Issue**: [#9](https://github.com/Wladefant/leo/issues/9)

**Mockup Reference**: [`mockups/products_view.png`](./mockups/products_view.png)

**ING App**: Can purchase insurance products
**ING Junior**: Can read about and do quizzes on insurance

### 14. Personal Questions Onboarding
**Issue**: [#38](https://github.com/Wladefant/leo/issues/38)

Initial setup flow asking about:
- Financial goals (short-term and long-term)
- Risk preferences
- Current financial situation
- Interests and learning preferences

### 15. Virtual Money Dashboard (ING Junior)
**Issue**: [#34](https://github.com/Wladefant/leo/issues/34)

- Virtual balance display
- Simulated transaction history
- Investment portfolio (virtual)
- Weekly "salary" deposits

### 16. High Contrast / Accessibility View
**Mockup Reference**: [`mockups/high_contrast_general_account_view.png`](./mockups/high_contrast_general_account_view.png)

- High contrast mode for visual accessibility
- Screen reader compatible elements
- Simplified navigation for cognitive accessibility

---

## AI Agent "Leo" Specifications

### Personality & Tone
**Issue**: [#45](https://github.com/Wladefant/leo/issues/45)

Based on [ING Leo Important Considerations](./ING%20Leo%20important%20considerations.pdf):

| Attribute | Description |
|-----------|-------------|
| **Tone** | Friendly, non-judgmental, empathetic, motivating |
| **Language** | Simple, jargon-free, easy to understand |
| **Examples** | Real-life scenarios that resonate with young users |
| **Emotional Support** | Helps users deal with fears (risks, debt, investments) |
| **Feeling Created** | Empathy, understanding, support |

### Core Capabilities

1. **Financial Knowledge Adaptation**
   - Knows user's short- and long-term goals
   - Understands risk preferences
   - Aligns advice with personal tradeoffs

2. **Query Understanding**
   - Natural language processing for financial questions
   - SQL-like data queries on user transactions
   - Context-aware responses based on conversation history

3. **Content Generation**
   - Quiz questions adapted to user level
   - Personalized insights and recommendations
   - Document explanations in plain language

### Technical Constraints
**Issue**: [#35](https://github.com/Wladefant/leo/issues/35)

- **Strictly Finance-Related**: Cannot discuss non-financial topics
- **Closed Environment**: Does not scrape open internet (prevents fake news/hallucinations)
- **Two Memory Types**:
  - **Shared Memory**: General financial knowledge (accessible to all)
  - **Closed Memory**: Private user data (never leaked between users)

### Interaction Modes

1. **Text Chat**: Standard messaging interface
2. **Voice Input**: Speech-to-text for questions
3. **Voice Output**: Text-to-speech for responses
4. **Camera/File Upload**: Document analysis capability

### Widgets (Inline in Chat)
**Issue**: [#48](https://github.com/Wladefant/leo/issues/48)

| Widget | Description |
|--------|-------------|
| **Stock Widget** | Live stock chart with key metrics |
| **Graph Widget** | Line/bar charts for financial data |
| **Diagram Widget** | Pie charts for spending breakdown |
| **Transfer Prompt** | Quick money transfer dialog |
| **Settings Dialog** | Quick settings changes |

---

## Design System & UI Guidelines

### Color Palette
**Issue**: [#25](https://github.com/Wladefant/leo/issues/25)

| Color | Hex Code | Usage |
|-------|----------|-------|
| **Main (Orange)** | `#ff6200` | Primary actions, highlights, ING branding |
| **Background (Light Grey)** | `#f4f4f4` | Screen backgrounds |
| **Text (Dark Grey)** | `#1f1f1f` | Body text, headings |
| **Violet** | (accent) | Secondary actions (e.g., Send button) |

### Design Principles

1. **Consistency with ING App**: Follow existing ING design patterns
2. **Simplified for Junior**: Less complex UI for younger users
3. **Accessibility First**: WCAG compliance, high contrast mode
4. **Mobile-First**: Optimized for smartphone interactions

### UI Elements

**Leo Button**: 
- Floating action button present on all screens
- Lion mascot icon ([`mockups/Leo.png`](./mockups/Leo.png))
- Opens chat interface

**Navigation**:
- Bottom tab bar (Konten, Investieren, Products, Settings)
- Leo button accessible from all tabs

---

## Legal & Compliance Considerations

### EU AI Act Classification
**Issue**: [#50](https://github.com/Wladefant/leo/issues/50)

Based on legal analysis in Issue #50:

| Classification | Rationale |
|---------------|-----------|
| **Limited Risk** | General financial advice, spending analysis, saving potential insights |
| **NOT High-Risk** | Not used for creditworthiness evaluation, insurance pricing, or essential benefits eligibility |

**Primary Obligation - Transparency (Article 50)**:
- Users must be informed they're interacting with AI
- AI-generated content must be machine-readable and detectable
- Staff must have sufficient AI literacy

### GDPR Compliance
**Issue**: [#50](https://github.com/Wladefant/leo/issues/50)

| Requirement | Implementation |
|-------------|----------------|
| **DPIA** | Data Protection Impact Assessment required for sensitive data processing |
| **Explicit Consent** | Cannot use "legitimate interest" for sensitive financial data |
| **Enhanced Security** | Encryption, strict access controls |
| **Data Minimization** | Collect only necessary data |

### Minors Protection (Under 18)
**Issue**: [#50](https://github.com/Wladefant/leo/issues/50)

| Requirement | Implementation |
|-------------|----------------|
| **Age Verification** | Reasonable efforts to verify consent (not just Y/N) |
| **Parental Consent** | Required for users under 16 in Germany |
| **Child-Friendly Transparency** | Clear, plain language explanations |
| **No Profiling-Based Ads** | Prohibited for minors |
| **Highest Privacy Settings** | Default configuration |
| **No Dark Patterns** | No manipulative or addictive design |

### Prohibited Practices
From [ING Leo Important Considerations](./ING%20Leo%20important%20considerations.pdf):

❌ **Manipulation Tactics**:
- Pressure tactics
- Disguised sales pushes
- Emotional manipulation to upsell products

✅ **Required Practices**:
- Human oversight for critical decisions
- Privacy-by-design
- Transparency and explainability
- Ethical neutrality

### Data Usage Boundaries
**Issue**: [#50](https://github.com/Wladefant/leo/issues/50)

**Allowed**:
- System improvement (aggregated, anonymized)
- Security purposes
- Educational analytics

**Prohibited**:
- Marketing/cross-selling using simulator data
- Bundled consent ("play simulator" ≠ "open bank account")

### Implementation Examples

**Transparency Popup**:
```
"Let's face it: managing subscriptions is boring stuff. Ever bought the 
same service twice or forgot to cancel a free trial? 🤦‍♂️

To help you avoid that, we analyze your transaction data to spot 
duplicates and wasted money. We do this to give you personalized 
savings tips.

Read the full [Privacy Policy] to see exactly how we crunch the numbers."
```

**Opt-Out Option**:
```
☐ Allow personalized insights based on my spending data.
```

---

## Technical Architecture

### Integration Model
Based on Q&A transcript in [Issue #19](https://github.com/Wladefant/leo/issues/19):

```
┌─────────────────────────────────────────────────────┐
│                  Existing ING App                    │
├─────────────────────────────────────────────────────┤
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐ │
│  │   Konten    │  │ Investieren │  │  Products   │ │
│  └─────────────┘  └─────────────┘  └─────────────┘ │
│                                                      │
│         ┌──────────────────────────────┐           │
│         │    LEO AI Layer (New)        │           │
│         │  • Chat Interface            │           │
│         │  • Quiz Engine               │           │
│         │  • Investment Simulator      │           │
│         │  • Analytics Engine          │           │
│         └──────────────────────────────┘           │
│                         │                           │
│         ┌───────────────┴───────────────┐         │
│         │                               │          │
│   ┌─────▼─────┐                 ┌──────▼─────┐   │
│   │  Shared   │                 │   Closed   │    │
│   │  Memory   │                 │   Memory   │    │
│   │ (General  │                 │   (User    │    │
│   │  Finance) │                 │    Data)   │    │
│   └───────────┘                 └────────────┘    │
└─────────────────────────────────────────────────────┘
```

### Data Architecture

**Shared Memory** (Accessible to all users):
- Financial education content
- General market data
- Quiz question bank
- News articles

**Closed Memory** (Per-user, sandboxed):
- Transaction history
- Account balances
- User preferences
- Quiz performance
- Investment simulator data

### API Assumptions
From Q&A transcript:
- Financial education API (assumed to exist or be purchased)
- Real-time market data API
- User transaction data API (internal ING)
- Notification/push API

### Knowledge Base
**Issue**: [#29](https://github.com/Wladefant/leo/issues/29)

- Filtered, verified content only
- No open internet scraping
- Suggested: Purchase API from third-party financial education provider
- ING does not currently have in-house financial education API

---

## Mockups & Visual References

### Repository Mockups

| Screen | File Path |
|--------|-----------|
| Leo Mascot | [`mockups/Leo.png`](./mockups/Leo.png) |
| General Account View | [`mockups/general_account_view.png`](./mockups/general_account_view.png) |
| Single Account View | [`mockups/single_account_view.png`](./mockups/single_account_view.png) |
| Chat View | [`mockups/chat_view.png`](./mockups/chat_view.png) |
| Statistics | [`mockups/statistics.png`](./mockups/statistics.png) |
| Savings Planner | [`mockups/savings_planner.png.png`](./mockups/savings_planner.png.png) |
| Products View | [`mockups/products_view.png`](./mockups/products_view.png) |
| Stock View 1 | [`mockups/stock1.png`](./mockups/stock1.png) |
| Stock View 2 | [`mockups/stock2.png`](./mockups/stock2.png) |
| High Contrast View | [`mockups/high_contrast_general_account_view.png`](./mockups/high_contrast_general_account_view.png) |
| Main View 1 | [`mockups/main1.png`](./mockups/main1.png) |
| Main View 2 | [`mockups/main2.png`](./mockups/main2.png) |

### Original ING App Screenshots
Located in [`mockups/original-mockups-ing/`](./mockups/original-mockups-ing/):
- ING App Setup flows
- Transfer flows ("Überweisen mit der ING App")
- Card limit management ("Kartenlimit ändern")
- Depot transfer ("Depot zur ING übertragen")
- App tutorial ("Lerne Deine ING App kennen")

### Investment Flow Screens
Located in [`mockups/Investment/`](./mockups/Investment/):
- Detailed investment journey screens

### Watchlist Screens
Located in [`mockups/Watchlist invest/`](./mockups/Watchlist%20invest/)

### ING Trading Features (Official)
Located in [`ING Trading Features/`](./ING%20Trading%20Features/):

| Feature | Folder |
|---------|--------|
| Markets Overview | `Börsen & Märkte/` |
| Depot Order Flow | `Depot – Order-Flow/` |
| Order Manager | `Depot – Ordermananger/` |
| Savings Plan | `Depot – Sparplananlage/` |
| Depot Overview | `Depot-Übersicht/` |
| Investment Dashboard | `Investieren Dashboard/` |
| Watchlist | `Watchlist/` |
| Security Portraits | `Wertpapier-Portraits/` |
| Stock Filter | `Wertpapier-Suche – Aktien-Filter/` |
| ETF Filter | `Wertpapier-Suche – ETF-Filter/` |
| Leverage Products | `Wertpapier-Suche – Hebelprodukte/` |
| Inspirations | `Wertpapier-Suche – Inspirationen/` |

### Issue-Embedded Mockups

Many mockups are attached directly in GitHub issues:
- [Issue #54](https://github.com/Wladefant/leo/issues/54) - Original ING App Screens
- [Issue #51](https://github.com/Wladefant/leo/issues/51) - Stock View Chatbot
- [Issue #52](https://github.com/Wladefant/leo/issues/52) - Smart Action Transfer Widget
- [Issue #47](https://github.com/Wladefant/leo/issues/47) - Smart AI Statistics
- [Issue #36](https://github.com/Wladefant/leo/issues/36) - Investment Stock View (17+ comments with images)
- [Issue #44](https://github.com/Wladefant/leo/issues/44) - General Chatbot View
- [Issue #5](https://github.com/Wladefant/leo/issues/5) - Investment Simulator
- [Issue #6](https://github.com/Wladefant/leo/issues/6) - Savings Goal Planner

---

## Roadmap & Implementation Phases

### Phase Overview
**Issue**: [#49](https://github.com/Wladefant/leo/issues/49)

From ING Q&A guidance: Use **Steps** not fixed dates (compliance processes can take 1.5-2 years)

```
Step 1: MVP (Foundation)
├── Basic Leo Chat Interface
├── Simple Q&A functionality
├── User data integration
└── Transaction categorization

Step 2: Learning Features
├── Quiz system implementation
├── Financial education content
├── Basic gamification (points)
└── Progress tracking

Step 3: Investment Simulator (Junior)
├── Virtual money system
├── Real market data integration
├── Portfolio tracking
├── Tax simulation

Step 4: Advanced Features
├── Smart notifications
├── Document analysis
├── Voice interaction
├── Leaderboards

Step 5: Expansion
├── School partnerships
├── Advanced analytics
├── Inter-school competitions
└── Premium features
```

### Cost & Timeline Considerations
**Issue**: [#49](https://github.com/Wladefant/leo/issues/49)

- Realistic implementation: 1.5-2 years
- Must account for:
  - Regulatory compliance reviews
  - Security audits
  - User testing phases
  - Legal approval processes

---

## Issue References

### Core Features
| Issue | Title | Labels |
|-------|-------|--------|
| [#44](https://github.com/Wladefant/leo/issues/44) | General chatbot view | feature, ING APP, ING Junior, Screens/View, AiChat |
| [#45](https://github.com/Wladefant/leo/issues/45) | LeoAgentChatView: Emotional access points | ING APP, ING Junior, AiChat |
| [#5](https://github.com/Wladefant/leo/issues/5) | Investment Simulator | feature, ING Junior |
| [#6](https://github.com/Wladefant/leo/issues/6) | Savings goal planner | feature, ING APP |
| [#33](https://github.com/Wladefant/leo/issues/33) | QuizzesView | feature, ING APP, ING Junior, Screens/View |
| [#15](https://github.com/Wladefant/leo/issues/15) | Gamification | feature, ING Junior |
| [#43](https://github.com/Wladefant/leo/issues/43) | Transaction analysis | feature, ING APP |
| [#42](https://github.com/Wladefant/leo/issues/42) | Subscription optimization | feature, ING APP |

### Screen Definitions
| Issue | Title | Labels |
|-------|-------|--------|
| [#54](https://github.com/Wladefant/leo/issues/54) | ING APP original UI Screens | - |
| [#51](https://github.com/Wladefant/leo/issues/51) | Stock View Chatbot | ING APP, ING Junior, Screens/View |
| [#52](https://github.com/Wladefant/leo/issues/52) | Smart Action Transfer Widget | Screens/View |
| [#47](https://github.com/Wladefant/leo/issues/47) | Konten / smart ai statistics | ING APP, Screens/View |
| [#46](https://github.com/Wladefant/leo/issues/46) | Separate App MockUp 18-29 | ING Junior |
| [#40](https://github.com/Wladefant/leo/issues/40) | Salary / Taxes View | ING Junior, Screens/View |
| [#38](https://github.com/Wladefant/leo/issues/38) | Personal Questions at start | ING Junior, Screens/View |
| [#37](https://github.com/Wladefant/leo/issues/37) | LeaderboardView | feature, ING Junior |
| [#36](https://github.com/Wladefant/leo/issues/36) | Investment Stock View | ING APP, ING Junior, Screens/View |
| [#34](https://github.com/Wladefant/leo/issues/34) | Virtual Money for kids | ING Junior, Screens/View |
| [#32](https://github.com/Wladefant/leo/issues/32) | ING APP with ING Junior Overview | ING APP, ING Junior |
| [#11](https://github.com/Wladefant/leo/issues/11) | Stock list View | ING APP, ING Junior, Screens/View |

### Technical & Compliance
| Issue | Title | Labels |
|-------|-------|--------|
| [#50](https://github.com/Wladefant/leo/issues/50) | Legal Risks - Regulatory Review | documentation, help wanted, Legal |
| [#29](https://github.com/Wladefant/leo/issues/29) | Knowledge base | feature |
| [#35](https://github.com/Wladefant/leo/issues/35) | Chatbot strictly finances | Presentation |
| [#17](https://github.com/Wladefant/leo/issues/17) | Learning Path Deep AI integration | feature, ING APP, ING Junior |
| [#18](https://github.com/Wladefant/leo/issues/18) | AI prompt algorithm | feature, ING APP, ING Junior |
| [#13](https://github.com/Wladefant/leo/issues/13) | Legal part | Presentation, Legal |

### Presentation & Strategy
| Issue | Title | Labels |
|-------|-------|--------|
| [#27](https://github.com/Wladefant/leo/issues/27) | Work on slide deck | Presentation |
| [#26](https://github.com/Wladefant/leo/issues/26) | Unique Selling Point (USP) | Presentation |
| [#25](https://github.com/Wladefant/leo/issues/25) | App design colors | ING APP, ING Junior |
| [#24](https://github.com/Wladefant/leo/issues/24) | Create project plan | - |
| [#23](https://github.com/Wladefant/leo/issues/23) | Inclusion | Presentation |
| [#22](https://github.com/Wladefant/leo/issues/22) | Ideas from other banks | - |
| [#21](https://github.com/Wladefant/leo/issues/21) | Sources | - |
| [#19](https://github.com/Wladefant/leo/issues/19) | Summary/Transcript of ING Q&A | - |
| [#14](https://github.com/Wladefant/leo/issues/14) | Feasibility | Presentation |
| [#49](https://github.com/Wladefant/leo/issues/49) | Project Roadmap | Presentation |

### Additional Features
| Issue | Title | Labels |
|-------|-------|--------|
| [#53](https://github.com/Wladefant/leo/issues/53) | Notification | feature |
| [#48](https://github.com/Wladefant/leo/issues/48) | Widgets | feature, ING APP, ING Junior, Screens/View |
| [#41](https://github.com/Wladefant/leo/issues/41) | Questions from ING Team | - |
| [#39](https://github.com/Wladefant/leo/issues/39) | Investment Quiz | - |
| [#31](https://github.com/Wladefant/leo/issues/31) | Two apps into one: why? | Presentation |
| [#30](https://github.com/Wladefant/leo/issues/30) | Pain points | ING APP, ING Junior |
| [#28](https://github.com/Wladefant/leo/issues/28) | Files/images/camera/voice in LEO | ING APP, additional feature |
| [#16](https://github.com/Wladefant/leo/issues/16) | News | feature, ING APP, ING Junior |
| [#9](https://github.com/Wladefant/leo/issues/9) | Insurance Scenarios | feature, ING APP, ING Junior |
| [#4](https://github.com/Wladefant/leo/issues/4) | Access login with card | ING APP |

---

## Unique Selling Points (USP)
**Issue**: [#26](https://github.com/Wladefant/leo/issues/26)

1. **AI-First Financial Education**: Unlike competitors, Leo provides truly personalized, adaptive learning
2. **Risk-Free Investment Learning**: Real market data with virtual money
3. **Seamless Banking Integration**: Not a separate app, but enhanced ING experience
4. **Emotional Intelligence**: AI that understands financial anxiety
5. **Regulatory Compliance by Design**: Built with EU AI Act and GDPR from ground up
6. **Multi-Generational**: Serves both teens learning and young adults managing real money

---

## Competitor Analysis
**Issue**: [#22](https://github.com/Wladefant/leo/issues/22)

| Competitor | Strengths | Weaknesses | Leo Advantage |
|------------|-----------|------------|---------------|
| **N26 Learn** | Clean UI, good tone | Not interactive | Interactive AI conversations |
| **Revolut Junior** | Gamified, parental control | Limited real learning | Deep financial education |
| **Finanzfluss** | Strong content | No personalization | Personalized AI guidance |
| **Finanzguru** | Financial assistance | Not educational | Learning + assistance combined |
| **Planspiel Börse** | Investment simulation | Separate from banking | Integrated in real banking app |

---

## Presentation Resources
**Issue**: [#27](https://github.com/Wladefant/leo/issues/27)

- **Slide Deck**: [Edit on Canva](https://www.canva.com/design/DAG5tk0mDz4/mp7t4R00-hH_7H4fKeaW2w/edit?utm_content=DAG5tk0mDz4&utm_campaign=designshare&utm_medium=link2&utm_source=sharebutton)
- Maximum 8 slides (including title and literature)
- Additional materials (videos, URLs, MVPs) can be uploaded via portal

---

## Document References

| Document | Description |
|----------|-------------|
| [ING assignment english version.pdf](./ING%20assignment%20english%20version.pdf) | Original challenge brief |
| [ING assignment german version.pdf](./ING%20assignment%20german%20version.pdf) | German version of challenge |
| [important criteria.pdf](./important%20criteria.pdf) | Jury evaluation criteria |
| [ING Leo important considerations.pdf](./ING%20Leo%20important%20considerations.pdf) | AI design guidelines |
| [DFC2025 - Submission Template_DE.pdf](./DFC2025%20-%20Submission%20Template_DE%20%20-%20%20Schreibgeschützt.pdf) | Submission template |

---

*Last Updated: November 2025*
*Repository: [Wladefant/leo](https://github.com/Wladefant/leo)*
