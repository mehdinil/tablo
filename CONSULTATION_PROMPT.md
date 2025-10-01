# پرامپت مشاوره برای پروژه Tablo (GoalPad)

```
سلام! من یک پروژه Flutter دارم به اسم "Tablo" (GoalPad) که در حال توسعه است و نیاز به مشاوره دارم.

📱 **درباره پروژه:**
یک اپلیکیشن شخصی برای مدیریت اهداف، عادت‌ها و ژورنال نویسی با معماری offline-first

🎯 **ویژگی‌های اصلی:**
1. **مدیریت اهداف (Goals)**: ساخت و پیگیری اهداف با اولویت و تاریخ سررسید
2. **ردیابی عادت‌ها (Habits)**: ایجاد عادت‌های روزانه/هفتگی با شمارش streak و نمایش فعالیت
3. **ژورنال نویسی (Journal)**: نوشتن یادداشت‌های روزانه با ردیابی حالت و سیستم تگ
4. **مدیریت تسک‌ها (Tasks)**: افزودن تسک به اهداف با پیگیری تکمیل

⚙️ **استک تکنولوژی:**
- **Framework**: Flutter 3.4+ با null-safety
- **State Management**: Riverpod 2.5
- **Local Storage**: Hive 2.2 (offline-first, NoSQL)
- **UI Design**: Material 3 Design System
- **Code Generation**: build_runner برای Hive adapters
- **Utilities**: UUID برای ID generation، intl برای i18n

🏗️ **معماری پروژه:**
- معماری feature-based با جداسازی واضح
- ساختار: data/local → models → logic → ui
- 4 مدل اصلی: Goal, Task, Habit, JournalEntry
- همه داده‌ها در Hive boxes ذخیره می‌شوند

✅ **قابلیت‌های پیاده‌شده:**
- CRUD کامل برای Goals
- سیستم Task management
- Habit tracking با streak counter
- Journal entries با mood tracking
- ذخیره‌سازی محلی با Hive
- UI مدرن با Material 3

🎯 **اهداف آینده:**
- اضافه کردن Export/Import داده‌ها
- سیستم Notification برای یادآوری عادت‌ها و اهداف
- پیگیری پیشرفت اهداف با Progress Bar
- آمار و Insights برای عادت‌ها
- پشتیبانی از Dark Mode
- [سایر ویژگی‌هایی که نیاز دارم]

💡 **سوالات/کمک مورد نیاز من:**
[اینجا سوال یا موضوعی که می‌خواهی درباره‌اش مشاوره بگیری را بنویس، مثلاً:]
- چطور می‌تونم سیستم notification محلی پیاده کنم؟
- بهترین روش برای اضافه کردن قابلیت export/import JSON چیه؟
- چطور می‌تونم analytics و statistics برای habits اضافه کنم؟
- پیشنهادات UX برای بهبود تجربه کاربری
- راهکار برای اضافه کردن cloud sync در آینده (optional)
```

---

## نحوه استفاده:

این پرامپت رو کپی کن و قسمت **"سوالات/کمک مورد نیاز من"** رو با سوال خودت پر کن. به این ترتیب ChatGPT اطلاعات کامل از پروژه‌ت داره و می‌تونه مشاوره هدفمند بده! 🚀

## نمونه سوالات مفید:

### برای مرحله شروع پروژه:
- بهترین ساختار فولدر برای یک پروژه Flutter با معماری feature-based چیه؟
- چطور Hive رو برای offline storage به درستی setup کنم؟
- پیشنهادات برای طراحی مدل‌های داده Goal, Task, Habit, JournalEntry

### برای توسعه ویژگی‌ها:
- پیاده‌سازی habit streak counter با Riverpod
- طراحی UI برای habit tracking با Material 3
- سیستم تگ‌گذاری برای journal entries
- Progress tracking برای اهداف

### برای بهبود عملکرد:
- بهینه‌سازی Hive queries برای داده‌های زیاد
- مدیریت state با Riverpod در اپ‌های پیچیده
- کش کردن داده‌ها برای بهبود سرعت

### برای ویژگی‌های پیشرفته:
- پیاده‌سازی local notifications
- Export/Import داده‌ها به JSON
- آمار و نمودار برای habits
- Dark mode implementation
- Cloud sync strategy