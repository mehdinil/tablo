# پرامپت مشاوره ChatGPT برای پروژه Tablo (GoalPad)

## نسخه فارسی

```markdown
سلام! من یک پروژه Flutter دارم به اسم "Tablo" (که GoalPad هم نامیده می‌شود) که در حال توسعه است و نیاز به مشاوره تخصصی دارم.

## 📱 **معرفی پروژه:**
Tablo یک اپلیکیشن شخصی برای مدیریت زندگی و بهره‌وری است که با رویکرد offline-first طراحی شده. هدف اصلی این اپلیکیشن کمک به کاربران برای دستیابی به اهداف، ایجاد عادت‌های مثبت و ثبت احساسات روزانه است.

## 🎯 **ویژگی‌های اصلی پیاده‌سازی شده:**

### 1. **مدیریت اهداف (Goals Management)**
- ایجاد اهداف کوتاه‌مدت و بلندمدت
- تعیین اولویت‌بندی (High, Medium, Low)
- تاریخ سررسید و یادآوری
- دسته‌بندی اهداف (Personal, Work, Health, Education, etc.)
- وضعیت پیشرفت (Not Started, In Progress, Completed)

### 2. **ردیابی عادت‌ها (Habit Tracking)**
- ایجاد عادت‌های روزانه، هفتگی یا ماهانه
- سیستم Streak Counter برای انگیزه
- Heat map برای نمایش فعالیت‌ها
- آمار تکمیل عادت‌ها
- یادآوری‌های زمان‌بندی شده

### 3. **ژورنال و یادداشت‌برداری (Journaling)**
- ثبت یادداشت‌های روزانه
- Mood Tracking با emoji
- سیستم تگ‌گذاری برای دسته‌بندی
- جستجو در یادداشت‌ها
- پیوست عکس به یادداشت‌ها (planned)

### 4. **مدیریت وظایف (Task Management)**
- اضافه کردن تسک‌های فرعی به هر هدف
- چک‌لیست برای تکمیل تسک‌ها
- تاریخ سررسید برای تسک‌ها
- اولویت‌بندی تسک‌ها

## ⚙️ **استک تکنولوژی و وابستگی‌ها:**

### **Core Dependencies:**
```yaml
dependencies:
  flutter: ^3.4.0
  
  # State Management
  flutter_riverpod: ^2.5.1
  riverpod_annotation: ^2.3.5
  
  # Local Storage
  hive: ^2.2.3
  hive_flutter: ^1.1.0
  
  # Utilities
  uuid: ^4.3.3
  intl: ^0.19.0
  path_provider: ^2.1.2
  
  # UI Components
  fl_chart: ^0.66.2  # برای نمودارها
  table_calendar: ^3.0.9  # برای تقویم
  flutter_slidable: ^3.0.1  # برای swipe actions
  
dev_dependencies:
  build_runner: ^2.4.8
  hive_generator: ^2.0.1
  riverpod_generator: ^2.4.0
```

## 🏗️ **معماری و ساختار پروژه:**

```
lib/
├── main.dart
├── app.dart
├── core/
│   ├── constants/
│   │   ├── app_colors.dart
│   │   ├── app_strings.dart
│   │   └── app_themes.dart
│   ├── utils/
│   │   ├── date_formatter.dart
│   │   └── validators.dart
│   └── widgets/
│       ├── custom_button.dart
│       └── loading_indicator.dart
│
├── features/
│   ├── goals/
│   │   ├── data/
│   │   │   ├── local/
│   │   │   │   └── goals_local_storage.dart
│   │   │   └── repositories/
│   │   │       └── goals_repository.dart
│   │   ├── domain/
│   │   │   ├── models/
│   │   │   │   ├── goal.dart
│   │   │   │   └── goal.g.dart
│   │   │   └── providers/
│   │   │       └── goals_provider.dart
│   │   └── presentation/
│   │       ├── screens/
│   │       │   ├── goals_list_screen.dart
│   │       │   ├── goal_detail_screen.dart
│   │       │   └── add_goal_screen.dart
│   │       └── widgets/
│   │           ├── goal_card.dart
│   │           └── goal_progress_bar.dart
│   │
│   ├── habits/
│   │   ├── data/
│   │   ├── domain/
│   │   └── presentation/
│   │
│   ├── journal/
│   │   ├── data/
│   │   ├── domain/
│   │   └── presentation/
│   │
│   └── tasks/
│       ├── data/
│       ├── domain/
│       └── presentation/
│
└── shared/
    ├── navigation/
    │   └── app_router.dart
    └── services/
        ├── notification_service.dart
        └── storage_service.dart
