# Thesis Propostal:MoodSync

## Українською

**Попередня робоча назва проєкту:**
Розробка кросплатформної екосистеми MoodSync для трекінгу емоційного стану користувача з хмарною синхронізацією та аналітикою трендів.

**Актуальність та проблематика:**
Існуючі застосунки для трекінгу настрою (Daylio, Moodfit, Bearable) переважно орієнтовані на локальне зберігання даних в межах одного пристрою, що обмежує користувачів, які працюють з кількома пристроями (телефон, планшет), і пропонують лише базові історичні графіки без прогнозної аналітики. Не вирішеною залишається проблема надійної синхронізації даних в умовах нестабільного з'єднання (offline-first) з коректним розв'язанням конфліктів при одночасному внесенні записів з різних пристроїв. Додатково, чутливі персональні дані про емоційний стан здебільшого зберігаються без належного шифрування. Потребу становить система з надійною архітектурою синхронізації, захищеним зберіганням даних та елементами прогнозної аналітики емоційних трендів користувача.

**Сформована ідея продукту:**

Кросплатформна система, що складається з трьох основних компонентів:

1. **Мобільний клієнт (Android, Kotlin/Jetpack Compose):** фіксація настрою користувача, локальне offline-first зберігання з чергою відкладених синхронізацій.
2. **Серверний бекенд (FastAPI):** бізнес-логіка, автентифікація користувачів, синхронізація даних між пристроями, генерація аналітичних звітів.
3. **Аналітичний модуль (Python, scikit-learn):** виявлення трендів та прогнозування динаміки емоційного стану на основі історичних даних користувача.

**Детальний опис функціоналу (Core Features):**

1. **Логування настрою:** фіксація категорій, тегів, нотаток та шкали інтенсивності емоційного стану (Android, Jetpack Compose).
2. **Offline-first зберігання даних:** локальна база (Room) з чергою відкладених змін (outbox pattern) для роботи без стабільного інтернет-з'єднання.
3. **Хмарна синхронізація між пристроями:** розв'язання конфліктів одночасного редагування за timestamp-стратегією (last-write-wins / поле-орієнтований merge).
4. **Захищена автентифікація та зберігання:** JWT (access + refresh токени), шифрування чутливих даних на клієнті (SQLCipher), передача виключно по HTTPS.
5. **Аналітична панель:** динамічна візуалізація трендів настрою за тиждень/місяць/рік.
6. **Прогнозування динаміки настрою:** легка ML-модель (лінійна регресія / ковзне середнє) для виявлення тенденцій та потенційних негативних сплесків.
7. **Push-нагадування:** щоденні сповіщення про необхідність внести запис (WorkManager).

**Попередній інструментарій та технологічний стек:**

- **Мови програмування:** Kotlin, Python.
- **Архітектурні патерни:** Offline-first / Outbox pattern, Repository, MVVM.
- **Фреймворки та бібліотеки:** Jetpack Compose, Room, WorkManager, FastAPI, SQLAlchemy, Pydantic, scikit-learn, Pandas.
- **Бази даних:** PostgreSQL (сервер, основне сховище), Room + SQLCipher (клієнт, зашифроване локальне сховище).
- **DevOps та безпека:** Docker, Docker Compose, GitHub Actions (CI/CD), Bandit (статичний аналіз Python-коду), Android Lint.

## English

**Preliminary Project Title:**
Development of a Cross-Platform MoodSync Ecosystem for User Emotional State Tracking with Cloud Synchronization and Trend Analytics.

**Relevance and Problem Statement:**
Existing mood-tracking applications (Daylio, Moodfit, Bearable) are primarily oriented toward local, single-device data storage, limiting users who work across multiple devices, and offer only basic historical charts without predictive analytics. The problem of reliable data synchronization under unstable connectivity (offline-first) with correct conflict resolution when entries are made simultaneously from different devices remains unaddressed. Additionally, sensitive personal emotional data is often stored without proper encryption. There is a need for a system with a reliable synchronization architecture, secure data storage, and elements of predictive analytics of the user's emotional trends.

**Product Idea:**

A cross-platform system consisting of three core components:

1. **Mobile Client (Android, Kotlin/Jetpack Compose):** captures the user's mood, with offline-first local storage and a queue of deferred synchronizations.
2. **Backend (FastAPI):** implements business logic, user authentication, cross-device data synchronization, and analytics report generation.
3. **Analytics Module (Python, scikit-learn):** detects trends and forecasts the dynamics of the user's emotional state based on historical data.

**Core Features:**

1. **Mood Logging:** recording categories, tags, notes, and an intensity scale for emotional state (Android, Jetpack Compose).
2. **Offline-First Data Storage:** local database (Room) with a deferred-change queue (outbox pattern) for operation without a stable internet connection.
3. **Cloud Synchronization Across Devices:** conflict resolution for simultaneous edits via a timestamp-based strategy (last-write-wins / field-level merge).
4. **Secure Authentication and Storage:** JWT (access + refresh tokens), client-side encryption of sensitive data (SQLCipher), HTTPS-only transport.
5. **Analytics Dashboard:** dynamic visualization of mood trends over week/month/year.
6. **Mood Trend Forecasting:** a lightweight ML model (linear regression / moving average) to detect tendencies and potential negative spikes.
7. **Push Reminders:** daily notifications prompting the user to log an entry (WorkManager).

**Preliminary Technology Stack:**

- **Languages:** Kotlin, Python.
- **Architectural Patterns:** Offline-first / Outbox pattern, Repository, MVVM.
- **Frameworks:** Jetpack Compose, Room, WorkManager, FastAPI, SQLAlchemy, Pydantic, scikit-learn, Pandas.
- **Databases:** PostgreSQL (server, primary store), Room + SQLCipher (client, encrypted local store).
- **DevOps & Security:** Docker, Docker Compose, GitHub Actions (CI/CD), Bandit (Python static analysis), Android Lint.