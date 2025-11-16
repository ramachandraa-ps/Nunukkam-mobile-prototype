# Design Document

## Overview

This document outlines the technical design for the Nunukkam Student Portal React Native mobile application. The application is a frontend-only prototype that demonstrates the complete user interface and user experience without backend integration. The design focuses on creating a maintainable, scalable component architecture with realistic mock data to simulate a fully functional learning management system.

### Technology Stack

- **Framework**: React Native with Expo SDK (latest stable version)
- **Navigation**: React Navigation v6 (Stack Navigator, Bottom Tab Navigator)
- **State Management**: React Context API for global state, useState/useReducer for local state
- **Styling**: React Native StyleSheet API with theme system
- **Icons**: @expo/vector-icons (Material Icons)
- **Data**: JSON mock data files with TypeScript interfaces
- **Development**: TypeScript for type safety

### Design Principles

1. **Component Reusability**: Create atomic, reusable components for common UI patterns
2. **Separation of Concerns**: Separate presentation, logic, and data layers
3. **Mock Data Realism**: Use realistic data structures that mirror actual backend responses
4. **Theme Consistency**: Centralized theme configuration for colors, spacing, and typography
5. **Performance**: Optimize list rendering and minimize re-renders

## Architecture

### High-Level Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                     React Native App                         │
├─────────────────────────────────────────────────────────────┤
│  Navigation Layer (React Navigation)                         │
│  ├── Auth Stack (Login, Forgot Password)                    │
│  └── Main Tab Navigator                                      │
│      ├── Home Stack                                          │
│      ├── Journey Stack                                       │
│      ├── Resume Stack                                        │
│      ├── Mentorship Stack                                    │
│      └── Leaderboard Stack                                   │
├─────────────────────────────────────────────────────────────┤
│  Screen Components                                           │
│  ├── Authentication Screens                                  │
│  ├── Dashboard Screens                                       │
│  ├── Learning Journey Screens                               │
│  ├── Assessment Screens                                      │
│  ├── Resume Screens                                          │
│  ├── Mentorship Screens                                      │
│  └── Leaderboard Screens                                     │
├─────────────────────────────────────────────────────────────┤
│  Reusable Components                                         │
│  ├── UI Components (Button, Card, Input, etc.)             │
│  ├── Layout Components (Header, Container, etc.)           │
│  └── Feature Components (ProgressBar, TaskCard, etc.)      │
├─────────────────────────────────────────────────────────────┤
│  Context Providers                                           │
│  ├── AuthContext (user session)                             │
│  ├── ThemeContext (light/dark mode)                         │
│  └── DataContext (mock data access)                         │
├─────────────────────────────────────────────────────────────┤
│  Services & Utilities                                        │
│  ├── Mock Data Service (data loading)                       │
│  ├── Theme Service (color schemes)                          │
│  └── Utility Functions (date formatting, calculations)      │
├─────────────────────────────────────────────────────────────┤
│  Data Layer (Mock Data)                                      │
│  ├── students.json                                           │
│  ├── courses.json                                            │
│  ├── modules.json                                            │
│  ├── chapters.json                                           │
│  ├── assessments.json                                        │
│  ├── tasks.json                                              │
│  ├── mentorships.json                                        │
│  └── leaderboard.json                                        │
└─────────────────────────────────────────────────────────────┘
```

### Folder Structure

```
nunukkam-mobile-app/
├── App.tsx                          # Root component
├── app.json                         # Expo configuration
├── package.json                     # Dependencies
├── tsconfig.json                    # TypeScript configuration
├── src/
│   ├── navigation/
│   │   ├── AppNavigator.tsx         # Root navigator
│   │   ├── AuthNavigator.tsx        # Auth stack
│   │   ├── MainTabNavigator.tsx     # Bottom tab navigator
│   │   ├── HomeNavigator.tsx        # Home stack
│   │   ├── JourneyNavigator.tsx     # Journey stack
│   │   ├── ResumeNavigator.tsx      # Resume stack
│   │   ├── MentorshipNavigator.tsx  # Mentorship stack
│   │   └── LeaderboardNavigator.tsx # Leaderboard stack
│   ├── screens/
│   │   ├── auth/
│   │   │   ├── LoginScreen.tsx
│   │   │   └── ForgotPasswordScreen.tsx
│   │   ├── home/
│   │   │   └── HomeDashboardScreen.tsx
│   │   ├── journey/
│   │   │   ├── LearningJourneyScreen.tsx
│   │   │   ├── CoreSkillsScreen.tsx
│   │   │   ├── ModuleDetailScreen.tsx
│   │   │   ├── TaskDetailScreen.tsx
│   │   │   └── YourPerformanceScreen.tsx
│   │   ├── assessment/
│   │   │   ├── MCQAssessmentScreen.tsx
│   │   │   ├── TextAssessmentScreen.tsx
│   │   │   └── AssessmentResultsScreen.tsx
│   │   ├── resume/
│   │   │   ├── ResumeDashboardScreen.tsx
│   │   │   └── ResumeBuilderScreen.tsx
│   │   ├── mentorship/
│   │   │   ├── MentorshipDashboardScreen.tsx
│   │   │   ├── BookSessionScreen.tsx
│   │   │   ├── SessionNotesScreen.tsx
│   │   │   └── CancelSessionScreen.tsx
│   │   ├── leaderboard/
│   │   │   ├── LeaderboardMainScreen.tsx
│   │   │   ├── FullLeaderboardScreen.tsx
│   │   │   └── LeaderboardLockedScreen.tsx
│   │   └── profile/
│   │       └── UserProfileScreen.tsx
│   ├── components/
│   │   ├── common/
│   │   │   ├── Button.tsx
│   │   │   ├── Card.tsx
│   │   │   ├── Input.tsx
│   │   │   ├── Icon.tsx
│   │   │   ├── Avatar.tsx
│   │   │   ├── Badge.tsx
│   │   │   └── EmptyState.tsx
│   │   ├── layout/
│   │   │   ├── Container.tsx
│   │   │   ├── Header.tsx
│   │   │   ├── BottomNav.tsx
│   │   │   └── SafeAreaWrapper.tsx
│   │   └── features/
│   │       ├── ProgressBar.tsx
│   │       ├── ProgressCircle.tsx
│   │       ├── TaskCard.tsx
│   │       ├── ModuleCard.tsx
│   │       ├── ChapterCard.tsx
│   │       ├── CalendarView.tsx
│   │       ├── PieChart.tsx
│   │       ├── LeaderboardPodium.tsx
│   │       └── SessionCard.tsx
│   ├── contexts/
│   │   ├── AuthContext.tsx
│   │   ├── ThemeContext.tsx
│   │   └── DataContext.tsx
│   ├── services/
│   │   ├── mockDataService.ts
│   │   └── storageService.ts
│   ├── utils/
│   │   ├── dateUtils.ts
│   │   ├── progressUtils.ts
│   │   └── validationUtils.ts
│   ├── theme/
│   │   ├── colors.ts
│   │   ├── typography.ts
│   │   ├── spacing.ts
│   │   └── index.ts
│   ├── types/
│   │   ├── navigation.ts
│   │   ├── student.ts
│   │   ├── course.ts
│   │   ├── assessment.ts
│   │   ├── task.ts
│   │   ├── mentorship.ts
│   │   └── index.ts
│   └── data/
│       ├── students.json
│       ├── courses.json
│       ├── modules.json
│       ├── chapters.json
│       ├── assessments.json
│       ├── tasks.json
│       ├── mentorships.json
│       └── leaderboard.json
└── assets/
    ├── images/
    └── fonts/