```

## 📊 **مدل‌های داده (Data Models):**

### Goal Model:
```dart
@HiveType(typeId: 0)
class Goal extends HiveObject {
  @HiveField(0)
  final String id;
  
  @HiveField(1)
  String title;
  
  @HiveField(2)
  String? description;
  
  @HiveField(3)
  Priority priority;
  
  @HiveField(4)
  Category category;
  
  @HiveField(5)
  DateTime? deadline;
  
  @HiveField(6)
  GoalStatus status;
  
  @HiveField(7)
  List<String> taskIds;
  
  @HiveField(8)
  DateTime createdAt;
  
  @HiveField(9)
  DateTime? completedAt;
  
  @HiveField(10)
  double progress; // 0.0 to 1.0
}
```

### Habit Model:
```dart
@HiveType(typeId: 1)
class Habit extends HiveObject {
  @HiveField(0)
  final String id;
  
  @HiveField(1)
  String name;
  
  @HiveField(2)
  String? description;
  
  @HiveField(3)
  HabitFrequency frequency;
  
  @HiveField(4)
  List<DateTime> completedDates;
  
  @HiveField(5)
  int currentStreak;
  
  @HiveField(6)
  int bestStreak;
  
  @HiveField(7)
  TimeOfDay? reminderTime;
  
  @HiveField(8)
  bool isActive;
}
```

### JournalEntry Model:
```dart
@HiveType(typeId: 2)
class JournalEntry extends HiveObject {
  @HiveField(0)
  final String id;
  
  @HiveField(1)
  String content;
  
  @HiveField(2)
  DateTime date;
  
  @HiveField(3)
  Mood mood;
  
  @HiveField(4)
  List<String> tags;
  
  @HiveField(5)
  List<String>? imagePaths;
  
  @HiveField(6)
  Weather? weather;
  
  @HiveField(7)
  Location? location;
}
```

## ✅ **قابلیت‌های تکمیل شده:**
- ✅ Setup اولیه Flutter با null-safety
- ✅ پیکربندی Riverpod برای state management
- ✅ راه‌اندازی Hive برای ذخیره‌سازی محلی
- ✅ طراحی مدل‌های داده با Hive adapters
- ✅ پیاده‌سازی CRUD برای Goals
- ✅ سیستم Task management متصل به Goals
- ✅ Habit tracking با streak counter
- ✅ Journal entries با mood tracking
- ✅ Material 3 theming و responsive UI
- ✅ Bottom navigation برای بخش‌های اصلی

## 🚀 **قابلیت‌های در حال توسعه:**
- ⏳ سیستم Notification محلی
- ⏳ Export/Import داده‌ها (JSON/CSV)
- ⏳ Dashboard با آمار و insights
- ⏳ Dark mode support
- ⏳ Backup & Restore
- ⏳ Widget برای home screen

## 🎯 **اهداف و برنامه‌های آینده:**

### **Phase 1 (Current) - Core Features:**
- تکمیل سیستم notification
- پیاده‌سازی data export/import
- افزودن charts و statistics
- بهبود UX/UI

### **Phase 2 - Enhanced Features:**
- سیستم Gamification (badges, achievements)
- Templates برای اهداف و عادت‌ها
- Social features (share progress)
- AI-powered insights
- Voice notes برای journal

### **Phase 3 - Advanced Features:**
- Cloud sync با Firebase/Supabase
- Multi-platform support (Web, Desktop)
- Collaboration features
- Integration با تقویم‌های خارجی
- API برای third-party integrations

## 🐛 **چالش‌های فعلی:**
1. بهینه‌سازی performance برای لیست‌های طولانی
2. مدیریت حافظه در Hive boxes
3. Sync بین صفحات مختلف
4. Complex queries در Hive
5. Testing strategy برای offline features

## 📈 **معیارهای موفقیت:**
- User retention rate > 60% after 30 days
- Daily active users
- Average session duration > 5 minutes
- Habit completion rate > 70%
- User satisfaction score > 4.5/5

## 💡 **سوالات و نیازمندی‌های مشاوره:**

[اینجا سوال خود را وارد کنید، مثال‌ها:]

### مثال سوالات:

1. **Notification System:**
   - بهترین package برای local notifications چیست؟
   - چطور می‌توانم recurring notifications پیاده کنم؟
   - راهکار برای notification در iOS background؟

2. **Data Management:**
   - آیا Hive برای این حجم داده مناسب است یا به SQLite نیاز دارم؟
   - بهترین روش برای backup/restore چیست؟
   - چطور می‌توانم data migration انجام دهم؟

3. **Performance:**
   - راهکارهای بهینه‌سازی برای لیست‌های طولانی؟
   - Best practices برای image caching؟
   - چطور memory leaks را شناسایی کنم؟

4. **Architecture:**
   - آیا معماری فعلی scalable است؟
   - پیشنهاد برای بهبود separation of concerns؟
   - Testing strategy مناسب؟

5. **UX/UI:**
   - Best practices برای onboarding flow؟
   - راهکار برای smooth animations؟
   - Accessibility considerations؟

## 📚 **منابع و مستندات مرتبط:**
- [Flutter Documentation](https://flutter.dev/docs)
- [Riverpod Documentation](https://riverpod.dev)
- [Hive Documentation](https://docs.hivedb.dev)
- [Material 3 Design System](https://m3.material.io)

## 🤝 **نوع کمک مورد نیاز:**
- [ ] Code Review
- [ ] Architecture Consultation
- [ ] Performance Optimization
- [ ] UI/UX Improvement
- [ ] Testing Strategy
- [ ] Feature Implementation
- [ ] Bug Fixing
- [ ] Best Practices

---

لطفاً با توجه به اطلاعات فوق، در زمینه [موضوع مورد نظر] راهنمایی کنید.
```

