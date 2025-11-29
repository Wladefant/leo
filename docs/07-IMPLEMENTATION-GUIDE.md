# Implementation Guide for ING-App

> This document provides specific implementation suggestions for the [ing-app repository](https://github.com/Wladefant/ing-app) based on the LEO specifications.

---

## Table of Contents
1. [Current Implementation Status](#current-implementation-status)
2. [High Priority Changes](#high-priority-changes)
3. [File-by-File Suggestions](#file-by-file-suggestions)
4. [New Files to Create](#new-files-to-create)
5. [Demo Sidebar User Stories](#demo-sidebar-user-stories)

---

## Current Implementation Status

Based on analysis of the ing-app codebase:

### ✅ Working Features
- Bottom navigation
- Profile switching (Adult/Junior)
- Leo chat overlay with basic AI
- Quiz widget display
- Stock detail view
- Demo scenario triggering
- Basic dashboard views

### ⚠️ Partial Features
- Quiz system (static questions only)
- Gamification display (no real XP tracking)
- Stock widgets (visual only)
- Transfer flow (incomplete)

### ❌ Missing Features
- AI-generated quiz questions
- Real XP/points system
- Kahoot-style multiplayer
- Smart notifications
- Document scanning
- Voice mode
- Parent dashboard

---

## High Priority Changes

### 1. Quiz System Overhaul

**Current Problem**: Quiz uses hardcoded static questions in `junior/quiz.tsx`

**Solution**: Create AI-generated quiz service

**File to create**: `client/src/lib/quiz-generator.ts`

```typescript
import OpenAI from 'openai';

interface QuizQuestion {
  question: string;
  options: string[];
  correctAnswer: number;
  explanation: string;
  difficulty: 'easy' | 'medium' | 'hard';
}

interface GeneratedQuiz {
  topic: string;
  questions: QuizQuestion[];
  estimatedXP: number;
}

const QUIZ_PROMPT = `
Du bist Leo, ein freundlicher Finanz-Assistent für junge Menschen.
Erstelle ein Quiz zum Thema: {topic}

Anforderungen:
- {count} Fragen
- Schwierigkeit: {difficulty}
- Sprache: Einfaches Deutsch, keine Fachbegriffe
- Jede Frage hat 4 Antwortmöglichkeiten
- Erkläre nach jeder Antwort warum sie richtig/falsch ist

Antworte im JSON-Format:
{
  "questions": [
    {
      "question": "...",
      "options": ["A", "B", "C", "D"],
      "correctAnswer": 0,
      "explanation": "..."
    }
  ]
}
`;

export async function generateQuiz(
  topic: string,
  difficulty: 'easy' | 'medium' | 'hard' = 'medium',
  count: number = 5
): Promise<GeneratedQuiz> {
  const openai = new OpenAI({
    apiKey: process.env.OPENAI_API_KEY
  });

  const prompt = QUIZ_PROMPT
    .replace('{topic}', topic)
    .replace('{count}', count.toString())
    .replace('{difficulty}', difficulty);

  const response = await openai.chat.completions.create({
    model: 'gpt-4',
    messages: [{ role: 'user', content: prompt }],
    temperature: 0.7,
  });

  const content = response.choices[0].message.content;
  const parsed = JSON.parse(content || '{}');
  
  const xpMap = { easy: 10, medium: 15, hard: 25 };
  const estimatedXP = count * xpMap[difficulty];

  return {
    topic,
    questions: parsed.questions,
    estimatedXP
  };
}

// Context-aware quiz generation
export async function generateContextualQuiz(
  context: {
    currentScreen: string;
    recentActions: string[];
    userLevel: number;
    weakTopics: string[];
  }
): Promise<GeneratedQuiz> {
  // Generate quiz based on what user is currently doing
  let topic = 'Allgemeine Finanzen';
  
  if (context.currentScreen.includes('stock')) {
    topic = 'Aktien Grundlagen';
  } else if (context.currentScreen.includes('etf')) {
    topic = 'ETFs verstehen';
  } else if (context.weakTopics.length > 0) {
    topic = context.weakTopics[0]; // Focus on weak areas
  }
  
  const difficulty = context.userLevel < 3 ? 'easy' : 
                     context.userLevel < 7 ? 'medium' : 'hard';
  
  return generateQuiz(topic, difficulty);
}
```

### 2. Add Points/XP System

**File to create**: `client/src/lib/gamification.ts`

```typescript
interface UserProgress {
  totalXP: number;
  weeklyXP: number;
  level: number;
  streak: number;
  badges: string[];
  quizHistory: QuizResult[];
}

interface QuizResult {
  topic: string;
  score: number;
  total: number;
  xpEarned: number;
  timestamp: Date;
}

// Level thresholds
const LEVELS = [
  { level: 1, xp: 0, title: 'Finanz-Anfänger' },
  { level: 2, xp: 500, title: 'Geld-Lerner' },
  { level: 3, xp: 1200, title: 'Spar-Fuchs' },
  { level: 4, xp: 2500, title: 'Budget-Held' },
  { level: 5, xp: 5000, title: 'Finanz-Entdecker' },
  // ...etc
];

export function calculateLevel(xp: number): { level: number; title: string; progress: number } {
  let currentLevel = LEVELS[0];
  let nextLevel = LEVELS[1];
  
  for (let i = LEVELS.length - 1; i >= 0; i--) {
    if (xp >= LEVELS[i].xp) {
      currentLevel = LEVELS[i];
      nextLevel = LEVELS[i + 1] || LEVELS[i];
      break;
    }
  }
  
  const progress = nextLevel.xp === currentLevel.xp ? 100 :
    ((xp - currentLevel.xp) / (nextLevel.xp - currentLevel.xp)) * 100;
  
  return {
    level: currentLevel.level,
    title: currentLevel.title,
    progress
  };
}

export function calculateQuizXP(
  correctAnswers: number,
  totalQuestions: number,
  difficulty: string,
  streakMultiplier: number
): number {
  const baseXP = { easy: 10, medium: 15, hard: 25 }[difficulty] || 15;
  const xp = correctAnswers * baseXP;
  
  // Perfect score bonus
  const perfectBonus = correctAnswers === totalQuestions ? 50 : 0;
  
  // Streak multiplier
  const finalXP = Math.floor((xp + perfectBonus) * streakMultiplier);
  
  return finalXP;
}

// Store in localStorage for now (should be backend in production)
export function getUserProgress(): UserProgress {
  const stored = localStorage.getItem('leo_user_progress');
  if (stored) return JSON.parse(stored);
  
  return {
    totalXP: 0,
    weeklyXP: 0,
    level: 1,
    streak: 0,
    badges: [],
    quizHistory: []
  };
}

export function saveUserProgress(progress: UserProgress): void {
  localStorage.setItem('leo_user_progress', JSON.stringify(progress));
}

export function addXP(amount: number, source: string): UserProgress {
  const progress = getUserProgress();
  progress.totalXP += amount;
  progress.weeklyXP += amount;
  
  const levelInfo = calculateLevel(progress.totalXP);
  progress.level = levelInfo.level;
  
  saveUserProgress(progress);
  return progress;
}
```

### 3. Connect Quiz Widget to Actual Quiz

**File to modify**: `client/src/components/ing/leo/chat-overlay.tsx`

**Current issue**: QuizWidget has a non-functional "Quiz starten" button

**Change**:

```typescript
// In chat-overlay.tsx, find the QuizWidget render section

// Before:
function QuizWidget({ topic, questions, xp, difficulty, onStart }: { ... }) {
  return (
    <div>
      ...
      <button onClick={onStart}>Quiz starten</button>
    </div>
  );
}

// After - connect to state and start real quiz:
function QuizWidget({ topic, questions, xp, difficulty, onStart }: { ... }) {
  const handleStartQuiz = async () => {
    if (onStart) {
      // If we have an AI-generated quiz ready, use it
      onStart();
    } else {
      // Generate new quiz on demand
      try {
        const quiz = await generateQuiz(topic, difficulty);
        // Trigger quiz state
        setQuizState({
          isActive: true,
          topic,
          difficulty,
          questions: quiz.questions,
          currentQuestion: 0,
          score: 0,
          answered: false,
          selectedAnswer: null,
          showExplanation: false,
          completed: false
        });
      } catch (error) {
        console.error('Failed to generate quiz:', error);
      }
    }
  };
  
  return (
    <div>
      ...
      <button onClick={handleStartQuiz}>Quiz starten</button>
    </div>
  );
}
```

### 4. Fix Non-Functional Buttons

**File to modify**: `client/src/pages/ing-app.tsx`

Add navigation handlers for missing buttons:

```typescript
// Add these handlers to the main ing-app component

const handleNavigate = (screen: string, params?: any) => {
  switch (screen) {
    case 'stock-search':
      setCurrentScreen('invest');
      // Open search modal: Show a modal with search input field,
      // display matching stocks as user types, allow selecting a stock
      // to navigate to its detail view
      setShowSearchModal(true);
      break;
    case 'savings-goals':
      setCurrentScreen('junior-savings');
      break;
    case 'achievements':
      setCurrentScreen('achievements'); // Create this screen
      break;
    case 'buy-stock':
      setCurrentScreen('stock-detail');
      setSelectedStock(params?.symbol);
      // Open buy modal: Display stock price, quantity input (shares or euros),
      // calculate total cost, show portfolio impact, confirm with Leo explanation
      // For Junior: virtual purchase with V€ currency
      // For Adult: real purchase flow with confirmation
      setShowBuyModal(true);
      break;
    // ... etc
  }
};

// Pass this to child components
<JuniorDashboard 
  onNavigate={handleNavigate}
  userProgress={userProgress}
/>
```

---

## File-by-File Suggestions

### `client/src/components/ing/screens/junior/dashboard.tsx`

**Changes needed**:

1. **"Sparen" button** - Currently does nothing
```typescript
// Find the Sparen button and add:
<button onClick={() => onNavigate('savings-goals')}>
  Sparen
</button>
```

2. **Display real XP/Level** - Currently hardcoded
```typescript
// Replace hardcoded values with:
const { level, title, totalXP } = getUserProgress();

// In render:
<div>Level {level}</div>
<div>{title}</div>
<div>{totalXP} XP</div>
```

3. **Daily challenge should trigger real quiz**
```typescript
// Change challenge button to:
<button onClick={() => {
  setShowLeoChat(true);
  triggerScenario('quiz_trigger');
}}>
  Quiz starten
</button>
```

---

### `client/src/components/ing/screens/junior/quiz.tsx`

**Complete rewrite needed**:

```typescript
// client/src/components/ing/screens/junior/quiz.tsx
import { useState, useEffect } from 'react';
import { generateQuiz, GeneratedQuiz } from '@/lib/quiz-generator';
import { addXP, calculateQuizXP, getUserProgress } from '@/lib/gamification';

interface EnhancedQuizProps {
  topic?: string;
  difficulty?: 'easy' | 'medium' | 'hard';
  onComplete: (result: QuizResult) => void;
  onBack: () => void;
}

export function EnhancedQuiz({ topic, difficulty, onComplete, onBack }: EnhancedQuizProps) {
  const [quiz, setQuiz] = useState<GeneratedQuiz | null>(null);
  const [loading, setLoading] = useState(true);
  const [currentQuestion, setCurrentQuestion] = useState(0);
  const [selectedAnswer, setSelectedAnswer] = useState<number | null>(null);
  const [showExplanation, setShowExplanation] = useState(false);
  const [score, setScore] = useState(0);
  const [completed, setCompleted] = useState(false);
  
  useEffect(() => {
    async function loadQuiz() {
      setLoading(true);
      try {
        const generated = await generateQuiz(
          topic || 'Allgemeine Finanzen',
          difficulty || 'medium',
          5
        );
        setQuiz(generated);
      } catch (error) {
        console.error('Quiz generation failed:', error);
        // Fall back to static questions
      } finally {
        setLoading(false);
      }
    }
    loadQuiz();
  }, [topic, difficulty]);
  
  const handleAnswer = (answerIndex: number) => {
    if (showExplanation) return;
    
    setSelectedAnswer(answerIndex);
    setShowExplanation(true);
    
    const question = quiz?.questions[currentQuestion];
    if (answerIndex === question?.correctAnswer) {
      setScore(score + 1);
    }
  };
  
  const handleNext = () => {
    if (currentQuestion < (quiz?.questions.length || 0) - 1) {
      setCurrentQuestion(currentQuestion + 1);
      setSelectedAnswer(null);
      setShowExplanation(false);
    } else {
      // Quiz completed
      const userProgress = getUserProgress();
      const xpEarned = calculateQuizXP(
        score,
        quiz?.questions.length || 0,
        difficulty || 'medium',
        userProgress.streak > 7 ? 1.5 : 1
      );
      
      addXP(xpEarned, 'quiz');
      setCompleted(true);
      
      onComplete({
        topic: topic || 'Allgemein',
        score,
        total: quiz?.questions.length || 0,
        xpEarned,
        timestamp: new Date()
      });
    }
  };
  
  if (loading) {
    return <QuizLoadingSkeleton />;
  }
  
  if (completed) {
    return <QuizResults score={score} total={quiz?.questions.length} onBack={onBack} />;
  }
  
  return (
    <QuizQuestion
      question={quiz?.questions[currentQuestion]}
      questionNumber={currentQuestion + 1}
      totalQuestions={quiz?.questions.length || 0}
      selectedAnswer={selectedAnswer}
      showExplanation={showExplanation}
      onAnswer={handleAnswer}
      onNext={handleNext}
    />
  );
}
```

---

### `client/src/components/ing/leo/demo-sidebar.tsx`

**Add more user stories**:

```typescript
// In demo-scenarios.ts, add these scenarios:

export const DEMO_SCENARIOS: Record<DemoScenarioId, DemoScenario> = {
  // ... existing scenarios ...
  
  // NEW: Daily Challenge
  daily_challenge: {
    id: 'daily_challenge',
    name: 'Tägliche Challenge',
    description: 'Tägliches Quiz mit Leo',
    category: 'junior',
    messages: [
      {
        id: 'dc1',
        sender: 'leo',
        text: '🎯 Deine tägliche Challenge ist da! Heute: ETF Grundlagen',
        timestamp: new Date(),
        widgetType: 'quiz',
        widgetData: {
          topic: 'ETFs verstehen',
          questions: 3,
          xp: 75,
          difficulty: 'mittel'
        }
      }
    ]
  },
  
  // NEW: Leaderboard Update
  leaderboard_climb: {
    id: 'leaderboard_climb',
    name: 'Leaderboard Aufstieg',
    description: 'Sieh deinen Rang steigen',
    category: 'junior',
    messages: [
      {
        id: 'lb1',
        sender: 'leo',
        text: '🏆 Leaderboard Update! Du bist auf Platz #42. Emma ist nur 60 XP vor dir!',
        timestamp: new Date()
      },
      {
        id: 'lb2',
        sender: 'leo',
        text: 'Ein Quiz könnte reichen um sie zu überholen. Bereit?',
        timestamp: new Date(),
        widgetType: 'quiz',
        widgetData: {
          topic: 'Schnellquiz',
          questions: 5,
          xp: 100,
          difficulty: 'mittel'
        }
      }
    ]
  },
  
  // NEW: Achievement Unlock
  achievement_unlock: {
    id: 'achievement_unlock',
    name: 'Badge freigeschaltet!',
    description: 'Feiere einen neuen Badge',
    category: 'junior',
    messages: [
      {
        id: 'au1',
        sender: 'leo',
        text: '🎉 NEUER BADGE FREIGESCHALTET!',
        timestamp: new Date(),
        widgetType: 'achievement',
        widgetData: {
          name: 'Quiz Regular',
          xp: 100,
          description: 'Du hast 10 Quizzes abgeschlossen!'
        }
      }
    ]
  },
  
  // NEW: Streak Reminder
  streak_reminder: {
    id: 'streak_reminder',
    name: 'Streak Erinnerung',
    description: 'Rette deinen Streak!',
    category: 'junior',
    messages: [
      {
        id: 'sr1',
        sender: 'leo',
        text: '⚠️ Dein 12-Tage-Streak läuft in 2 Stunden ab! Eine Frage reicht zum Retten.',
        timestamp: new Date()
      },
      {
        id: 'sr2',
        sender: 'leo',
        text: 'Quick: Was ist ein ETF?',
        timestamp: new Date(),
        widgetType: 'quiz_question',
        widgetData: {
          question: 'Was ist ein ETF?',
          options: ['Exchange Traded Fund', 'European Tax Form', 'Extra Trading Fee', 'End-Term Financing'],
          correctAnswer: 0
        }
      }
    ]
  },
  
  // NEW: News Alert
  portfolio_news: {
    id: 'portfolio_news',
    name: 'Portfolio News',
    description: 'Wichtige Neuigkeiten zu deinen Aktien',
    category: 'both',
    messages: [
      {
        id: 'pn1',
        sender: 'leo',
        text: '📰 Wichtige News zu Apple!',
        timestamp: new Date()
      },
      {
        id: 'pn2',
        sender: 'leo',
        text: 'Apple hat Rekordzahlen gemeldet. Deine 5 Aktien sind +€23.50 wert!\n\nDas iPhone 15 verkauft sich super, und Services wachsen weiter.',
        timestamp: new Date(),
        widgetType: 'stock',
        widgetData: {
          symbol: 'AAPL',
          price: 178.50,
          change: 2.3,
          analysis: 'Starke Q4-Zahlen treiben den Kurs'
        }
      }
    ]
  },
  
  // NEW: Savings Goal Progress
  savings_milestone: {
    id: 'savings_milestone',
    name: 'Sparziel Fortschritt',
    description: 'Update zu deinem Sparziel',
    category: 'both',
    messages: [
      {
        id: 'sm1',
        sender: 'leo',
        text: '🎯 Sparziel Update!',
        timestamp: new Date(),
        widgetType: 'savings_goal',
        widgetData: {
          goalName: 'Urlaub 2026',
          targetAmount: 2000,
          currentAmount: 850,
          weeksRemaining: 28
        }
      },
      {
        id: 'sm2',
        sender: 'leo',
        text: 'Du bist auf gutem Weg! Mit €50 mehr pro Monat erreichst du dein Ziel noch früher.',
        timestamp: new Date()
      }
    ]
  }
};
```

---

## New Files to Create

### 1. `client/src/components/ing/screens/achievements.tsx`

Achievement gallery screen to display all badges:

```typescript
import { motion } from 'framer-motion';
import { Trophy, Lock } from 'lucide-react';
import { ScreenHeader } from '../layout';
import { getUserProgress } from '@/lib/gamification';

const ALL_BADGES = [
  { id: 'quiz_newbie', name: 'Quiz Newbie', icon: '🎓', description: 'Erstes Quiz abgeschlossen' },
  { id: 'quiz_regular', name: 'Quiz Regular', icon: '📚', description: '10 Quizzes abgeschlossen' },
  { id: 'quiz_master', name: 'Quiz Master', icon: '🧠', description: '50 Quizzes abgeschlossen' },
  { id: 'first_trade', name: 'First Trade', icon: '📈', description: 'Erster virtueller Trade' },
  { id: 'diamond_hands', name: 'Diamond Hands', icon: '💎', description: 'Durch 20% Rückgang gehalten' },
  { id: 'week_warrior', name: 'Week Warrior', icon: '🔥', description: '7-Tage Streak' },
  { id: 'month_master', name: 'Month Master', icon: '🔥🔥', description: '30-Tage Streak' },
  { id: 'diversifier', name: 'Diversifier', icon: '🎯', description: '5 verschiedene Aktien' },
  // ... more badges
];

export function AchievementsScreen({ onBack }: { onBack: () => void }) {
  const { badges } = getUserProgress();
  
  const earnedBadges = ALL_BADGES.filter(b => badges.includes(b.id));
  const lockedBadges = ALL_BADGES.filter(b => !badges.includes(b.id));
  
  return (
    <div className="bg-gray-50 min-h-full">
      <ScreenHeader title="Achievements" onBack={onBack} />
      
      <div className="p-4 space-y-6">
        {/* Progress Overview */}
        <div className="bg-white rounded-xl p-4 shadow-sm">
          <div className="flex items-center gap-3">
            <Trophy className="text-yellow-500" size={32} />
            <div>
              <div className="text-2xl font-bold">{earnedBadges.length}/{ALL_BADGES.length}</div>
              <div className="text-gray-500">Badges verdient</div>
            </div>
          </div>
        </div>
        
        {/* Earned Badges */}
        <div>
          <h2 className="text-lg font-bold mb-3">Verdient ({earnedBadges.length})</h2>
          <div className="grid grid-cols-4 gap-3">
            {earnedBadges.map(badge => (
              <motion.div
                key={badge.id}
                whileHover={{ scale: 1.05 }}
                className="bg-gradient-to-br from-yellow-100 to-orange-100 rounded-xl p-3 text-center"
              >
                <div className="text-3xl mb-1">{badge.icon}</div>
                <div className="text-xs font-medium">{badge.name}</div>
              </motion.div>
            ))}
          </div>
        </div>
        
        {/* Locked Badges */}
        <div>
          <h2 className="text-lg font-bold mb-3">Noch freischalten ({lockedBadges.length})</h2>
          <div className="grid grid-cols-4 gap-3">
            {lockedBadges.map(badge => (
              <div
                key={badge.id}
                className="bg-gray-100 rounded-xl p-3 text-center opacity-50"
              >
                <Lock className="mx-auto mb-1 text-gray-400" size={24} />
                <div className="text-xs text-gray-400">{badge.name}</div>
              </div>
            ))}
          </div>
        </div>
      </div>
    </div>
  );
}
```

### 2. `client/src/components/ing/screens/junior/savings.tsx`

Savings goals screen:

```typescript
import { useState } from 'react';
import { motion } from 'framer-motion';
import { Target, Plus, Edit } from 'lucide-react';
import { ScreenHeader } from '../../layout';

interface SavingsGoal {
  id: string;
  name: string;
  targetAmount: number;
  currentAmount: number;
  deadline?: Date;
  icon: string;
}

const MOCK_GOALS: SavingsGoal[] = [
  { id: '1', name: 'Urlaub 2026', targetAmount: 2000, currentAmount: 850, icon: '🏖️' },
  { id: '2', name: 'Neues Handy', targetAmount: 800, currentAmount: 240, icon: '📱' },
  { id: '3', name: 'Führerschein', targetAmount: 2500, currentAmount: 500, icon: '🚗' },
];

export function JuniorSavingsScreen({ onBack }: { onBack: () => void }) {
  const [goals, setGoals] = useState(MOCK_GOALS);
  
  return (
    <div className="bg-gray-50 min-h-full">
      <ScreenHeader 
        title="Sparziele" 
        onBack={onBack}
        rightContent={
          <button className="p-2 rounded-full bg-orange-100 text-orange-600">
            <Plus size={20} />
          </button>
        }
      />
      
      <div className="p-4 space-y-4">
        {goals.map(goal => {
          const progress = (goal.currentAmount / goal.targetAmount) * 100;
          
          return (
            <motion.div
              key={goal.id}
              initial={{ opacity: 0, y: 20 }}
              animate={{ opacity: 1, y: 0 }}
              className="bg-white rounded-xl p-4 shadow-sm"
            >
              <div className="flex items-center gap-3 mb-3">
                <div className="text-3xl">{goal.icon}</div>
                <div className="flex-1">
                  <div className="font-bold">{goal.name}</div>
                  <div className="text-sm text-gray-500">
                    €{goal.currentAmount} / €{goal.targetAmount}
                  </div>
                </div>
                <button className="p-2 text-gray-400 hover:text-orange-600">
                  <Edit size={18} />
                </button>
              </div>
              
              <div className="h-3 bg-gray-100 rounded-full overflow-hidden">
                <motion.div
                  initial={{ width: 0 }}
                  animate={{ width: `${progress}%` }}
                  className="h-full bg-gradient-to-r from-orange-400 to-orange-600 rounded-full"
                />
              </div>
              
              <div className="flex justify-between text-sm mt-2">
                <span className="text-gray-500">{progress.toFixed(0)}% erreicht</span>
                <span className="text-orange-600 font-medium">
                  Noch €{goal.targetAmount - goal.currentAmount}
                </span>
              </div>
            </motion.div>
          );
        })}
        
        {/* Leo Tip */}
        <div className="bg-blue-50 rounded-xl p-4 border border-blue-100">
          <div className="flex gap-2 items-start">
            <span className="text-xl">💡</span>
            <div>
              <div className="font-medium text-blue-800">Leo's Tipp</div>
              <div className="text-sm text-blue-700">
                Mit €50/Monat erreichst du dein Urlaubs-Ziel noch vor August!
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  );
}
```

---

## Demo Sidebar User Stories

Here are complete user story configurations to add to demo-scenarios.ts:

```typescript
// Add to DEMO_SCENARIOS in client/src/lib/demo-scenarios.ts

// STORY 1: Complete Quiz Journey (Junior)
complete_quiz_journey: {
  id: 'complete_quiz_journey',
  name: '📚 Quiz Komplettablauf',
  description: 'Vollständiger Quiz von Start bis XP',
  category: 'junior',
  messages: [
    { id: 'cqj1', sender: 'leo', text: 'Zeit für dein tägliches Quiz! 🎯', timestamp: new Date() },
    { id: 'cqj2', sender: 'leo', text: 'Heute: ETF Grundlagen - 5 Fragen', timestamp: new Date(), widgetType: 'quiz', widgetData: { topic: 'ETFs', questions: 5, xp: 100, difficulty: 'mittel' } },
    { id: 'cqj3', sender: 'user', text: 'Quiz starten!', timestamp: new Date() },
    { id: 'cqj4', sender: 'leo', text: 'Frage 1: Was bedeutet ETF?\n\nA) Exchange Traded Fund\nB) European Tax Form\nC) Extra Trading Fee\nD) End-Term Financing', timestamp: new Date() },
    { id: 'cqj5', sender: 'user', text: 'A', timestamp: new Date() },
    { id: 'cqj6', sender: 'leo', text: '✅ Richtig! +20 XP\n\nETF steht für Exchange Traded Fund - ein börsengehandelter Fonds.', timestamp: new Date() },
    // ... continue with more questions ...
    { id: 'cqj_final', sender: 'leo', text: '🎉 Quiz abgeschlossen!\n\n5/5 richtig\n+100 XP (+50 Bonus für Perfektion!)\n\nDu bist jetzt auf Level 6!', timestamp: new Date(), widgetType: 'achievement', widgetData: { name: 'Perfect Score', xp: 150, description: 'Alle Fragen richtig!' } }
  ]
},

// STORY 2: First Investment (Junior)
first_virtual_investment: {
  id: 'first_virtual_investment',
  name: '📈 Erster Trade',
  description: 'Junior kauft erste virtuelle Aktie',
  category: 'junior',
  messages: [
    { id: 'fvi1', sender: 'user', text: 'Ich will Apple kaufen!', timestamp: new Date() },
    { id: 'fvi2', sender: 'leo', text: 'Super Wahl für den Anfang! 🍎\n\nApple ist ein Tech-Gigant, der iPhones, Macs und mehr herstellt.', timestamp: new Date(), widgetType: 'stock', widgetData: { symbol: 'AAPL', price: 178.50, change: 1.5 } },
    { id: 'fvi3', sender: 'leo', text: 'Bevor du kaufst - lass mich erklären:\n\n• Aktien können steigen ODER fallen\n• Apple ist relativ stabil (Blue Chip)\n• Du hast V€2,450 virtuelles Geld\n\nWie viel möchtest du investieren?', timestamp: new Date() },
    { id: 'fvi4', sender: 'user', text: '500 Euro', timestamp: new Date() },
    { id: 'fvi5', sender: 'leo', text: 'V€500 = ca. 2.8 Apple Aktien (aufgerundet auf 3)\n\nDas wäre 20% deines Portfolios. Gute Startgröße!\n\n⚠️ Zur Erinnerung: Das ist virtuelles Geld zum Lernen.', timestamp: new Date() },
    { id: 'fvi6', sender: 'leo', text: '✅ Trade ausgeführt!\n\n3x Apple (AAPL)\nKaufpreis: €178.50\nGesamt: V€535.50\n\n+100 XP für deinen ersten Trade! 🎉', timestamp: new Date(), widgetType: 'achievement', widgetData: { name: 'First Trade', xp: 100, description: 'Dein erster virtueller Aktienkauf!' } }
  ]
},

// STORY 3: Smart Transfer (Adult)
smart_transfer_complete: {
  id: 'smart_transfer_complete',
  name: '💸 Smart Transfer',
  description: 'KI-unterstützte Überweisung',
  category: 'adult',
  messages: [
    { id: 'stc1', sender: 'leo', text: '🏠 Erinnerung: Heute ist der 1.!\n\nMiete ist fällig. Soll ich €800 an deinen Vermieter senden?', timestamp: new Date() },
    { id: 'stc2', sender: 'leo', text: '', timestamp: new Date(), widgetType: 'transfer', widgetData: { recipient: 'Max Mustermann', amount: 800, reference: 'Miete Dezember' } },
    { id: 'stc3', sender: 'user', text: 'Ja, senden', timestamp: new Date() },
    { id: 'stc4', sender: 'leo', text: '✅ €800 an Max Mustermann gesendet!\n\nReferenz: Miete Dezember\n\nSoll ich das als monatlich wiederkehrend speichern?', timestamp: new Date() },
    { id: 'stc5', sender: 'user', text: 'Ja bitte', timestamp: new Date() },
    { id: 'stc6', sender: 'leo', text: '📅 Erledigt! Ich erinnere dich jeden Monat am 1. an die Miete.\n\nDu kannst die Erinnerung jederzeit in den Einstellungen anpassen.', timestamp: new Date() }
  ]
},

// STORY 4: Spending Insight (Adult)
spending_deep_dive: {
  id: 'spending_deep_dive',
  name: '📊 Ausgabenanalyse',
  description: 'Detaillierte Ausgabenübersicht',
  category: 'adult',
  messages: [
    { id: 'sdd1', sender: 'user', text: 'Wo geht mein Geld hin?', timestamp: new Date() },
    { id: 'sdd2', sender: 'leo', text: 'Lass mich das analysieren... 🔍', timestamp: new Date() },
    { id: 'sdd3', sender: 'leo', text: 'November 2025 Zusammenfassung:', timestamp: new Date(), widgetType: 'spending_chart', widgetData: { category: 'Monat November', amount: 2145.67, percentChange: -9.8, breakdown: [{ name: 'Wohnen', amount: 850 }, { name: 'Essen', amount: 420 }, { name: 'Transport', amount: 280 }] } },
    { id: 'sdd4', sender: 'leo', text: '💡 Auffälligkeiten:\n\n1. Essen: +€67 mehr als üblich (12 Restaurant-Besuche)\n2. Shopping: €0 - gut gespart!\n3. Abos: €61.87 (Netflix nicht genutzt seit 45 Tagen)\n\nMöchtest du Spartipps?', timestamp: new Date() },
    { id: 'sdd5', sender: 'user', text: 'Was ist mit Netflix?', timestamp: new Date() },
    { id: 'sdd6', sender: 'leo', text: 'Du zahlst €17.99/Monat für Netflix, aber hast seit 45 Tagen nichts geschaut.\n\nDas sind €215.88 pro Jahr!\n\nOptionen:\n• Kündigen (spart €215.88/Jahr)\n• Pausieren (spart bis du wieder schauen willst)\n• Behalten (kein Urteil!)', timestamp: new Date(), widgetType: 'subscription_card', widgetData: { name: 'Netflix', amount: 17.99, lastUsed: '45 Tage', action: 'Kündigen empfohlen' } }
  ]
}
```

---

## Summary of Implementation Tasks

### Immediate (Week 1)
1. Create `quiz-generator.ts`
2. Create `gamification.ts`
3. Connect quiz widget to real quiz state
4. Add XP display to Junior dashboard

### Short-term (Week 2-3)
1. Create Achievements screen
2. Create Savings Goals screen
3. Fix non-functional buttons
4. Add demo sidebar user stories

### Medium-term (Week 4-6)
1. Implement real leaderboard
2. Add streak tracking
3. Create parent dashboard
4. Implement notifications

---

*Last Updated: November 2025*