```

## Components and Interfaces

### Core Components

#### 1. Navigation Components

**AppNavigator**
- Root navigator that determines auth state
- Renders AuthNavigator or MainTabNavigator based on login status
- Manages navigation state persistence

**MainTabNavigator**
- Bottom tab bar with 5 tabs
- Custom tab bar component with icons and labels
- Active/inactive state styling
- Badge indicators for notifications

#### 2. Screen Components

**LoginScreen**
- Email and password input fields with validation
- Sign in button with loading state
- Forgot password link
- Error message display
- Auto-focus on email field

**HomeDashboardScreen**
- Welcome header with user name
- Three progress bars (Modules, Chapters, Assessments)
- Calendar view with attendance indicators
- Pending tasks list (top 3)
- Updates/notifications section
- Pull-to-refresh functionality

**LearningJourneyScreen**
- Overall progress circular indicator
- Task completion bar (clickable)
- Skills accomplished pie chart with legend
- Weekly content horizontal scroll
- Badges section (grid or empty state)

**ModuleDetailScreen**
- Module list with expandable cards
- Progress bar at top
- Linear learning flow with lock states
- Chapter items with CTAs (View Notes, Take Test)
- Completion status indicators

**TaskDetailScreen**
- Filter chips (All, Overdue, Today, Upcoming, Completed)
- Task cards with priority dots
- Progress bars per task
- Action buttons (Start, Resume, Retake, Review)
- Deadline information

**MCQAssessmentScreen**
- Question display with options
- Timer in top right
- Radio button selection
- Submit button
- Tab switch warning modal

**ResumeDashboardScreen**
- Resume draft cards with thumbnails
- Action buttons (Edit, Download, Rename, Delete)
- Floating action button for new draft
- Empty state for no resumes

**MentorshipDashboardScreen**
- Upcoming session card with Join/Cancel buttons
- Past sessions list with View Notes buttons
- Empty states for no sessions
- Book session floating action button

**LeaderboardMainScreen**
- Filter chips (In Class, In College, At Nunukkam)
- User rank card with proficiency breakdown
- Top 3 podium display
- View full leaderboard button

#### 3. Reusable UI Components

**Button Component**
```typescript
interface ButtonProps {
  title: string;
  onPress: () => void;
  variant?: 'primary' | 'secondary' | 'outline' | 'danger';
  size?: 'small' | 'medium' | 'large';
  disabled?: boolean;
  loading?: boolean;
  icon?: string;
  fullWidth?: boolean;
}
```

**Card Component**
```typescript
interface CardProps {
  children: React.ReactNode;
  onPress?: () => void;
  style?: ViewStyle;
  shadow?: boolean;
}
```

**Input Component**
```typescript
interface InputProps {
  label?: string;
  value: string;
  onChangeText: (text: string) => void;
  placeholder?: string;
  secureTextEntry?: boolean;
  keyboardType?: KeyboardTypeOptions;
  error?: string;
  leftIcon?: string;
  rightIcon?: string;
  onRightIconPress?: () => void;
}
```

**ProgressBar Component**
```typescript
interface ProgressBarProps {
  progress: number; // 0-100
  label?: string;
  showPercentage?: boolean;
  color?: string;
  height?: number;
}
```

**TaskCard Component**
```typescript
interface TaskCardProps {
  task: Task;
  onActionPress: () => void;
}

