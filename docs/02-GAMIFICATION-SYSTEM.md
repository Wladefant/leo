# Gamification System - Complete Specification

> This document details the gamification system for both Junior and Adult profiles, with emphasis on Kahoot-style challenges, leaderboards, and user engagement mechanisms.

---

## Table of Contents
1. [Points System](#points-system)
2. [Achievements & Badges](#achievements--badges)
3. [Leaderboards](#leaderboards)
4. [Kahoot-Style Challenges](#kahoot-style-challenges)
5. [School Championships](#school-championships)
6. [User Stories for Demo Sidebar](#user-stories-for-demo-sidebar)

---

## Points System

### XP (Experience Points) Economy

#### Earning XP - Junior Profile

| Action | XP Awarded | Frequency Limit |
|--------|-----------|-----------------|
| **Daily Login** | 10 XP | Once/day |
| **Streak Bonus (7 days)** | 50 XP bonus | Weekly |
| **Streak Bonus (30 days)** | 200 XP bonus | Monthly |
| **Complete Quiz (Easy)** | 25-50 XP | Per quiz |
| **Complete Quiz (Medium)** | 50-100 XP | Per quiz |
| **Complete Quiz (Hard)** | 100-200 XP | Per quiz |
| **Perfect Quiz Score** | +50% bonus XP | Per quiz |
| **First Virtual Trade** | 100 XP | Once |
| **Complete Learning Module** | 50-150 XP | Per module |
| **Watch Educational Video** | 20 XP | 5/day max |
| **Read News Article** | 10 XP | 10/day max |
| **Add Stock to Watchlist** | 15 XP | 10/day max |
| **Make Virtual Trade** | 20 XP | 5/day max |
| **Achieve Portfolio Milestone** | 100-500 XP | Per milestone |
| **Win Weekly Challenge** | 500 XP | Once/week |
| **Refer Friend** | 200 XP | Per friend |
| **Complete Daily Challenge** | 30-75 XP | Once/day |
| **Help Classmate (explain feature)** | 25 XP | 3/day max |

#### XP Multipliers

| Condition | Multiplier |
|-----------|------------|
| 7-day streak | 1.5x |
| 14-day streak | 1.75x |
| 30-day streak | 2x |
| 60-day streak | 2.5x |
| Weekend bonus | 1.25x |
| Perfect quiz | 1.5x |
| First attempt | 1.2x |

### Level System

| Level | XP Required | Title | Unlocks |
|-------|-------------|-------|---------|
| 1 | 0 | Finanz-Anfänger | Basic features |
| 2 | 500 | Geld-Lerner | First badge slot |
| 3 | 1,200 | Spar-Fuchs | Custom avatar color |
| 4 | 2,500 | Budget-Held | Second badge slot |
| 5 | 5,000 | Finanz-Entdecker | Hard quizzes unlock |
| 6 | 8,500 | Aktien-Kenner | Advanced stocks |
| 7 | 13,000 | Portfolio-Profi | Third badge slot |
| 8 | 20,000 | Investment-Guru | Custom title |
| 9 | 30,000 | Finanz-Meister | Special badge frame |
| 10 | 50,000 | Leo's Champion | All features + VIP status |

### Real Financial Rewards (No Physical Gifts!)

**Junior Profile - Accumulated at Age 18:**

| XP Milestone | Reward at 18 |
|--------------|--------------|
| 5,000 XP | €5 account bonus |
| 15,000 XP | €15 account bonus |
| 35,000 XP | €35 account bonus |
| 75,000 XP | €75 account bonus |
| 150,000 XP | €150 account bonus + 0.1% interest bonus (1 year) |

**Adult Profile - Immediate Rewards:**

| Achievement | Reward |
|-------------|--------|
| Complete Financial Health checkup | €5 account credit |
| First investment | Free trade |
| 6-month active user | 0.1% interest bonus |
| Refer 3 friends | €25 account credit |

---

## Achievements & Badges

### Badge Categories

#### 🎓 Learning Badges (Education)

| Badge | Criteria | XP Bonus |
|-------|----------|----------|
| **Quiz Newbie** | Complete first quiz | 25 XP |
| **Quiz Regular** | Complete 10 quizzes | 100 XP |
| **Quiz Master** | Complete 50 quizzes | 500 XP |
| **Perfect 10** | Get 10 perfect quiz scores | 250 XP |
| **ETF Expert** | Complete all ETF quizzes | 200 XP |
| **Tax Whiz** | Complete all tax quizzes | 200 XP |
| **Insurance Insider** | Complete all insurance quizzes | 200 XP |
| **Stock Scholar** | Complete all stock quizzes | 200 XP |
| **Know-It-All** | 90%+ average across all quizzes | 1000 XP |

#### 📈 Investment Badges (Trading)

| Badge | Criteria | XP Bonus |
|-------|----------|----------|
| **First Trade** | Execute first virtual trade | 50 XP |
| **Trader in Training** | Execute 10 trades | 100 XP |
| **Active Trader** | Execute 50 trades | 300 XP |
| **Diversifier** | Own 5 different stocks | 150 XP |
| **Sector Spreader** | Own stocks from 3 sectors | 200 XP |
| **Global Investor** | Own international stocks | 150 XP |
| **ETF Enthusiast** | Own 3 different ETFs | 200 XP |
| **Diamond Hands 💎** | Hold through 20% drop | 300 XP |
| **Paper Hands (shame!)** | Panic sell (learn from it!) | 0 XP |
| **Beat the Market** | Outperform DAX for 1 month | 500 XP |

#### 🔥 Consistency Badges (Streaks)

| Badge | Criteria | XP Bonus |
|-------|----------|----------|
| **Week Warrior** | 7-day streak | 75 XP |
| **Fortnight Fighter** | 14-day streak | 150 XP |
| **Month Master** | 30-day streak | 400 XP |
| **Quarter Champion** | 90-day streak | 1000 XP |
| **Year Legend** | 365-day streak | 5000 XP |

#### 💰 Savings Badges (Goals)

| Badge | Criteria | XP Bonus |
|-------|----------|----------|
| **First Goal** | Set first savings goal | 25 XP |
| **Goal Getter** | Achieve first savings goal | 100 XP |
| **Serial Saver** | Achieve 5 savings goals | 300 XP |
| **Dream Funded** | Save €1,000 toward a goal | 200 XP |
| **Money Mountain** | €5,000 total saved | 500 XP |

#### 🏆 Competition Badges (Social)

| Badge | Criteria | XP Bonus |
|-------|----------|----------|
| **Top 100** | Rank in weekly top 100 | 50 XP |
| **Top 10** | Rank in weekly top 10 | 200 XP |
| **Weekly Champion** | #1 for the week | 500 XP |
| **Class Leader** | #1 in school leaderboard | 300 XP |
| **School Pride** | Help school reach top 50 | 200 XP |
| **School Champion** | School wins monthly championship | 500 XP |

### Badge Display System

```
┌─────────────────────────────────────┐
│  🏆 My Badges (24/48)               │
│                                     │
│  ──── EQUIPPED (3 slots) ────       │
│  [💎 Diamond Hands]                 │
│  [🔥 Month Master]                  │
│  [📈 Beat the Market]               │
│                                     │
│  ──── EARNED ────                   │
│  🎓🎓🎓🎓🎓 Learning (5)            │
│  📈📈📈 Trading (3)                 │
│  🔥🔥🔥🔥 Streaks (4)               │
│  💰💰 Savings (2)                   │
│  🏆🏆🏆 Competition (3)             │
│                                     │
│  ──── LOCKED ────                   │
│  ⬜⬜⬜⬜ (24 more to unlock)        │
│                                     │
│  🎯 Next: "Quiz Master" (45/50)    │
│     [View all badges →]             │
└─────────────────────────────────────┘
```

---

## Leaderboards

### Leaderboard Types

#### 1. Weekly Leaderboard (Global)
- Resets every Sunday at midnight
- Shows XP earned that week only
- Top 10 winners announced Monday morning
- Prizes for top 3 (€25, €15, €10 bonus at age 18)

#### 2. All-Time Leaderboard (Global)
- Cumulative XP from account creation
- Shows rank and total XP
- Special flair for top 100 all-time

#### 3. School Leaderboard
- Aggregate XP from all students at school
- Requires 5+ students from same school
- Monthly school championships with prizes

#### 4. Friends Leaderboard
- Compare only with added friends
- Encourages friendly competition
- No prizes, just bragging rights

#### 5. Class Leaderboard (Kahoot-style)
- Real-time during live quiz sessions
- Teacher-created challenges
- Live updates after each question

### Leaderboard UI Specification

```
┌─────────────────────────────────────┐
│  🏆 Weekly Leaderboard              │
│  Resets in: 2d 14h 32m              │
│                                     │
│  ┌─────────────────────────────┐   │
│  │ 🥈    🥇    🥉               │   │
│  │ [2]  [1]   [3]               │   │
│  │ Max  Lisa  Tom               │   │
│  │ 2.2k 2.5k  2.1k              │   │
│  └─────────────────────────────┘   │
│                                     │
│  4. Sarah         1,980 XP    ▲2   │
│  5. Michael       1,875 XP    ▼1   │
│  6. Emma          1,820 XP    ▲5   │
│  7. Felix         1,790 XP    ─    │
│  8. Anna          1,755 XP    ▲3   │
│  ...                               │
│  ─────────────────────────────     │
│  42. You (MoneyLearner)            │
│      840 XP    ▲15                 │
│      Need 60 XP to pass Emma       │
│  ─────────────────────────────     │
│                                     │
│  🎁 This week's prize:             │
│  1st: €25  2nd: €15  3rd: €10     │
│  (credited at age 18)              │
└─────────────────────────────────────┘
```

---

## Kahoot-Style Challenges

### Overview

Leo can host live, multiplayer quiz sessions similar to Kahoot! These are designed for:
1. **Classroom use**: Teachers create sessions for students
2. **Friend challenges**: Users invite friends to compete
3. **School championships**: Monthly inter-class competitions
4. **Global events**: ING-sponsored special quizzes

### Creating a Challenge (Teacher/Host Flow)

```
Leo: "Ready to host a quiz challenge? 🎮"

Step 1: Select topic
[ ] ETFs & Funds
[ ] Stock Basics  
[ ] Taxes 101
[ ] Insurance Explained
[ ] Mixed Topics
[ ] Custom (create your own)

Step 2: Settings
• Number of questions: [5] [10] [15] [20]
• Time per question: [10s] [15s] [20s] [30s]
• Difficulty: [Easy] [Medium] [Hard] [Mixed]
• Points: [Standard] [Speed bonus] [Streak bonus]

Step 3: Share code
"Your game code: FINANZ-2847"
Share this code with participants!

[Start when ready] [Wait for more players]

Lobby shows:
"8 players joined (waiting for more...)"
👤 Max
👤 Lisa  
👤 Tom
👤 Sarah
...
```

### Playing a Challenge (Participant Flow)

```
Leo: "Join a quiz challenge! 🎮"

Enter game code: [FINANZ-2847]
                 [Join Game]

─────────────────────────────────

Waiting in lobby...
"Game: Stock Basics Quiz"
"Host: Frau Müller"
"Players: 24/30"

Your avatar: 🦁 MoneyLearner
Ready! Waiting for host to start...

─────────────────────────────────

[GAME STARTS]

Question 1/10                    ⏱️ 15s

"What does IPO stand for?"

┌─────────┐  ┌─────────┐
│    A    │  │    B    │
│ Initial │  │ Internal│
│ Public  │  │ Private │
│ Offering│  │ Option  │
└─────────┘  └─────────┘
┌─────────┐  ┌─────────┐
│    C    │  │    D    │
│ Instant │  │ Inter-  │
│ Profit  │  │ national│
│ Order   │  │ Purchase│
└─────────┘  └─────────┘

[Tap your answer!]

─────────────────────────────────

[AFTER ANSWER]

✅ Correct! +100 points (+20 speed bonus)

Current standings:
1. 🥇 Max      1,250
2. 🥈 Lisa     1,180  
3. 🥉 Tom      1,120
→ 4. You       1,100 (▲2)

─────────────────────────────────

[FINAL RESULTS]

🏆 Game Over! 🏆

Final Standings:
🥇 Lisa       2,450 (+250 XP)
🥈 Max        2,380 (+150 XP)
🥉 You        2,290 (+100 XP)

Your stats:
• 8/10 correct answers
• Best streak: 5 in a row
• Fastest answer: Q3 (2.1s)
• +100 XP earned

[Play Again] [Back to Home]
```

### Real-Time Scoring Mechanics

| Factor | Points |
|--------|--------|
| Correct answer | 100 base |
| Speed bonus (0-20 points) | Faster = more |
| Streak bonus (2+ correct in a row) | +10 per question in streak |
| Perfect game bonus | +100 |
| First to answer correctly | +25 |

### Sound & Visual Effects

- **Question appears**: Dramatic reveal animation, countdown sound
- **Answer submitted**: Lock-in sound, button highlights
- **Correct answer**: Confetti, success sound, green flash
- **Wrong answer**: Gentle buzz, red flash, "Next time!" message
- **Leaderboard update**: Swoosh sound, animated position changes
- **Final results**: Victory fanfare for winner, celebration for all

---

## School Championships

### Monthly Championship Structure

**Week 1-3**: Qualification Phase
- Students earn XP through regular activities
- School's total XP aggregated
- Top 50 schools qualify for finals

**Week 4**: Championship Week
- Special championship quizzes unlocked
- 3x XP multiplier on all activities
- Live inter-school challenge on Friday

**Prizes**:
- 1st place school: €1,000 to school's financial literacy program
- 2nd place: €500
- 3rd place: €250
- Top 10: Recognition on ING website
- All participants: Digital certificate

### School Registration Flow

```
Teacher/Admin Portal:

1. Register school
   School name: [Gymnasium Musterstadt]
   School code: Will be generated
   Admin email: [teacher@school.de]

2. Students join
   Students enter school code in app
   OR teacher sends invite link

3. Class management
   Create class groups
   Track class progress
   Set up class challenges

4. Parent consent
   Automatic consent flow for parents
   Required for competition participation
```

---

## User Stories for Demo Sidebar

### Story 1: Daily Challenge Completion
```yaml
ID: gamification_daily_challenge
Name: "Daily Challenge"
Description: "Complete today's Leo challenge"
Category: junior
Duration: ~1 minute

Flow:
1. Leo notification: "Your daily challenge is ready! 🎯"
2. User opens app to see challenge card
3. Challenge: "Answer 3 questions about ETFs"
4. User completes quick quiz (3 questions)
5. Leo: "Awesome! +75 XP and 🔥 streak extended!"
6. Show updated XP bar and streak counter
7. Tease tomorrow's challenge

Demo Messages:
- Leo: "Here's your daily challenge! 3 ETF questions - ready?"
- User: "Let's do it!"
- Leo: [Quiz Widget with 3 questions]
- [After completion]
- Leo: "🎉 Perfect! +75 XP earned. You're on fire with a 7-day streak!"
- Leo: [Achievement Widget: "Week Warrior" badge unlocked]
```

### Story 2: Leaderboard Climb
```yaml
ID: gamification_leaderboard_climb
Name: "Leaderboard Climb"
Description: "See your weekly ranking and compete"
Category: junior
Duration: ~45 seconds

Flow:
1. User opens leaderboard
2. See current position (#42)
3. Leo: "You're 60 XP away from passing Emma!"
4. Quick quiz suggestion to earn points
5. Complete quiz, watch rank animate up

Demo Messages:
- Leo: "Let's check the leaderboard! You're doing great this week."
- [Show leaderboard with user at #42]
- Leo: "Emma is just 60 XP ahead. One quiz could change that!"
- User: "Show me a quick quiz"
- Leo: [Quiz Widget: 5 questions]
- [After quiz - earned 85 XP]
- Leo: "BOOM! 💥 You passed Emma AND Felix! New rank: #40"
- [Animated leaderboard showing climb]
```

### Story 3: Achievement Unlock
```yaml
ID: gamification_achievement_unlock
Name: "Badge Unlocked!"
Description: "Unlock a new achievement badge"
Category: junior
Duration: ~30 seconds

Flow:
1. User completes 10th quiz
2. Screen flash, celebration animation
3. Leo: "NEW BADGE UNLOCKED! 🏆"
4. Badge reveal animation
5. Show badge added to collection
6. Hint at next badge to earn

Demo Messages:
- [After quiz completion]
- Leo: "Wait... is that your 10th quiz? 👀"
- [Dramatic pause]
- Leo: "🎉 NEW BADGE UNLOCKED!"
- [Achievement Widget: "Quiz Regular" with celebration animation]
- Leo: "Add it to your profile! You're 40 quizzes away from 'Quiz Master'"
```

### Story 4: Kahoot-Style Class Challenge
```yaml
ID: gamification_class_kahoot
Name: "Class Quiz Challenge"
Description: "Join a live classroom quiz competition"
Category: junior
Duration: ~3 minutes

Flow:
1. User enters game code from teacher
2. Join lobby, see classmates
3. Host starts game
4. 10 rapid-fire questions
5. Live leaderboard between questions
6. Final results and XP awards

Demo Messages:
- Leo: "Ready for the class challenge? Enter the code your teacher shared!"
- User: "FINANZ-2847"
- Leo: "Joining 'Frau Müller's Stock Quiz'... 18 players in lobby"
- [Lobby animation showing players joining]
- Leo: "Game starting in 3... 2... 1... GO!"
- [Simulated Kahoot-style quiz with 5 questions]
- [After each question: leaderboard update]
- Leo: "FINAL RESULTS: You came in 3rd! 🥉 +100 XP"
- Leo: "Great job! Your class average was 72% - better than yesterday!"
```

### Story 5: School Championship Entry
```yaml
ID: gamification_school_championship
Name: "School Championship"
Description: "Compete for your school in the monthly championship"
Category: junior
Duration: ~2 minutes

Flow:
1. Leo announces championship week
2. Show school's current rank
3. Special championship quiz available
4. Complete quiz with 3x XP multiplier
5. Watch school rank improve
6. Team celebration moment

Demo Messages:
- Leo: "🏆 CHAMPIONSHIP WEEK IS HERE!"
- Leo: "Your school (Gymnasium Musterstadt) is ranked #23. Can you help climb higher?"
- Leo: "Championship quizzes earn 3x XP this week!"
- [Show special Championship Quiz Widget]
- User: "Let's do this!"
- [Quiz with 10 harder questions]
- Leo: "Incredible! +450 XP (with 3x bonus)"
- Leo: "Your school jumped to #21! 2 spots closer to the top 20!"
- [Animation showing school climbing leaderboard]
```

### Story 6: Weekly Winner Announcement
```yaml
ID: gamification_weekly_winner
Name: "Weekly Winner"
Description: "See who won this week's competition"
Category: junior
Duration: ~1 minute

Flow:
1. Monday morning notification
2. Leo reveals weekly winners
3. Show prizes awarded
4. New week starts
5. Encourage user to compete

Demo Messages:
- Leo: "📣 Last week's results are in!"
- Leo: "🥇 Lisa (2,450 XP) - €25 bonus"
- Leo: "🥈 Max (2,380 XP) - €15 bonus"  
- Leo: "🥉 Tom (2,290 XP) - €10 bonus"
- Leo: "You finished #42 with 840 XP - your best week yet!"
- Leo: "New week, fresh start! First quiz of the week earns 2x XP 🎁"
- User: "Let's aim for top 10 this week!"
- Leo: "That's the spirit! Here's your first quiz..."
```

### Story 7: Streak Save Reminder
```yaml
ID: gamification_streak_reminder
Name: "Save Your Streak!"
Description: "Urgent reminder to maintain streak"
Category: junior
Duration: ~30 seconds

Flow:
1. Evening notification (streak about to expire)
2. Leo shows streak status
3. Quick action to save streak
4. Streak extended celebration

Demo Messages:
- Leo: "⚠️ Your 12-day streak expires in 2 hours!"
- Leo: "Just one quick question to keep it alive?"
- User: "Yes, quick!"
- Leo: [Single quiz question]
- [User answers correctly]
- Leo: "🔥 STREAK SAVED! Day 13 begins tomorrow!"
- Leo: "Fun fact: You're in the top 5% of streak holders!"
```

---

## Technical Implementation Notes

### Points & XP Storage

```typescript
interface UserGamification {
  userId: string;
  level: number;
  totalXP: number;
  weeklyXP: number;
  currentStreak: number;
  longestStreak: number;
  badges: Badge[];
  equippedBadges: string[]; // max 3
  achievements: Achievement[];
  quizHistory: QuizResult[];
  schoolCode?: string;
  lastActivityDate: Date;
}
```

### Leaderboard Query

```sql
-- Weekly leaderboard
SELECT 
  user_id,
  username,
  weekly_xp,
  RANK() OVER (ORDER BY weekly_xp DESC) as rank
FROM user_gamification
WHERE week_start = CURRENT_WEEK()
ORDER BY weekly_xp DESC
LIMIT 100;
```

### Real-Time Kahoot Events

```typescript
// WebSocket events for live quiz
socket.on('game:join', { gameCode, userId });
socket.on('game:start', { questions });
socket.on('answer:submit', { questionId, answer, timestamp });
socket.on('leaderboard:update', { standings });
socket.on('game:end', { finalResults });
```

---

*Last Updated: November 2025*
