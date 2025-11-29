# News & Insights Feed - Complete Specification

> This document details the personalized news feed system with Perplexity-style AI summarization, stock-specific news, and "For You" page functionality.

---

## Table of Contents
1. [Overview](#overview)
2. [News Sources & Integration](#news-sources--integration)
3. [AI Summarization](#ai-summarization)
4. [For You Page](#for-you-page)
5. [Stock-Specific News](#stock-specific-news)
6. [Notification System](#notification-system)
7. [UI Specifications](#ui-specifications)
8. [User Stories for Demo](#user-stories-for-demo)

---

## Overview

The LEO News system provides personalized financial news that:
- **Is relevant**: Filtered based on user's portfolio and watchlist
- **Is understandable**: AI-summarized in plain language
- **Is actionable**: Connected to user's actual investments
- **Is timely**: Real-time alerts for portfolio-affecting news

### Key Principles

1. **No noise**: Only show news that matters to the user
2. **Context first**: Explain WHY this news matters to them
3. **Leo explains**: Every article can be expanded with Leo's analysis
4. **Action-oriented**: Clear next steps when relevant

---

## News Sources & Integration

### Recommended News APIs

| Provider | Pros | Cons | Cost |
|----------|------|------|------|
| **NewsAPI** | Wide coverage, easy integration | Rate limits | Free tier + paid |
| **Alpha Vantage** | Financial focus, stock data included | Limited articles | Free tier |
| **Bloomberg API** | Premium content, authoritative | Expensive | Enterprise |
| **Reuters API** | Real-time, trusted | Expensive | Enterprise |
| **Yahoo Finance** | Free, good stock coverage | Less premium content | Free |
| **Google News API** | Wide coverage | Requires filtering | Free |

### Recommended Setup

```
Primary: NewsAPI (general financial news)
+ Yahoo Finance (stock-specific, free)
+ Custom RSS aggregation (German finance sources)
```

### German News Sources to Aggregate

| Source | Type | RSS/API |
|--------|------|---------|
| Handelsblatt | Business news | RSS |
| Börsen-Zeitung | Stock market | RSS |
| Finanznachrichten | Finance | RSS |
| Der Aktionär | Stock tips | RSS |
| Wirtschaftswoche | Business | RSS |
| FAZ Finanzen | Finance section | RSS |
| Manager Magazin | Business | RSS |
| finanztreff.de | Market news | RSS |

### Data Structure

```typescript
interface NewsArticle {
  id: string;
  title: string;
  source: string;
  publishedAt: Date;
  url: string;
  imageUrl?: string;
  
  // Raw content
  fullText: string;
  
  // AI-processed
  summary: string;           // 2-3 sentences
  keyPoints: string[];       // Bullet points
  sentiment: 'positive' | 'negative' | 'neutral';
  relevanceScore: number;    // 0-100
  
  // Connections
  relatedStocks: string[];   // Ticker symbols
  relatedTopics: string[];   // ETF, Tax, Insurance, etc.
  
  // Leo's analysis
  leoExplanation?: string;
  leoAdvice?: string;
  quizPrompt?: string;
}
```

---

## AI Summarization

### Summarization Pipeline

```
Raw Article → Content Extraction → AI Summarization → Relevance Scoring → Storage
```

### GPT Prompt for Summarization

```
You are Leo, a friendly financial assistant helping young users understand financial news.

Article to summarize:
[ARTICLE_TEXT]

User's portfolio:
[USER_STOCKS]

Provide:
1. A 2-3 sentence summary in simple German (Leichte Sprache)
2. 3 bullet points of key takeaways
3. Sentiment (positive/negative/neutral)
4. If relevant to user's stocks, explain the connection
5. A quiz question about this topic (optional)

Format as JSON:
{
  "summary": "...",
  "keyPoints": ["...", "...", "..."],
  "sentiment": "...",
  "portfolioImpact": "...",
  "quizQuestion": {
    "question": "...",
    "options": ["A", "B", "C", "D"],
    "correct": 0
  }
}
```

### Summary Levels by Profile

**Junior Profile:**
```
Original: "Apple Inc. reported Q4 earnings that beat analyst expectations, 
with revenue of $89.5B driven by strong iPhone 15 sales and services growth."

Leo's Summary: "Apple hat mehr Geld verdient als erwartet! 📱 
Das neue iPhone 15 verkauft sich super gut, und viele Menschen 
nutzen Apple-Dienste wie iCloud und Apple Music."
```

**Adult Profile:**
```
Original: [Same article]

Leo's Summary: "Apple übertrifft Q4-Erwartungen mit €89,5 Mrd. Umsatz. 
iPhone 15 und Services-Wachstum treiben die Zahlen. 
Deine Apple-Aktien (+2.3% nachbörslich) profitieren."
```

---

## For You Page

### Perplexity-Style Design

The "For You" page aggregates and presents news like Perplexity's Discover feature:

```
┌─────────────────────────────────────┐
│  📰 Für Dich                        │
│  Personalisiert basierend auf       │
│  deinem Portfolio & Interessen      │
│                                     │
│  ┌─────────────────────────────┐   │
│  │ 🔴 WICHTIG FÜR DICH         │   │
│  │                             │   │
│  │ Apple meldet Rekordumsatz   │   │
│  │                             │   │
│  │ Leo: "Du hast Apple-Aktien! │   │
│  │ Das sind gute Nachrichten   │   │
│  │ für dein Portfolio (+2.3%)" │   │
│  │                             │   │
│  │ [Vollständig lesen]         │   │
│  │ [Leo fragen]                │   │
│  └─────────────────────────────┘   │
│                                     │
│  ──── Heute ────                    │
│                                     │
│  📈 Tech-Aktien steigen            │
│  "Nasdaq erreicht Jahreshoch..."   │
│  💬 Betrifft: AAPL, MSFT           │
│                                     │
│  🇪🇺 EZB hält Zinsen stabil        │
│  "Keine Änderung des Leitzinses"   │
│  💬 Betrifft: Deine Sparkonten     │
│                                     │
│  📊 ETF-Tipp der Woche             │
│  "Warum MSCI World beliebt ist"    │
│  💬 Quiz verfügbar!                │
│                                     │
│  ──── Gestern ────                  │
│  ...                               │
└─────────────────────────────────────┘
```

### Personalization Algorithm

News is ranked by:

1. **Portfolio Relevance** (40%): Does it mention user's stocks?
2. **Interest Match** (25%): Based on quiz topics completed
3. **Recency** (20%): Newer = more relevant
4. **Source Quality** (10%): Trusted sources ranked higher
5. **Engagement History** (5%): Articles similar to ones user read

```typescript
function calculateRelevanceScore(article: NewsArticle, user: User): number {
  let score = 0;
  
  // Portfolio relevance (40%)
  const portfolioStocks = user.portfolio.map(h => h.ticker);
  const watchlistStocks = user.watchlist;
  
  if (article.relatedStocks.some(s => portfolioStocks.includes(s))) {
    score += 40; // Directly affects their money
  } else if (article.relatedStocks.some(s => watchlistStocks.includes(s))) {
    score += 25; // They're interested
  }
  
  // Interest match (25%)
  const userTopics = user.quizHistory.map(q => q.topic);
  if (article.relatedTopics.some(t => userTopics.includes(t))) {
    score += 25;
  }
  
  // Recency (20%)
  const hoursOld = (Date.now() - article.publishedAt) / 3600000;
  score += Math.max(0, 20 - hoursOld / 2); // Decays over ~40 hours
  
  // Source quality (10%)
  score += getSourceQualityScore(article.source) * 0.1;
  
  // Engagement (5%)
  if (userLikesSimilarArticles(user, article)) {
    score += 5;
  }
  
  return score;
}
```

### For You Feed Categories

| Category | Icon | Criteria |
|----------|------|----------|
| **Important for You** | 🔴 | Score > 80, affects portfolio |
| **Your Stocks** | 📈 | Mentions owned stocks |
| **Your Watchlist** | 👀 | Mentions watchlist stocks |
| **Market News** | 📊 | General market updates |
| **Learning** | 📚 | Educational content |
| **Quiz Available** | 🎯 | Has attached quiz |

---

## Stock-Specific News

### News on Stock Detail Page

When viewing a stock, show dedicated news section:

```
┌─────────────────────────────────────┐
│  ING Groep NV                       │
│  €12.45  ▲ +1.2%                   │
│  [Chart...]                         │
│                                     │
│  ──── Leo's Analyse ────            │
│  "ING zeigt stabile Zahlen und     │
│  profitiert von höheren Zinsen.    │
│  Der Bankensektor insgesamt..."    │
│  [Mehr erfahren]                   │
│                                     │
│  ──── News zu ING ────              │
│                                     │
│  📰 ING erhöht Dividende           │
│  vor 2 Stunden • Reuters           │
│  "Mehr Geld für Aktionäre..."      │
│                                     │
│  📰 Banken profitieren von EZB     │
│  vor 5 Stunden • Handelsblatt      │
│  "Zinserhöhung gut für Gewinne..." │
│                                     │
│  📰 ING startet neue App           │
│  vor 1 Tag • Finanzen.net          │
│  "Digitale Innovation im Fokus..." │
│                                     │
│  [Alle 12 News anzeigen →]         │
└─────────────────────────────────────┘
```

### News Alert Triggers

Automatic notifications for:

| Event | Trigger Condition | Notification |
|-------|------------------|--------------|
| **Earnings Report** | Company in portfolio reports | "Apple Q4 Ergebnisse sind da! Leo erklärt..." |
| **Price Movement** | Stock moves >5% | "ING +5% heute! Hier ist warum..." |
| **Analyst Rating** | Rating change | "Goldman Sachs stuft Apple hoch" |
| **Breaking News** | High-impact news mentioning stock | "EILMELDUNG: Tesla kündigt neues Model an" |
| **Market News** | Major index movement | "DAX fällt 2% - was bedeutet das für dich?" |

---

## Notification System

### News Notification Types

#### 1. Breaking News (Immediate)
```
🔴 EILMELDUNG
Apple kündigt Aktienrückkauf an

Du hast 5 Apple-Aktien!
Das könnte den Kurs steigern.

[Leo fragen] [Artikel lesen]
```

#### 2. Portfolio Alert (High Priority)
```
📈 Portfolio-Update
Deine Tesla-Aktien +8% heute

Grund: Rekord-Auslieferungszahlen
Leo: "Gute Nachrichten! Aber..."

[Details ansehen]
```

#### 3. Daily Digest (Scheduled)
```
☀️ Guten Morgen! Dein Finanz-Update:

• DAX: +0.5% (Trend: aufwärts)
• Dein Portfolio: +1.2% diese Woche
• 3 neue Artikel zu deinen Aktien

[Öffnen]
```

#### 4. Learning Opportunity (Contextual)
```
📚 Lernchance!

Die EZB hat den Leitzins geändert.
Weißt du, was das für dein Sparkonto bedeutet?

[Quiz machen +50 XP]
```

### Notification Preferences

```
┌─────────────────────────────────────┐
│  🔔 News-Benachrichtigungen         │
│                                     │
│  Eilmeldungen (Portfolio)           │
│  [████████████░░] An               │
│                                     │
│  Tägliche Zusammenfassung           │
│  [████████████░░] 8:00 Uhr         │
│                                     │
│  Kurs-Alerts (>5% Bewegung)         │
│  [████████████░░] An               │
│                                     │
│  Lern-Tipps                         │
│  [████████░░░░░░] Max 2/Tag        │
│                                     │
│  Allgemeine Marktnews               │
│  [░░░░░░░░░░░░░░] Aus              │
│                                     │
│  Ruhezeiten: 22:00 - 7:00          │
│  [Bearbeiten]                       │
└─────────────────────────────────────┘
```

---

## UI Specifications

### News Card Component

```typescript
interface NewsCardProps {
  article: NewsArticle;
  variant: 'compact' | 'expanded' | 'featured';
  showPortfolioConnection: boolean;
  onAskLeo: () => void;
  onRead: () => void;
}
```

#### Compact News Card
```
┌─────────────────────────────────────┐
│ 📰 Apple meldet Rekordumsatz       │
│ vor 2h • Reuters   💬 AAPL (+2.3%) │
└─────────────────────────────────────┘
```

#### Expanded News Card
```
┌─────────────────────────────────────┐
│ 📰 Apple meldet Rekordumsatz        │
│ vor 2 Stunden • Reuters             │
│                                     │
│ "Apple übertrifft Erwartungen mit   │
│ €89,5 Mrd. Umsatz im Q4. iPhone 15  │
│ und Services treiben das Wachstum." │
│                                     │
│ 💬 Betrifft: AAPL (du hast 5 Aktien)│
│ 📈 Dein Gewinn: +€23.50 heute       │
│                                     │
│ [Vollständig lesen] [Leo fragen]    │
└─────────────────────────────────────┘
```

#### Featured News Card (For You - Important)
```
┌─────────────────────────────────────┐
│ 🔴 WICHTIG FÜR DEIN PORTFOLIO       │
│                                     │
│ Apple meldet Rekordumsatz           │
│ +2.3% nachbörslich                  │
│                                     │
│ ┌─────────────────────────────┐    │
│ │ [Article Image]              │    │
│ └─────────────────────────────┘    │
│                                     │
│ Leo erklärt:                        │
│ "Super Nachrichten für dich! Deine  │
│ 5 Apple-Aktien sind jetzt €23.50   │
│ mehr wert. Das iPhone 15 verkauft  │
│ sich besser als erwartet."         │
│                                     │
│ Key Points:                         │
│ • Umsatz: €89,5 Mrd. (+8% YoY)     │
│ • iPhone: Verkäufe über Erwartung  │
│ • Services: Rekordhoch             │
│                                     │
│ [Ganzen Artikel lesen]              │
│ [Leo fragen]                        │
│ [Quiz zu Earnings +25 XP]          │
└─────────────────────────────────────┘
```

### Investment Dashboard News Tab

```
┌─────────────────────────────────────┐
│  [Portfolio] [News] [Watchlist]     │
│           ═══════                   │
│                                     │
│  ──── Personalisierte News ────     │
│                                     │
│  🔴 Apple Q4 übertrifft Erwartungen │
│     vor 2h • Betrifft: AAPL        │
│                                     │
│  📈 DAX erreicht Jahreshoch         │
│     vor 3h • Allgemeiner Markt     │
│                                     │
│  🏦 EZB lässt Zinsen unverändert   │
│     vor 5h • Betrifft: Sparkonten  │
│                                     │
│  📊 ETF-Zuflüsse auf Rekordhoch    │
│     vor 8h • Lernen               │
│                                     │
│  ──── Weitere News ────             │
│                                     │
│  • Tesla plant neue Fabrik          │
│  • Bitcoin über 40.000$             │
│  • Immobilienmarkt kühlt ab         │
│                                     │
│  [Alle News anzeigen →]             │
└─────────────────────────────────────┘
```

---

## User Stories for Demo

### Story 1: Portfolio-Relevant News Alert
```yaml
ID: news_portfolio_alert
Name: "Breaking News - Your Stock"
Description: "Important news affecting user's portfolio"
Category: both
Duration: ~1 minute

Flow:
1. Push notification: "🔴 News zu deiner Apple-Aktie"
2. User opens to see featured news card
3. Leo explains the impact on their portfolio
4. Option to read full article or quiz

Demo Messages:
- [Push notification arrives]
- Leo: "Wichtige Neuigkeiten zu Apple! 📰"
- [Featured News Card with article]
- Leo: "Das sind gute Nachrichten! Deine 5 Aktien sind jetzt €23.50 mehr wert."
- Leo: "Möchtest du mehr über Quartalsberichte lernen? [Quiz starten +25 XP]"
```

### Story 2: Daily News Digest
```yaml
ID: news_daily_digest
Name: "Morning News Summary"
Description: "Personalized daily financial news roundup"
Category: both
Duration: ~1.5 minutes

Flow:
1. Morning notification: "☀️ Dein Finanz-Morgen"
2. Shows 3-4 most relevant news items
3. Quick stats on portfolio overnight
4. Leo's thought for the day

Demo Messages:
- Leo: "Guten Morgen! ☀️ Hier ist dein Finanz-Update:"
- Leo: "📊 DAX: +0.5% | Dein Portfolio: +€45.20"
- Leo: "📰 3 wichtige News für dich heute:"
- [News list with summaries]
- Leo: "💡 Tipp des Tages: Wusstest du, dass Montage statistisch die schlechtesten Börsentage sind?"
```

### Story 3: For You Page Discovery
```yaml
ID: news_for_you_page
Name: "Discover Your News"
Description: "Browse personalized news feed"
Category: both
Duration: ~2 minutes

Flow:
1. User opens News tab
2. See personalized "For You" feed
3. Leo explains why each article is relevant
4. Deep-dive into one article with quiz

Demo Messages:
- Leo: "Hier ist deine personalisierte Newsübersicht! 📰"
- Leo: "Ich hab 12 Artikel gefunden, die für dich relevant sind."
- [For You feed with 5 articles]
- User taps on EZB article
- Leo: "Die EZB hat die Zinsen nicht geändert. Das bedeutet..."
- [Expanded article with Leo's explanation]
- Leo: "Lust auf ein Quiz zu Zentralbanken? [Quiz +50 XP]"
```

### Story 4: Stock News Deep Dive
```yaml
ID: news_stock_specific
Name: "News About Your Stock"
Description: "View news specific to a stock"
Category: both
Duration: ~1 minute

Flow:
1. User opens Apple stock detail
2. Scroll to news section
3. See latest Apple-specific news
4. Ask Leo about implications

Demo Messages:
- [User on Apple stock page]
- Leo: "Es gibt 8 aktuelle News zu Apple 📰"
- [News section with Apple articles]
- User: "Was bedeutet das für den Kurs?"
- Leo: "Die Earnings waren super! Historisch steigt Apple nach guten Earnings oft um 3-5% in der Folgewoche. Aber Vorsicht: vergangene Performance garantiert keine Zukunft!"
```

### Story 5: Learning from News
```yaml
ID: news_learning_quiz
Name: "Learn from News"
Description: "Turn current event into learning opportunity"
Category: junior
Duration: ~2 minutes

Flow:
1. Leo highlights educational news
2. Explains concept in simple terms
3. Offers quiz to test understanding
4. Awards XP for completion

Demo Messages:
- Leo: "📚 Lernchance! Die Fed hat gerade die Zinsen erhöht."
- Leo: "Weißt du, was eine Zentralbank ist und warum Zinsen wichtig sind?"
- User: "Nicht wirklich..."
- Leo: "Kein Problem! Stell dir vor, die Zentralbank ist wie eine Bank für Banken..."
- [Educational explanation with simple analogies]
- Leo: "Alles verstanden? Lass uns das testen!"
- [Quiz Widget with 3 questions]
- Leo: "Super! +50 XP und du hast das 'Zentralbank Grundlagen' Badge verdient! 🏆"
```

---

## Technical Implementation

### News Aggregation Service

```typescript
class NewsAggregator {
  private sources: NewsSource[];
  private cache: Map<string, NewsArticle>;
  
  async fetchLatestNews(): Promise<NewsArticle[]> {
    const articles = await Promise.all(
      this.sources.map(s => s.fetch())
    );
    return this.deduplicate(articles.flat());
  }
  
  async summarizeArticle(article: NewsArticle): Promise<NewsArticle> {
    const response = await openai.chat({
      model: 'gpt-4',
      messages: [
        { role: 'system', content: NEWS_SUMMARY_PROMPT },
        { role: 'user', content: article.fullText }
      ]
    });
    
    return {
      ...article,
      summary: response.summary,
      keyPoints: response.keyPoints,
      sentiment: response.sentiment
    };
  }
  
  async getPersonalizedFeed(user: User): Promise<NewsArticle[]> {
    const allNews = await this.fetchLatestNews();
    
    return allNews
      .map(article => ({
        article,
        score: calculateRelevanceScore(article, user)
      }))
      .sort((a, b) => b.score - a.score)
      .slice(0, 20)
      .map(item => item.article);
  }
}
```

### News Caching Strategy

```
1. Fetch new articles every 15 minutes
2. Summarize articles in background queue
3. Cache summaries for 24 hours
4. Cache user-specific relevance scores for 1 hour
5. Invalidate cache on portfolio changes
```

---

*Last Updated: November 2025*