interface Task {
  id: string;
  title: string;
  chapter: string;
  progress: number;
  deadline: Date;
  status: 'overdue' | 'today' | 'upcoming' | 'completed';
  action: 'start' | 'resume' | 'retake' | 'review';
}
```

## Data Models

### Student Model
```typescript
interface Student {
  id: string;
  name: string;
  email: string;
  profilePicture: string;
  college: string;
  batch: string;
  enrollmentDate: Date;
  progress: {
    modulesCompleted: number;
    totalModules: number;
    chaptersCompleted: number;
    totalChapters: number;
    assessmentsCompleted: number;
    totalAssessments: number;
  };
  attendance: {
    percentage: number;
    records: AttendanceRecord[];
  };
  skills: SkillProficiency[];
}

interface AttendanceRecord {
  date: Date;
  status: 'present' | 'absent' | 'rescheduled' | 'future';
}

interface SkillProficiency {
  skillName: string;
  level: 'expert' | 'intermediate' | 'novice';
  percentage: number;
}
```

### Course Model
```typescript
interface Course {
  id: string;
  name: string;
  description: string;
  coreSkills: CoreSkill[];
}

interface CoreSkill {
  id: string;
  name: string;
  description: string;
  duration: number; // in hours
  modules: Module[];
  progress: {
    completed: number;
    total: number;
  };
  locked: boolean;
}

interface Module {
  id: string;
  name: string;
  description: string;
  chapters: Chapter[];
  assessments: Assessment[];
}

interface Chapter {
  id: string;
  name: string;
  description: string;
  type: 'notes' | 'video' | 'practice';
  content: string; // URL or content reference
  completed: boolean;
  locked: boolean;
}
```

### Assessment Model
```typescript
interface Assessment {
  id: string;
  title: string;
  type: 'mcq' | 'text' | 'video';
  chapterId: string;
  duration: number; // in minutes
  passingScore: number;
  questions: Question[];
  deadline: Date;
  attempts: AssessmentAttempt[];
}

