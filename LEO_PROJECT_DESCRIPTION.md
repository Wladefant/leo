# LEO - AI Financial Assistant for ING
## Comprehensive Project Documentation
### Single Source of Truth for DFC2025 Challenge

---

## Table of Contents
1. [Executive Summary](#executive-summary)
2. [AI-First Philosophy](#ai-first-philosophy)
3. [Project Context & Challenge](#project-context--challenge)
4. [Target User Profiles](#target-user-profiles)
5. [Core Features Overview](#core-features-overview)
6. [UI Creator Specifications](#ui-creator-specifications)
7. [Detailed Screen Descriptions](#detailed-screen-descriptions)
8. [AI Agent "Leo" Specifications](#ai-agent-leo-specifications)
9. [Design System & UI Guidelines](#design-system--ui-guidelines)
10. [Legal & Compliance Considerations](#legal--compliance-considerations)
11. [Technical Architecture](#technical-architecture)
12. [Answered Questions & Decisions](#answered-questions--decisions)
13. [Mockups & Visual References](#mockups--visual-references)
14. [Roadmap & Implementation Phases](#roadmap--implementation-phases)
15. [Presentation Strategy](#presentation-strategy)
16. [Issue References](#issue-references)

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

## AI-First Philosophy

> **Core Principle**: Every interaction in the LEO ecosystem starts and ends with AI. Leo is not a feature—it is THE interface.

### What "AI-First" Means for LEO

| Traditional Banking App | LEO AI-First Approach |
|------------------------|----------------------|
| User navigates menus to find features | User asks Leo, Leo navigates for them |
| Static screens with fixed information | Dynamic screens generated based on context |
| User must learn app structure | App learns user's habits and preferences |
| Reactive (user initiates actions) | Proactive (AI suggests actions before user thinks of them) |
| One-size-fits-all UI | Personalized UI based on user profile and behavior |

### AI-First for ING Junior Profile (Ages 13-17)
- **Learning is Primary**: Every screen is a learning opportunity
- **Leo Guides Everything**: No dead-ends; Leo is always available to explain
- **Proactive Education**: Leo notices when user is confused and offers help
- **Gamified AI**: Leo turns financial concepts into challenges
- **Safe Exploration**: Virtual money + real AI guidance = risk-free learning
- **Natural Language First**: Teens can type/speak naturally; no banking jargon required

### AI-First for ING Adult Profile (Ages 18-29)
- **Intelligent Automation**: Leo predicts and suggests recurring transactions
- **Contextual Insights**: Real-time analysis appears when relevant (not hidden in reports)
- **Document Intelligence**: Scan any financial document, Leo explains it instantly
- **Conversational Banking**: Complete banking tasks through natural conversation
- **Proactive Financial Health**: Leo alerts about unusual spending, opportunities, risks
- **Smart Notifications**: Not just alerts—actionable AI-powered suggestions

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

## UI Creator Specifications

> **Purpose**: This section provides copy-paste ready specifications for app builders and UI tools. Each screen is described with exact elements, behaviors, and AI integrations.

### Global UI Components

#### 1. Leo Floating Action Button (FAB)
**Present on ALL screens**

```
Component: LeoFAB
Position: Bottom-right corner, 16dp margin
Size: 56dp diameter
Icon: Leo lion mascot (animated idle state)
Background: #ff6200 (ING Orange)
Shadow: Elevation 6dp
Animation: 
  - Idle: Subtle breathing animation
  - Attention: Gentle bounce when Leo has suggestion
  - Active: Scales to 1.1x when pressed
Behavior:
  - Tap: Opens Leo Chat Overlay
  - Long press: Shows quick actions menu
  - Badge: Shows notification dot when Leo has proactive suggestion
```

#### 2. Leo Chat Overlay
**Modal that appears over any screen**

```
Component: LeoChatOverlay
Type: Bottom sheet (expandable to full screen)
Initial height: 60% of screen
Max height: 95% of screen (drag to expand)
Background: White with rounded top corners (16dp radius)

Header:
  - Leo avatar (40dp)
  - "Leo" text label
  - Mode toggle: [General] [Quiz] (pill buttons)
  - Close button (X icon)

Chat Area:
  - ScrollView with message bubbles
  - User messages: Right-aligned, #f4f4f4 background
  - Leo messages: Left-aligned, white background with #e0e0e0 border
  - Typing indicator: Three animated dots

Input Bar:
  - Text field (rounded, placeholder: "Ask Leo anything...")
  - Voice button (microphone icon)
  - Camera button (opens document scanner)
  - Attachment button (file picker)
  - Send button (#ff6200 when active)

Inline Widgets (appear in chat):
  - StockWidget: Mini stock chart + price + change%
  - GraphWidget: Line/bar chart visualization
  - DiagramWidget: Pie chart for spending
  - TransferPrompt: Quick send money card
  - QuizCard: Multiple choice question card
```

#### 3. Smart Notification Cards
**AI-triggered notifications**

```
Component: SmartNotificationCard
Type: Push notification + In-app card
Background: White
Border-left: 4dp #ff6200 accent

Structure:
  - Leo icon (24dp)
  - Title (bold, 16sp): "Leo suggests..."
  - Message (14sp): AI-generated suggestion
  - Action buttons (0-2 buttons):
    - Primary: #ff6200 background, white text
    - Secondary: Outlined, #ff6200 border
  - Dismiss button (X)

Examples:
  - "Rent is due today. Send €800 to Landlord?" [Send Now] [Later]
  - "You spent €50 more on dining this week. Want to see the breakdown?" [Show Me]
  - "Your Netflix trial ends tomorrow. Cancel subscription?" [Yes] [Keep It]
```

---

### Screen Specifications for ING Junior Profile

#### Screen J1: Junior Home Dashboard
**First screen after login for Junior users**

```
Screen: JuniorHomeDashboard
Navigation: Bottom tab "Home" (house icon)

Header Section:
  - Greeting: "Hey [Name]! 👋" (dynamic, time-based)
  - Leo speech bubble: AI-generated daily tip or challenge
  - Streak counter: "🔥 5 day streak!" (gamification)

Virtual Balance Card:
  - Background: Gradient #ff6200 to #ff8533
  - Virtual balance: "€2,450.00" (large, white)
  - Label: "Virtual Money" with info tooltip
  - Subtext: "Next salary: Monday (+€200)"
  - Leo mini-avatar corner badge

Quick Stats Row:
  - Portfolio value: "€1,200" with trend arrow
  - This week's gains: "+€45.20" (green) or "-€12.50" (red)
  - Points earned: "🏆 340 pts"

AI Insights Card:
  - Title: "Leo's Insight"
  - Dynamic content: AI-generated observation about user's activity
  - Example: "You've been researching tech stocks. Want a quiz about ETFs?"
  - Action button: [Take Quiz] or [Learn More]

Recent Activity Section:
  - List of last 5 virtual transactions
  - Each row: Icon, description, amount, time
  - Tap to expand with Leo explanation

Bottom Navigation:
  - Home (active)
  - Invest
  - Learn
  - Profile
```

#### Screen J2: Junior Investment Simulator
**Virtual stock trading interface**

```
Screen: JuniorInvestmentSimulator
Navigation: Bottom tab "Invest" (chart icon)

Tab Bar (top):
  - [Portfolio] [Watchlist] [News] [Discover]

Portfolio View (default tab):
  Header:
    - "My Portfolio"
    - Total value: "€1,234.56"
    - Daily change: "+€23.45 (+1.9%)" with color coding
    - Leo FAB shows "?" when user hovers over unfamiliar term

  Holdings List:
    - Each stock card:
      - Company logo (48dp)
      - Company name + ticker
      - Shares owned: "5 shares"
      - Current value + change %
      - Mini sparkline chart (7 days)
      - Tap to open Stock Detail Screen

  Cash Available Card:
    - "💰 Cash: €500.00"
    - "Available to invest"
    - [+ Add Funds] button (simulated)

  Leo Integration:
    - FAB pulsates when portfolio drops >5%
    - Tap shows: "Your tech stocks dropped. This is normal! Want to learn why?"

Discover Tab:
  - AI-curated stock suggestions
  - "Leo's Picks for You" section
  - Categories: Tech, Green Energy, Gaming, etc.
  - Each with Leo's explanation of why it fits user's profile
```

#### Screen J3: Junior Quiz Mode
**Gamified learning interface**

```
Screen: JuniorQuizMode
Navigation: From Leo FAB → Quiz Mode OR Learn tab

Quiz Selection:
  - Topic cards (swipeable):
    - 📈 Investing Basics (completion %)
    - 💼 Taxes 101 (completion %)
    - 🏠 Insurance Explained (completion %)
    - 💳 Smart Spending (completion %)
  - Each shows: Icon, title, progress bar, points available

Active Quiz View:
  Header:
    - Topic name
    - Progress: "Question 3/10"
    - Points at stake: "+15 pts"
    - Streak multiplier: "2x"

  Question Card:
    - AI-generated question text
    - Optional: Generated scenario image
    - Answer options (A, B, C, D) - large tap targets
    - 60-second timer (visual countdown ring)

  Answer Feedback:
    - Correct: Confetti animation + "+15 pts" toast
    - Wrong: Leo explanation appears
    - "Leo explains:" card with simple breakdown
    - [Got it!] button to continue

  Quiz Complete Screen:
    - Score summary
    - Points earned
    - Streak update
    - Leo message: "Great job! You now know more about..."
    - [Share Result] [Play Again] [Back to Learning]
```

#### Screen J4: Junior Leaderboard
**Social competition interface**

```
Screen: JuniorLeaderboard
Navigation: Profile tab → Leaderboards

Tab Bar:
  - [Weekly] [All-Time] [My School]

Leaderboard List:
  - Current user highlighted in #ff6200 background
  - Each row:
    - Rank (#1, #2, #3 have medal icons 🥇🥈🥉)
    - Avatar
    - Username (or anonymous option)
    - Points
    - Trend arrow (up/down from last week)

Weekly Prize Card (top):
  - "🏆 This Week's Prize"
  - Prize description: "€25 bonus to your real ING account at 18!"
  - Time remaining: "3 days 14 hours"
  - Current leader preview

My Stats Card:
  - Your rank: #42
  - Points: 1,240
  - "Need 60 more points to reach #40"
  - Leo tip: "Complete 2 more quizzes to climb 5 spots!"

School Championship Section:
  - School name + logo
  - School rank among all schools
  - [Invite classmates] button
```

#### Screen J5: Junior Salary/Taxes View
**Educational salary breakdown**

```
Screen: JuniorSalaryView
Trigger: Automatic popup when weekly "salary" arrives

Initial Popup:
  - "💰 Your Weekly Salary Arrived!"
  - Amount: "€200.00"
  - [See Breakdown] [Later]

Full View:
  Receipt-style card:
    - "SALARY RECEIPT" header
    - Gross salary: €200.00
    - Deductions section:
      - Income tax: -€30.00 (tap for Leo explanation)
      - Social security: -€15.00 (tap for Leo explanation)
      - Health insurance: -€10.00 (tap for Leo explanation)
    - Net salary: €145.00 (highlighted, green)
    
  Leo Education Card:
    - "This is how real salaries work!"
    - Animated infographic showing money flow
    - "In real life, these taxes pay for..."
    - [Take the Tax Quiz] button

  Historical View:
    - Chart showing weekly salary over time
    - "Your total earned: €2,400"
    - "Taxes paid: €440"
```

---

### Screen Specifications for ING Adult Profile

#### Screen A1: Adult Home Dashboard
**Main banking screen for adult users**

```
Screen: AdultHomeDashboard
Navigation: Bottom tab "Konten" (wallet icon)

Header:
  - "Good morning, [Name]" (time-based greeting)
  - Leo icon with notification badge if suggestion available

Accounts Overview:
  - Girokonto card:
    - Balance: €3,456.78 (large)
    - Account number (masked): •••• 4523
    - Quick actions: [Transfer] [Cards]
  - Extra-Konto card (savings):
    - Balance: €12,340.00
    - Interest rate badge: "1.5% p.a."
  - Depot card (investments):
    - Portfolio value: €8,234.56
    - Daily change indicator

Leo AI Insights Widget:
  - Position: Below accounts, above transactions
  - Background: Light blue (#e3f2fd)
  - Content: AI-generated insight
  - Examples:
    - "You have 3 subscriptions you haven't used this month"
    - "Your spending on dining increased 23% this week"
    - "You could save €200/month by refinancing your..."
  - [Tell Me More] button → Opens Leo chat with context

Recent Transactions:
  - Smart categorization (AI-assigned icons)
  - Each row: Merchant logo, name, amount, category
  - Tap transaction → Leo explains category + similar past transactions

Smart Actions Bar (AI-triggered):
  - Appears when Leo detects action opportunity
  - Example: "Rent due tomorrow → [Pay €800 now]"
  - Dismiss with swipe
```

#### Screen A2: Adult Leo Chat (Full Feature)
**Comprehensive AI assistant interface**

```
Screen: AdultLeoChat
Navigation: Leo FAB from any screen

Chat Interface:
  Header:
    - Leo avatar + name
    - Online status indicator
    - [Voice Mode] toggle
    - Settings gear icon

  Pre-populated Suggestions:
    - "How much did I spend on food this month?"
    - "Explain my last electricity bill"
    - "Should I invest in ETFs?"
    - "Analyze my subscriptions"

  Conversation Features:
    - Inline stock charts when discussing investments
    - Inline pie charts for spending breakdowns
    - Transaction cards with "Pay Now" buttons
    - Document preview cards (when scanning)

  Voice Mode:
    - Full screen takeover
    - Large Leo avatar (animated speaking)
    - Voice waveform visualization
    - "Listening..." / "Thinking..." / "Speaking..." states
    - Tap to interrupt

  Document Analysis Mode:
    - Camera opens with document frame guide
    - Auto-capture when document detected
    - Processing animation
    - Results in chat with highlighted key terms
    - Follow-up: "This insurance costs €50/month. Want me to find cheaper options?"
```

#### Screen A3: Adult Smart Statistics
**AI-powered financial analytics**

```
Screen: AdultSmartStatistics
Navigation: Konten → Statistics OR Ask Leo "Show my statistics"

Overview Card:
  - "Your Financial Health"
  - Score (1-100) with colored ring (red→yellow→green)
  - Leo-generated summary: "You're doing well! Spending is 5% under budget"

Spending Breakdown:
  - Animated pie chart
  - Categories: Housing, Food, Transport, Shopping, Subscriptions, Other
  - Tap category to drill down
  - Compare to: Last month / Last year / Average user

Income vs Expenses Graph:
  - Line chart with dual axis
  - Income line (green)
  - Expenses line (red)
  - Net savings area (blue fill)
  - Toggle: Weekly / Monthly / Yearly

AI Insights Section:
  - "🔍 Leo Found..."
  - List of discoveries:
    - "You paid for Spotify twice in November"
    - "Your grocery spending drops on weekends"
    - "You have €500 sitting idle - consider investing?"
  - Each with [Fix It] or [Learn More] action

Natural Language Query:
  - Search bar at top
  - "Ask about your finances..."
  - Voice input option
  - Example queries shown as chips
```

#### Screen A4: Adult Subscription Manager
**AI-powered subscription tracking**

```
Screen: AdultSubscriptionManager
Navigation: Konten → Subscriptions OR Ask Leo "Show my subscriptions"

Summary Card:
  - Total monthly: €89.99
  - Active subscriptions: 8
  - Leo flag: "2 potential issues found"

Subscription List:
  - Each card:
    - Service logo
    - Name
    - Monthly cost
    - Last charged date
    - AI flag (if unused/duplicate detected)

  AI Flags:
    - 🟡 "Not used in 30 days" (Netflix)
    - 🔴 "Duplicate service" (Spotify + Apple Music)
    - 🟢 "Good value" (no action needed)

  Tap subscription for detail:
    - Usage analysis (if detectable)
    - Total spent lifetime
    - Leo recommendation
    - [Cancel via Leo] [Keep]

Optimization Card:
  - "💡 Leo's Suggestions"
  - "Cancel these to save €35/month:"
  - List with one-tap cancel buttons
  - Total savings calculator
```

#### Screen A5: Adult Investment View
**Real investment portfolio with AI guidance**

```
Screen: AdultInvestmentView
Navigation: Bottom tab "Investieren"

Portfolio Summary:
  - Total value: €15,234.56
  - Daily change: +€123.45 (+0.82%)
  - Performance chart (1D/1W/1M/1Y/ALL)

Holdings List:
  - Each holding:
    - Logo + Name + Ticker
    - Shares × Price = Value
    - Gain/Loss (% and €)
    - Allocation percentage bar

Leo Investment Advisor:
  - Persistent card at bottom
  - "Based on your profile:"
  - Suggestions like:
    - "Your portfolio is tech-heavy. Diversify?"
    - "This ETF matches your sustainability preference"
  - [Ask Leo More] expands to full chat

Trade Actions:
  - [Buy] → Opens order flow with Leo guidance
  - [Sell] → Shows tax implications via Leo
  - Leo explains each step if user hesitates

News Integration:
  - "News affecting your portfolio"
  - AI-summarized articles
  - Relevance explained: "This news is about Apple (10% of your portfolio)"
```

---

### Shared Screen Specifications (Both Profiles)

#### Screen S1: Stock Detail View
**Individual stock information**

```
Screen: StockDetailView
Navigation: Tap any stock from portfolio/watchlist/search

Header:
  - Company logo (large, 64dp)
  - Company name
  - Ticker symbol
  - Current price (large)
  - Change: +€2.34 (+1.5%) with color

Price Chart:
  - Interactive line chart
  - Time range selector: [1D] [1W] [1M] [3M] [1Y] [ALL]
  - Touch to see price at point in time
  - Volume bars below

Key Metrics Grid:
  - Market cap
  - P/E ratio
  - 52-week high/low
  - Dividend yield
  - Each with (?) icon → Leo explains on tap

Leo Integration (Corner Overlay):
  - Leo avatar (small)
  - Expandable panel
  - Default text: "Want me to explain this stock?"
  - Junior: "Take a quiz about [Company]?"
  - Adult: "How does this fit your portfolio?"

Action Buttons:
  - Junior: [Add to Watchlist] [Practice Trade]
  - Adult: [Buy] [Sell] [Add to Watchlist]

News Section:
  - "Latest News about [Company]"
  - AI-summarized headlines
  - Sentiment indicator (positive/neutral/negative)
```

#### Screen S2: Onboarding Flow
**First-time user experience**

```
Flow: OnboardingFlow
Screens: 5-step wizard

Step 1: Welcome
  - Leo animation (friendly wave)
  - "Hi! I'm Leo, your AI financial assistant"
  - "I'll help you learn and manage money"
  - [Let's Start] button

Step 2: Profile Type
  - "Tell me about yourself"
  - Options:
    - "I'm new to finance" → Junior path emphasis
    - "I want to manage my money better" → Adult path emphasis
    - "I want to learn investing" → Both
  - Leo adapts future content based on selection

Step 3: Goals
  - "What are your financial goals?"
  - Multi-select cards:
    - 🎓 Save for education
    - 🏠 Save for a home
    - 🚗 Buy a car
    - 💼 Build emergency fund
    - 📈 Grow wealth
    - 🎮 Just explore
  - Leo: "Great choices! I'll remember these"

Step 4: Risk Preference
  - "How do you feel about risk?"
  - Visual slider with descriptions:
    - Conservative: "I prefer safety over high returns"
    - Moderate: "Balance of safety and growth"
    - Aggressive: "I'm okay with ups and downs for higher potential"
  - Leo shows example scenarios for each level

Step 5: Notifications
  - "How should I reach you?"
  - Toggles:
    - Daily tip from Leo
    - Weekly financial summary
    - Smart action suggestions
    - Quiz reminders (Junior only)
    - Market alerts (if invested)
  - [Complete Setup] button

Completion:
  - Confetti animation
  - "You're all set!"
  - "Your first tip: [AI-generated based on profile]"
  - [Go to Home]
```

#### Screen S3: Settings & Privacy
**User preferences and data control**

```
Screen: SettingsPrivacy
Navigation: Profile tab → Settings

Profile Section:
  - Photo
  - Name
  - Email
  - Phone
  - [Edit Profile]

Leo Preferences:
  - Personality: [Friendly] [Professional] slider
  - Proactivity: [More suggestions] ← → [Less suggestions]
  - Voice: Male/Female/Off
  - Language: German/English

Privacy & Data:
  - "What Leo can access:"
    - ✅ Transaction history
    - ✅ Account balances
    - ⬜ Location data
    - ✅ Document scans (temporary)
  - [View my data] → Export option
  - [Delete my data] → Confirmation flow

Notifications:
  - Master toggle
  - Individual toggles for each type
  - Quiet hours setting

Accessibility:
  - High contrast mode
  - Font size slider
  - Screen reader optimization
  - Reduce animations

Security:
  - Biometric login toggle
  - Change PIN
  - Login history
  - Active sessions

Legal:
  - Terms of service
  - Privacy policy
  - AI transparency information
  - "How Leo works" explainer
```

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

## Answered Questions & Decisions

> This section documents all major design decisions and answers to questions raised in issues.

### Q1: Why two profiles in one app instead of separate apps?
**Issue**: [#31](https://github.com/Wladefant/leo/issues/31)

**Answer**: 
- **Cost Efficiency**: One codebase, one maintenance team, one infrastructure
- **Seamless Transition**: When Junior users turn 18, they upgrade within the same app
- **Familiarity**: Leo remains their trusted assistant across life stages
- **Technical Simplicity**: Profile-based feature toggling is simpler than app switching
- **ING Requirement**: Must integrate into existing ING app (from Q&A session)

### Q2: How do we verify age for Junior users?
**Issue**: [#50](https://github.com/Wladefant/leo/issues/50)

**Answer**:
- **Initial**: Parental consent flow during Girokonto Junior account creation
- **Verification**: Connected to ING's existing KYC (Know Your Customer) process
- **Not a simple Y/N**: Requires parental email/phone verification
- **Compliance**: Meets GDPR Article 8 requirements for minors in Germany (under 16)

### Q3: What happens if Leo is asked non-financial questions?
**Issue**: [#35](https://github.com/Wladefant/leo/issues/35)

**Answer**:
- Leo politely redirects: "I'm your financial assistant, so I focus on money topics. But I'd love to help with questions about saving, investing, or managing your finances!"
- Leo can make the connection: "That's not quite my area, but if you're thinking about buying that car, want to see how it fits your budget?"
- Never abruptly refuses—always offers a financial angle

### Q4: How does the gamification work without physical rewards?
**Issues**: [#15](https://github.com/Wladefant/leo/issues/15), ING Q&A

**Answer**:
- **Points**: Earned for quizzes, streaks, achievements
- **Digital Badges**: Duolingo-style ("Quiz Master", "Saver Starter")
- **Financial Rewards**: Interest rate bonuses on real accounts when turning 18
- **Leaderboards**: Social competition without material prizes
- **School Championships**: Bragging rights, school-level recognition
- **No Merchandise**: ING policy prohibits physical gifts

### Q5: How does Leo generate quizzes dynamically?
**Issues**: [#17](https://github.com/Wladefant/leo/issues/17), [#18](https://github.com/Wladefant/leo/issues/18)

**Answer**:
- **Context Awareness**: If user just viewed Apple stock, quiz might ask about tech sector
- **Adaptive Difficulty**: Algorithm tracks correct/wrong answers, adjusts complexity
- **Image Generation**: Scenario-based questions can include AI-generated illustrations
- **Knowledge Gaps**: Leo identifies weak areas and creates targeted questions
- **Real-World Relevance**: Questions tied to user's actual virtual portfolio/transactions

### Q6: What data does Leo have access to?
**Issues**: [#19](https://github.com/Wladefant/leo/issues/19), [#50](https://github.com/Wladefant/leo/issues/50)

**Answer**:
- **Transaction History**: Full access with user consent
- **Account Balances**: Real-time access
- **User Preferences**: Goals, risk tolerance, learning progress
- **Market Data**: Real-time stock prices, news
- **NOT Accessible**: Location data (unless explicitly enabled), biometric data

### Q7: How do we handle duplicate subscriptions detection?
**Issues**: [#42](https://github.com/Wladefant/leo/issues/42), [#6](https://github.com/Wladefant/leo/issues/6)

**Answer**:
- **Pattern Recognition**: AI identifies similar services (Spotify + Apple Music)
- **Usage Analysis**: Cross-reference with app usage data (if permitted)
- **Timing Analysis**: Subscriptions not used for 30+ days flagged
- **User Control**: All suggestions are recommendations, not automatic actions
- **Transparency**: Leo explains why a subscription was flagged

### Q8: How does the Investment Simulator prevent "gambling" behavior?
**Issue**: [#5](https://github.com/Wladefant/leo/issues/5)

**Answer**:
- **No Reset**: Cannot reset virtual money to avoid consequence-free gambling
- **Weekly Salary**: Controlled income stream, like real life
- **Leo Warnings**: Alerts when behavior is risky ("You're putting all money in one stock")
- **Educational Friction**: Before any trade, Leo offers a brief explanation
- **Loss Limits**: If portfolio drops >50%, Leo intervenes with educational content

### Q9: What is the EU AI Act classification for Leo?
**Issue**: [#50](https://github.com/Wladefant/leo/issues/50)

**Answer**:
- **Classification**: Limited Risk (not High-Risk)
- **Why Not High-Risk**: Does not evaluate creditworthiness, insurance pricing, or essential benefits
- **Primary Obligation**: Transparency (users must know they're talking to AI)
- **Implementation**: Clear "AI Assistant" label, "How Leo Works" explainer in settings

### Q10: How do we ensure Leo doesn't manipulate users?
**Issue**: [#50](https://github.com/Wladefant/leo/issues/50), ING Leo Considerations PDF

**Answer**:
- **No Pressure Tactics**: Leo never urges immediate action
- **No Hidden Upselling**: Leo doesn't secretly promote ING products
- **Balanced Information**: Always presents pros and cons
- **Human Escalation**: Option to speak to human advisor available
- **Audit Trail**: All Leo recommendations logged for review
- **Ethical Review**: Content reviewed by ethics board before deployment

### Q11: How do Smart Notifications work?
**Issues**: [#52](https://github.com/Wladefant/leo/issues/52), [#53](https://github.com/Wladefant/leo/issues/53)

**Answer**:
- **Pattern Learning**: AI learns recurring transactions (rent, subscriptions)
- **Proactive Suggestions**: "Rent due tomorrow. Send €800?" (pre-filled)
- **One-Tap Actions**: Reduce friction for routine tasks
- **Timing Intelligence**: Sends reminders at optimal times
- **Dismissable**: Never forced; always can be snoozed/dismissed
- **Learning**: If user always dismisses, Leo stops suggesting that action

### Q12: What makes Leo different from ChatGPT or generic AI?
**Issue**: [#26](https://github.com/Wladefant/leo/issues/26) (USP)

**Answer**:
- **Financial Focus**: Can't be distracted, always brings back to money topics
- **Bank Integration**: Has access to actual transaction data
- **Verified Knowledge**: No hallucinations about financial facts
- **Compliance Built-In**: EU AI Act, GDPR, minors protection from day one
- **Action Capability**: Can actually execute transactions (with confirmation)
- **Personalized Learning**: Adapts to user's actual financial behavior

### Q13: How do we handle accessibility and inclusion?
**Issue**: [#23](https://github.com/Wladefant/leo/issues/23)

**Answer**:
- **Visual**: High contrast mode, adjustable font sizes
- **Auditory**: Voice mode for all interactions
- **Cognitive**: Simple language, no jargon, step-by-step guidance
- **Motor**: Large tap targets, voice control option
- **Language**: German and English support
- **Dyslexia-Friendly**: OpenDyslexic font option
- **Screen Readers**: Full VoiceOver/TalkBack compatibility

### Q14: What is the knowledge base source?
**Issue**: [#29](https://github.com/Wladefant/leo/issues/29)

**Answer**:
- **Recommended**: Purchase API from financial education provider
- **Content Types**: German tax laws, investment basics, insurance explanations
- **Quality Control**: All content human-reviewed before deployment
- **Updates**: Regular updates when regulations change
- **No Internet Scraping**: Closed environment prevents misinformation

---

## Presentation Strategy

> **Issue**: [#27](https://github.com/Wladefant/leo/issues/27)

### Slide Deck Structure (Max 8 Slides)

**Slide 1: Title**
- "LEO: Your AI Financial Companion"
- Team name and members
- DFC2025 + ING logos

**Slide 2: The Problem**
- Pain points of young users (anxiety, confusion, lack of knowledge)
- Statistics: Only 25% of Germans feel financially literate
- Quote from target user research

**Slide 3: Our Solution - LEO**
- AI-First approach (everything starts with Leo)
- Two profiles: Junior (learn) + Adult (manage)
- Key differentiator: Integrated, not another app

**Slide 4: How It Works**
- User journey visualization
- Junior: Virtual money → Quiz → Real skills
- Adult: Transaction insight → Smart suggestions → Action

**Slide 5: Live Demo Mockup**
- Interactive prototype link
- 3-4 key screens showing Leo in action
- Show AI-generated quiz example

**Slide 6: Why This Matters**
- Social relevance (financial literacy gap)
- Future viability (AI is the future of banking)
- Inclusion (accessible to all)

**Slide 7: Feasibility**
- Technical: Built on existing ING infrastructure
- Legal: EU AI Act compliant (Limited Risk)
- Timeline: Realistic 18-24 month rollout
- ING fit: Matches risk-averse culture

**Slide 8: Call to Action + Sources**
- "Ready to meet Leo?"
- MVP/Prototype link
- Academic and industry sources
- Team contact information

### Key Talking Points

1. **AI-First, Not AI-Added**: Leo isn't a feature—it's THE interface
2. **Two Profiles, One App**: Grow with users from teen to adult
3. **Safe Learning**: Virtual money with real consequences (no reset)
4. **Smart Insights**: AI that actually knows your finances
5. **Compliance by Design**: GDPR, EU AI Act, minors protection

### Anticipated Jury Questions

| Question | Prepared Answer |
|----------|----------------|
| "Why not a separate app for teens?" | Cost efficiency, seamless transition at 18, ING app integration requirement |
| "How do you prevent AI manipulation?" | Transparency, no hidden upselling, human escalation, audit trails |
| "Is this technically feasible?" | Yes, uses existing LLM technology + ING APIs; no quantum computing |
| "How do you handle privacy for minors?" | GDPR Article 8 compliance, parental consent flow, highest privacy defaults |
| "What's the business model?" | Builds loyalty—teens become adult customers; subscription optimization saves money |

### Prototype Requirements

- [ ] Working Leo chat interface (can be mock responses)
- [ ] At least 3 complete screens (Home, Chat, Quiz)
- [ ] One user flow end-to-end (e.g., Take a Quiz)
- [ ] Visual consistency with ING design system
- [ ] Leo personality demonstration

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

## Proposed New Issues

> These are new features and improvements identified during documentation that should be created as GitHub issues.

### AI-First Features (Priority: High)

#### NEW: Leo Proactive Conversation Starters
**Labels**: feature, ING APP, ING Junior, AiChat
```
Description: Leo shouldn't wait for users to ask questions. Based on user behavior and context, 
Leo should proactively start conversations.

Examples:
- "I noticed you viewed Apple stock 3 times this week. Want me to explain what's happening?"
- "You've been saving consistently! Have you thought about where this money could grow?"
- "Your rent payment bounced last month. Want help setting up a buffer fund?"

AI-First Principle: Leo is proactive, not reactive.
```

#### NEW: Leo Voice Personality Settings
**Labels**: feature, ING APP, ING Junior, AiChat
```
Description: Users should be able to customize Leo's voice and personality.

Options:
- Voice: Male / Female / Non-binary
- Tone: Friendly / Professional / Casual
- Emoji usage: On / Off / Minimal
- Verbosity: Detailed / Concise
- Language: German / English

Junior-specific: More playful tone, more emojis, simpler vocabulary
Adult-specific: More professional options, business terminology available
```

#### NEW: Leo Learning Mode Detection
**Labels**: feature, ING Junior, AiChat
```
Description: Leo detects when user is confused or struggling and automatically offers help.

Signals:
- User scrolling back and forth on same screen
- User opening and closing same feature repeatedly
- User typing questions but deleting them
- Long pauses during quiz

Response: Leo gently appears: "Looks like you might have questions. Can I help explain something?"
```

#### NEW: Leo Context Memory Across Sessions
**Labels**: feature, ING APP, ING Junior, AiChat
```
Description: Leo remembers conversations across sessions and references previous discussions.

Examples:
- "Last week you asked about ETFs. Ready to take the next step?"
- "Remember when you set that savings goal? You're 60% there!"
- "You were curious about Tesla. It's up 5% since we talked."

Privacy: User can clear conversation history anytime.
```

### Junior Profile Features (Priority: High)

#### NEW: Parent Dashboard
**Labels**: feature, ING Junior, Screens/View
```
Description: Parents of Junior users need visibility into their child's learning progress.

Features:
- View child's quiz scores and topics covered
- See virtual portfolio performance
- Approve/deny simulated purchases over certain amounts
- Set weekly screen time limits
- Receive weekly progress reports via email

NOT included:
- Cannot see chat conversations (privacy for teens)
- Cannot make investment decisions for child
```

#### NEW: Teen-to-Adult Transition Flow
**Labels**: feature, ING Junior, ING APP, Screens/View
```
Description: When Junior user turns 18, they transition to adult profile with celebration.

Flow:
1. On 18th birthday: Special Leo message + animation
2. "You're officially an adult now! Let's unlock your full account."
3. Show earned achievements and points
4. Convert virtual portfolio learnings to real suggestions
5. Optionally convert accumulated points to welcome bonus
6. Full ING features unlock

No data loss: All learning progress, quiz history preserved
```

#### NEW: School Registration Portal
**Labels**: feature, ING Junior, Screens/View
```
Description: Schools can register for Leo Education Program.

Features:
- School admin creates class groups
- Teachers track class progress
- Inter-class competitions
- School leaderboard
- Curriculum alignment tools
- Parent consent management

Partnership opportunity for ING.
```

### Adult Profile Features (Priority: Medium)

#### NEW: Bill Negotiation Assistant
**Labels**: feature, ING APP, AiChat
```
Description: Leo helps users negotiate bills and subscriptions.

Features:
- Identify bills that could be reduced (electricity, internet, insurance)
- Generate negotiation scripts
- Track negotiation outcomes
- Suggest competitors with better rates
- (Future) Actually negotiate on user's behalf via API

Example: "Your electricity bill is €50/month higher than average. Want me to draft a 
message to your provider asking for a better rate?"
```

#### NEW: Financial Goal Collaboration
**Labels**: feature, ING APP, Screens/View
```
Description: Couples/families can set shared savings goals.

Features:
- Invite partner to shared goal
- Combined progress tracking
- Split contributions automatically
- Leo celebrates joint milestones
- Individual contribution visibility

Example: "House fund: €12,000 / €50,000 (Lisa: €7,000, Max: €5,000)"
```

#### NEW: Investment Decision Explainer
**Labels**: feature, ING APP, AiChat
```
Description: Before any trade, Leo explains the decision in simple terms.

Features:
- Tax implications: "If you sell now, you'll owe €X in taxes"
- Portfolio impact: "This will make Apple 30% of your portfolio"
- Risk assessment: "This stock is more volatile than average"
- Alternative suggestions: "Have you considered this similar ETF?"
- Historical context: "The last time you sold during a dip, you regretted it"
```

### Technical Features (Priority: Medium)

#### NEW: Leo Offline Mode
**Labels**: feature, ING APP, ING Junior
```
Description: Basic Leo functionality when internet unavailable.

Available offline:
- View cached account balances
- See recent transactions
- Access downloaded quiz content
- Read saved financial tips

Not available offline:
- New AI conversations
- Real-time stock prices
- Send money

Sync: Automatically syncs when connection restored
```

#### NEW: Leo Widget for Home Screen
**Labels**: feature, ING APP, ING Junior
```
Description: iOS/Android home screen widget showing Leo insights.

Widget sizes:
- Small: Daily tip from Leo
- Medium: Account balance + tip
- Large: Balance + recent transactions + AI insight

Tap to expand: Opens app to relevant screen
Privacy: Can hide balance on widget
```

#### NEW: Leo API for Third-Party Integration
**Labels**: feature, ING APP, documentation
```
Description: Allow approved third-party apps to query Leo (with user consent).

Use cases:
- Budgeting apps asking "What's my spending category breakdown?"
- Tax software asking "What's my investment income this year?"
- Financial planning apps getting personalized insights

Security: OAuth 2.0, user explicit consent, audit logs
```

### Accessibility Features (Priority: High)

#### NEW: Leo Sign Language Mode
**Labels**: feature, ING APP, ING Junior, accessibility
```
Description: Leo avatar can communicate using sign language animations.

Implementation:
- Pre-rendered sign language animations for common phrases
- Real-time generation for custom responses
- German Sign Language (DGS) primary
- Optional subtitles alongside

Inclusive design: Makes Leo accessible to deaf/hard-of-hearing users
```

#### NEW: Simplified Language Mode
**Labels**: feature, ING APP, ING Junior, accessibility
```
Description: Ultra-simplified language for users with cognitive disabilities.

Features:
- Maximum 10 words per sentence
- Common words only (no financial jargon)
- Large, clear fonts
- Pictographic support
- Slower animations
- Repetition options

WCAG compliance: AAA level support
```

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