## نسخه انگلیسی (English Version)

```markdown
Hello! I have a Flutter project called "Tablo" (also known as GoalPad) that is under development and I need expert consultation.

## 📱 **Project Overview:**
Tablo is a personal productivity and life management application designed with an offline-first approach. The main goal is to help users achieve their goals, build positive habits, and track their daily emotions.

## 🎯 **Core Features Implemented:**

### 1. **Goals Management**
- Create short-term and long-term goals
- Priority levels (High, Medium, Low)
- Deadlines and reminders
- Categories (Personal, Work, Health, Education, etc.)
- Progress status (Not Started, In Progress, Completed)

### 2. **Habit Tracking**
- Create daily, weekly, or monthly habits
- Streak counter system for motivation
- Heat map for activity visualization
- Habit completion statistics
- Scheduled reminders

### 3. **Journaling**
- Daily journal entries
- Mood tracking with emojis
- Tagging system for categorization
- Search functionality
- Image attachments (planned)

### 4. **Task Management**
- Add subtasks to each goal
- Checklist for task completion
- Task deadlines
- Task prioritization

## ⚙️ **Technology Stack:**

### **Core Dependencies:**
```yaml
dependencies:
  flutter: ^3.4.0
  
  # State Management
  flutter_riverpod: ^2.5.1
  riverpod_annotation: ^2.3.5
  
  # Local Storage
  hive: ^2.2.3
  hive_flutter: ^1.1.0
  
  # Utilities
  uuid: ^4.3.3
  intl: ^0.19.0
  path_provider: ^2.1.2
  
  # UI Components
  fl_chart: ^0.66.2
  table_calendar: ^3.0.9
  flutter_slidable: ^3.0.1
  
dev_dependencies:
  build_runner: ^2.4.8
  hive_generator: ^2.0.1
  riverpod_generator: ^2.4.0
```

## 🏗️ **Architecture & Project Structure:**

```
lib/
├── main.dart
├── app.dart
├── core/
│   ├── constants/
│   ├── utils/
│   └── widgets/
├── features/
│   ├── goals/
│   │   ├── data/
│   │   ├── domain/
│   │   └── presentation/
│   ├── habits/
│   ├── journal/
│   └── tasks/
└── shared/
    ├── navigation/
    └── services/