interface Question {
  id: string;
  text: string;
  type: 'mcq' | 'text';
  options?: string[]; // for MCQ
  correctAnswer?: string | number;
  points: number;
}

interface AssessmentAttempt {
  attemptNumber: number;
  date: Date;
  score: number;
  proficiencyLevel: 'expert' | 'intermediate' | 'novice';
  answers: Answer[];
}

interface Answer {
  questionId: string;
  answer: string | number;
  correct: boolean;
}
```

### Task Model
```typescript
interface Task {
  id: string;
  title: string;
  description: string;
  type: 'assessment' | 'notes' | 'practice';
  chapterId: string;
  chapterName: string;
  deadline: Date;
  priority: 'overdue' | 'high' | 'medium' | 'low';
  status: 'not_started' | 'in_progress' | 'completed' | 'failed';
  progress: number;
  action: 'start' | 'resume' | 'retake' | 'review';
}
```

### Mentorship Model
```typescript
interface MentorshipSession {
  id: string;
  mentorId: string;
  mentorName: string;
  mentorTitle: string;
  mentorPhoto: string;
  date: Date;
  startTime: string;
  endTime: string;
  duration: number; // in minutes
  meetingLink: string;
  status: 'upcoming' | 'completed' | 'cancelled';
  notes?: SessionNotes;
}

interface SessionNotes {
  discussionPoints: string[];
  actionItems: ActionItem[];
}

interface ActionItem {
  id: string;
  description: string;
  completed: boolean;
  attachments: string[];
}
```

### Resume Model
```typescript
interface ResumeDraft {
  id: string;
  title: string;
  lastEdited: Date;
  thumbnail: string;
  sections: {
    summary: string;
    qualifications: Qualification[];
    internships: Experience[];
    workExperience: Experience[];
    projects: Project[];
    certifications: Certification[];
    skills: Skills;
  };
}

interface Qualification {
  degree: string;
  institution: string;
  year: number;
  percentage: number;
  documents: string[];
}

interface Experience {
  title: string;
  company: string;
  startDate: Date;
  endDate: Date | null;
  description: string;
  certificate: string;
}

interface Project {
  title: string;
  description: string;
  technologies: string[];
  link?: string;
}

interface Certification {
  title: string;
  issuedBy: string;
  issueDate: Date;
  expiryDate?: Date;
  certificate: string;
}

interface Skills {
  hardSkills: Skill[];
  softSkills: Skill[];
  languages: Language[];
}

interface Skill {
  name: string;
  proficiency: 'beginner' | 'intermediate' | 'advanced' | 'expert';
}

interface Language {
  name: string;
  proficiency: 'basic' | 'conversational' | 'fluent' | 'native';
}
```

### Leaderboard Model
```typescript
interface LeaderboardEntry {
  rank: number;
  studentId: string;
  studentName: string;
  profilePicture: string;
  points: number;
  proficiencyBreakdown: {
    expert: number;
    intermediate: number;
    novice: number;
  };
}

