# 📋 Processing Rules - Правила обработки отчётов

#ai #rules #processing #automation

## 🎯 Общие принципы

1. **Один отчёт = множество обновлений** - информация распределяется по разным файлам
2. **Сохранение связей** - создавать ссылки между связанными заметками  
3. **Временная привязка** - все записи датируются
4. **Теги для Dataview** - обязательные метаданные для запросов

## 🔍 Ключевые слова для категоризации

### 💼 Work (Работа)
**Проекты:** проект, задача, код, разработка, дедлайн, релиз
**Встречи:** встреча, звонок, презентация, обсуждение, совещание
**Финансы:** зарплата, доход, трата, покупка, инвестиции, бюджет
**Карьера:** собеседование, повышение, навык, резюме, LinkedIn

### 🌟 Life (Жизнь)  
**Здоровье:** спорт, тренировка, врач, лекарства, вес, пульс, давление
**Отношения:** встретился, позвонил, семья, друзья, свидание
**Цели:** цель, план, привычка, прогресс, достижение
**Быт:** дом, покупки, уборка, ремонт, путешествие

### 📚 Learning (Обучение)
**Чтение:** книга, статья, читал, прочитал, автор
**Курсы:** курс, лекция, урок, сертификат, экзамен
**Навыки:** изучал, практика, упражнение, туториал
**Творчество:** рисовал, писал, фото, музыка, хобби

## 📂 Структура файлов для создания

### Work файлы:
```
Work/
├── Projects/
│   └── [Project_Name].md           # #project #work #active
├── People/
│   └── [Person_Name].md            # #person #work #colleague  
├── Finance/
│   ├── Income.md                   # #finance #income #work
│   ├── Expenses.md                 # #finance #expenses
│   └── Investments.md              # #finance #investment
├── Meetings/
│   └── [YYYY-MM-DD]_[Topic].md     # #meeting #work
└── Achievements/
    └── [YYYY]_Achievements.md      # #achievement #work
```

### Life файлы:
```
Life/
├── Health/
│   ├── Fitness.md                  # #health #fitness #tracking
│   ├── Nutrition.md                # #health #nutrition
│   └── Medical.md                  # #health #medical
├── People/
│   ├── Family/
│   │   └── [Name].md               # #person #family
│   └── Friends/
│       └── [Name].md               # #person #friend
├── Goals/
│   ├── [YYYY]_Goals.md             # #goals #yearly
│   └── [Goal_Name].md              # #goal #active
├── Events/
│   └── [YYYY-MM-DD]_[Event].md     # #event #life
└── Habits/
    └── [Habit_Name].md             # #habit #tracking
```

### Learning файлы:
```
Learning/
├── Books/
│   └── [Book_Title].md             # #book #reading
├── Courses/
│   └── [Course_Name].md            # #course #education
├── Skills/
│   └── [Skill_Name].md             # #skill #development
├── Ideas/
│   └── [YYYY-MM-DD]_Ideas.md       # #idea #brainstorm
└── Projects/
    └── [Creative_Project].md       # #project #creative
```

## 🏷️ Система тегов для Dataview

### Основные категории:
- `#work` `#life` `#learning` `#ai-processed`

### Типы контента:
- `#project` `#person` `#goal` `#book` `#event` `#meeting` `#idea`

### Статусы:
- `#active` `#completed` `#paused` `#planned` `#cancelled`

### Приоритеты:
- `#high` `#medium` `#low`

### Временные:
- `#2025` `#2025-01` `#Q1` `#january`

### Контекстные:
- `#work-project` `#personal-goal` `#health-tracking` `#daily-report`

## 📝 Шаблоны создаваемых файлов

### Проект:
```markdown
---
created: 2025-01-15
updated: 2025-01-15
type: project
category: work
status: active
priority: medium
start_date: 2025-01-15
due_date: 2025-03-15
progress: 0
people: []
daily_sources: ["2025-01-15"]
---

# [Название проекта]

#project #work #active #ai-processed

## Описание
[Автоматически извлечённое из отчёта]

## История обновлений
### 2025-01-15
- [Информация из ежедневного отчёта]

## Связанные люди
[Автоматические ссылки]

## Файлы и ресурсы
[Ссылки на связанные материалы]
```

### Человек:
```markdown
---
created: 2025-01-15  
updated: 2025-01-15
type: person
category: work
relationship: colleague
last_contact: 2025-01-15
contact_frequency: weekly
daily_sources: ["2025-01-15"]
---

# [Имя Фамилия]

#person #work #colleague #ai-processed

## Контактная информация
[Если доступно]

## Журнал общения
### 2025-01-15
- [Информация из отчёта]

## Связанные проекты
[Автоматические ссылки]

## Заметки
[Дополнительная информация]
```

### Цель:
```markdown
---
created: 2025-01-15
updated: 2025-01-15  
type: goal
category: life
status: active
priority: high
target_date: 2025-12-31
progress: 0
metric: ""
daily_sources: ["2025-01-15"]
---

# [Название цели]

#goal #life #active #ai-processed

## Описание
[Извлечено из отчёта]

## Метрика успеха
[Как измерять прогресс]

## План действий
- [ ] [Шаги из отчёта]

## История прогресса  
### 2025-01-15
- Прогресс: 0%
- [Заметки из отчёта]

## Связанные заметки
[Автоматические ссылки]
```

## 🔄 Алгоритм обработки

### 1. Предварительный анализ
```
FOR каждое предложение в отчёте:
  IF содержит ключевые слова работы:
    category = "work"
  ELIF содержит ключевые слова жизни:
    category = "life"  
  ELIF содержит ключевые слова обучения:
    category = "learning"
```

### 2. Извлечение сущностей
```
FOR каждая категория:
  projects = extract_projects(text)
  people = extract_people(text)
  goals = extract_goals(text)
  activities = extract_activities(text)
```

### 3. Создание/обновление файлов
```
FOR каждая сущность:
  file_path = generate_path(category, type, name)
  IF file_exists(file_path):
    update_file(file_path, new_info)
  ELSE:
    create_file(file_path, template, new_info)
```

## 📊 Метаданные для Dataview

### Обязательные поля:
```yaml
created: дата создания
updated: дата последнего обновления  
type: тип записи (project/person/goal/etc)
category: основная категория (work/life/learning)
status: текущий статус
daily_sources: список дат отчётов-источников
```

### Дополнительные поля:
```yaml
priority: приоритет (high/medium/low)
progress: прогресс в процентах (0-100)
people: связанные люди
projects: связанные проекты  
start_date: дата начала
due_date: дата окончания
tags: дополнительные теги
```

---

**Навигация:** [[🤖 AI Context Guide]] | [[🏠 Home]]