```

## 📊 **Data Models:**

[Include Goal, Habit, JournalEntry, and Task models as shown above]

## ✅ **Completed Features:**
- ✅ Initial Flutter setup with null-safety
- ✅ Riverpod configuration for state management
- ✅ Hive setup for local storage
- ✅ Data models with Hive adapters
- ✅ CRUD operations for Goals
- ✅ Task management system connected to Goals
- ✅ Habit tracking with streak counter
- ✅ Journal entries with mood tracking
- ✅ Material 3 theming and responsive UI
- ✅ Bottom navigation for main sections

## 🚀 **Features in Development:**
- ⏳ Local notification system
- ⏳ Data export/import (JSON/CSV)
- ⏳ Dashboard with statistics and insights
- ⏳ Dark mode support
- ⏳ Backup & Restore functionality
- ⏳ Home screen widget

## 🎯 **Roadmap:**

### **Phase 1 (Current) - Core Features:**
- Complete notification system
- Implement data export/import
- Add charts and statistics
- Improve UX/UI

### **Phase 2 - Enhanced Features:**
- Gamification system (badges, achievements)
- Templates for goals and habits
- Social features (share progress)
- AI-powered insights
- Voice notes for journal

### **Phase 3 - Advanced Features:**
- Cloud sync with Firebase/Supabase
- Multi-platform support (Web, Desktop)
- Collaboration features
- External calendar integration
- API for third-party integrations

## 🐛 **Current Challenges:**
1. Performance optimization for long lists
2. Memory management in Hive boxes
3. State synchronization between screens
4. Complex queries in Hive
5. Testing strategy for offline features

## 💡 **Consultation Questions/Needs:**

[Insert your specific question here]

### Example Questions:

1. **Notification System:**
   - What's the best package for local notifications?
   - How to implement recurring notifications?
   - iOS background notification strategies?

2. **Data Management:**
   - Is Hive suitable for this data volume or should I use SQLite?
   - Best approach for backup/restore?
   - How to handle data migrations?

3. **Performance:**
   - Optimization strategies for long lists?
   - Best practices for image caching?
   - How to identify memory leaks?

4. **Architecture:**
   - Is the current architecture scalable?
   - Suggestions for improving separation of concerns?
   - Appropriate testing strategy?

5. **UX/UI:**
   - Best practices for onboarding flow?
   - Strategies for smooth animations?
   - Accessibility considerations?

## 🤝 **Type of Help Needed:**
- [ ] Code Review
- [ ] Architecture Consultation
- [ ] Performance Optimization
- [ ] UI/UX Improvement
- [ ] Testing Strategy
- [ ] Feature Implementation
- [ ] Bug Fixing
- [ ] Best Practices

---

Please provide guidance on [your specific topic] based on the above information.
```

## نکات استفاده:

1. **انتخاب نسخه**: از نسخه فارسی یا انگلیسی بر اساس نیاز استفاده کنید
2. **شخصی‌سازی**: قسمت‌های [bracketed] را با اطلاعات خود جایگزین کنید
3. **سوالات**: سوالات خود را در بخش مربوطه وارد کنید
4. **جزئیات**: هر چه اطلاعات دقیق‌تری ارائه دهید، پاسخ بهتری دریافت خواهید کرد
5. **به‌روزرسانی**: این template را با پیشرفت پروژه به‌روز کنید

## مثال‌های کاربردی:

### برای سوال درباره Notifications:
```
من می‌خواهم سیستم notification محلی پیاده کنم که:
- هر روز ساعت مشخصی برای habits یادآوری بفرسته
- برای deadline اهداف 24 ساعت قبل اطلاع بده
- حتی وقتی app بسته است کار کنه
لطفاً بهترین package و روش پیاده‌سازی رو پیشنهاد بدید.
```

### برای Performance Optimization:
```
لیست habits من وقتی بیش از 50 آیتم داره کند می‌شه.
از ListView.builder استفاده می‌کنم ولی همچنان lag دارم.
چطور می‌تونم performance رو بهبود بدم؟
```

### برای Architecture Review:
```
آیا استفاده از Riverpod + Hive برای این پروژه مناسبه؟
برای آینده که می‌خوام cloud sync اضافه کنم، چه تغییراتی باید بدم؟
```