interface Leaderboard {
  scope: 'class' | 'college' | 'nunukkam';
  entries: LeaderboardEntry[];
  currentUserRank: number;
}
```

## Error Handling

### Validation Errors
- Display inline error messages below form fields
- Highlight invalid fields with red border
- Prevent form submission until all validations pass
- Show error icon next to invalid fields

### Empty States
- Display friendly illustrations for empty data
- Provide clear messaging (e.g., "No tasks yet")
- Include call-to-action buttons where appropriate
- Use consistent empty state component across app

### Loading States
- Show skeleton screens for initial data loading
- Display spinner for button actions
- Use pull-to-refresh for list screens
- Implement optimistic UI updates where possible

### Mock Data Errors
- Gracefully handle missing mock data files
- Provide fallback empty arrays/objects
- Log errors to console for debugging
- Show "Unable to load data" message with retry option

## Testing Strategy

### Component Testing
- Test individual components in isolation
- Verify prop handling and rendering
- Test user interactions (button presses, input changes)
- Validate conditional rendering logic

### Screen Testing
- Test navigation flows between screens
- Verify data display from mock data
- Test form submissions and validations
- Validate empty states and error states

### Integration Testing
- Test complete user flows (login to dashboard)
- Verify navigation stack behavior
- Test context provider data flow
- Validate theme switching

### Manual Testing Checklist
- Test on iOS and Android simulators
- Verify all screens render correctly
- Test navigation between all screens
- Validate form inputs and validations
- Check dark mode appearance
- Test scroll behavior on long lists
- Verify button interactions and feedback
- Test empty states and error messages
- Validate progress calculations
- Check calendar date interactions

## Performance Considerations

### List Optimization
- Use FlatList with keyExtractor for long lists
- Implement getItemLayout for fixed-height items
- Use windowSize prop to limit rendered items
- Memoize list item components with React.memo

### Image Optimization
- Use appropriate image sizes for thumbnails
- Implement lazy loading for images
- Cache images with Expo Image component
- Provide placeholder images during load

### State Management
- Minimize context re-renders with useMemo
- Use useCallback for event handlers
- Split contexts by concern (auth, theme, data)
- Avoid unnecessary state updates

### Navigation Performance
- Use lazy loading for screen components
- Implement screen pre-fetching for common flows
- Optimize tab navigator rendering
- Use navigation.setOptions for dynamic headers

## Accessibility

### Screen Reader Support
- Add accessibilityLabel to all interactive elements
- Use accessibilityHint for complex interactions
- Mark decorative images as accessibilityElementsHidden
- Provide accessibilityRole for semantic elements

### Touch Targets
- Ensure minimum 44x44 pixel touch targets
- Add padding around small interactive elements
- Use hitSlop prop for icon buttons
- Provide visual feedback on press

### Color Contrast
- Ensure 4.5:1 contrast ratio for text
- Use both color and text/icons for status
- Test dark mode contrast ratios
- Avoid color-only information

### Keyboard Navigation
- Support tab navigation for forms
- Implement returnKeyType for input fields
- Auto-focus first input on screen load
- Handle keyboard dismiss on submit

## Theme System

### Color Palette
```typescript
const colors = {
  light: {
    primary: '#7c3bed',
    secondary: '#4A90E2',
    success: '#50C878',
    warning: '#FFA500',
    danger: '#D9534F',
    background: '#F5F7FA',
    card: '#FFFFFF',
    text: '#333333',
    textSecondary: '#757575',
    border: '#E0E0E0',
  },
  dark: {
    primary: '#9b5fff',
    secondary: '#5fa3ff',
    success: '#6dd98d',
    warning: '#ffb733',
    danger: '#ff6b6b',
    background: '#121212',
    card: '#1E1E1E',
    text: '#E0E0E0',
    textSecondary: '#B0B0B0',
    border: '#333333',
  },
};
```

### Typography
```typescript
const typography = {
  h1: { fontSize: 32, fontWeight: '700', lineHeight: 40 },
  h2: { fontSize: 24, fontWeight: '700', lineHeight: 32 },
  h3: { fontSize: 20, fontWeight: '600', lineHeight: 28 },
  body: { fontSize: 16, fontWeight: '400', lineHeight: 24 },
  bodySmall: { fontSize: 14, fontWeight: '400', lineHeight: 20 },
  caption: { fontSize: 12, fontWeight: '400', lineHeight: 16 },
  button: { fontSize: 16, fontWeight: '600', lineHeight: 24 },
};
```

### Spacing
```typescript
const spacing = {
  xs: 4,
  sm: 8,
  md: 16,
  lg: 24,
  xl: 32,
  xxl: 48,
};
```

## Security Considerations

### Mock Authentication
- Store auth token in memory (not persisted)
- Clear auth state on app restart
- Implement logout functionality
- No actual password validation (mock only)

### Data Privacy
- No real user data in mock files
- Use placeholder images from public sources
- Avoid storing sensitive information
- Clear all data on logout

## Future Enhancements

### Phase 2 Features (Not in Current Scope)
- Backend API integration
- Real authentication with JWT
- Data persistence with AsyncStorage
- Push notifications
- Offline mode support
- Video recording for assessments
- PDF generation for resumes
- Real-time leaderboard updates
- Chat with mentors
- File upload functionality
- Analytics tracking
- Crash reporting
- Deep linking
- Share functionality
- Biometric authentication
