# 📊 Dataview Templates - Шаблоны дашбордов

#dataview #dashboards #templates #ai

## 🎯 Готовые дашборды для Dataview

### 📅 Ежедневная сводка

```dataview
TABLE 
  status as "Статус",
  progress as "Прогресс", 
  priority as "Приоритет"
FROM #daily 
WHERE date(created) = date(today)
SORT created DESC
```

### 💼 Активные рабочие проекты

```dataview
TABLE 
  status as "Статус",
  progress + "%" as "Прогресс",
  due_date as "Дедлайн",
  people as "Команда"
FROM #project AND #work AND #active
SORT priority DESC, due_date ASC
```

### 🎯 Цели 2025

```dataview
TABLE 
  category as "Категория",
  progress + "%" as "Прогресс",
  target_date as "Цель к дате",
  status as "Статус"  
FROM #goal AND #2025
SORT progress DESC
```

### 👥 Недавние контакты

```dataview
TABLE 
  relationship as "Тип",
  last_contact as "Последний контакт", 
  contact_frequency as "Частота"
FROM #person 
WHERE last_contact > date(today) - dur(30 days)
SORT last_contact DESC
```

### 📚 Текущее обучение

```dataview
TABLE 
  type as "Тип",
  status as "Статус",
  progress + "%" as "Прогресс",
  updated as "Обновлено"
FROM #learning AND (#active OR #reading)
SORT updated DESC
```

### 💰 Финансовая сводка

```dataview
TABLE 
  type as "Тип",
  amount as "Сумма",
  category as "Категория",
  created as "Дата"
FROM #finance
WHERE created > date(today) - dur(30 days)
SORT created DESC
```

## 📈 Аналитические дашборды

### 📊 Прогресс по категориям

```dataview
TABLE 
  rows.category as "Категория",
  length(rows) as "Количество",
  round(average(rows.progress), 1) + "%" as "Средний прогресс"
FROM #project OR #goal
WHERE status = "active"
GROUP BY true
```

### ⏰ Активность по времени

```dataview
TABLE 
  rows.week as "Неделя",
  length(rows) as "Записей создано",
  length(filter(rows, (x) => x.type = "project")) as "Проектов",
  length(filter(rows, (x) => x.type = "goal")) as "Целей"
FROM ""
WHERE created > date(today) - dur(90 days)
GROUP BY dateformat(created, "yyyy-[W]WW")
SORT rows.week DESC
```

### 🏷️ Популярные теги

```dataview
TABLE 
  rows.tags as "Тег",
  length(rows) as "Использований"
FROM ""
WHERE tags
FLATTEN tags
GROUP BY tags
SORT length(rows) DESC
LIMIT 20
```

## 🎨 Специальные виды

### 📋 Канбан-доска проектов

```dataview
TABLE WITHOUT ID
  file.link as "Проект",
  choice(progress < 25, "🔴", choice(progress < 75, "🟡", "🟢")) as "",
  progress + "%" as "Прогресс"
FROM #project AND #work
WHERE status = "active"
SORT status, priority DESC
```

### 📅 Календарь событий

```dataview
CALENDAR created
FROM #event OR #meeting
WHERE created > date(today) - dur(365 days)
```

### 📊 График прогресса

```dataview
TABLE 
  progress as "Прогресс",
  "▓".repeat(progress / 10) + "░".repeat(10 - progress / 10) as "График"
FROM #goal AND #active
SORT progress DESC
```

## 🔍 Поисковые дашборды

### 🕵️ Поиск по ключевым словам

```dataview
LIST
FROM ""
WHERE contains(file.name, "проект") OR contains(file.tags, "project")
SORT file.mtime DESC
```

### 📝 Недавно обновлённые

```dataview
TABLE 
  updated as "Обновлено",
  type as "Тип",
  status as "Статус"
FROM ""
WHERE updated > date(today) - dur(7 days)
AND type != ""
SORT updated DESC
```

### ⚠️ Требуют внимания

```dataview
TABLE 
  due_date as "Дедлайн",
  priority as "Приоритет",
  progress as "Прогресс"
FROM #project OR #goal
WHERE status = "active" 
AND (
  due_date < date(today) + dur(7 days) OR
  priority = "high" OR
  progress = 0
)
SORT due_date ASC, priority DESC
```

## 📋 Шаблоны для MOCs

### 💼 Work MOC Dashboard

```dataview
## Активные проекты
TABLE progress + "%" as Прогресс, due_date as Дедлайн
FROM #project AND #work AND #active
SORT due_date ASC

## Недавние встречи  
LIST
FROM #meeting 
WHERE created > date(today) - dur(14 days)
SORT created DESC
LIMIT 5

## Финансы за месяц
TABLE amount as Сумма, category as Категория
FROM #finance 
WHERE created > date(today) - dur(30 days)
SORT created DESC
```

### 🌟 Life MOC Dashboard

```dataview
## Цели года
TABLE progress + "%" as Прогресс, target_date as "К дате"
FROM #goal AND #life AND #2025
SORT progress DESC

## Здоровье
LIST
FROM #health 
WHERE updated > date(today) - dur(7 days)
SORT updated DESC

## Контакты
TABLE last_contact as "Последний контакт"
FROM #person AND #friend
WHERE last_contact > date(today) - dur(14 days)
SORT last_contact DESC
```

### 📚 Learning MOC Dashboard

```dataview
## Текущее чтение
TABLE progress + "%" as Прогресс, status as Статус  
FROM #book AND (#reading OR #active)
SORT updated DESC

## Курсы
TABLE progress + "%" as Прогресс, due_date as Завершить
FROM #course AND #active
SORT due_date ASC

## Идеи для изучения
LIST
FROM #idea AND #learning
WHERE created > date(today) - dur(30 days)
SORT created DESC
LIMIT 10
```

## 🎛️ Персонализированные запросы

### 🎯 Мои приоритеты на сегодня

```dataview
TASK
FROM ""
WHERE !completed 
AND (due = date(today) OR priority = "high")
SORT priority DESC, due ASC
```

### 📊 Статистика месяца

```dataview
TABLE 
  "Проекты: " + length(filter(rows, (x) => x.type = "project")) as "Счётчики",
  "Цели: " + length(filter(rows, (x) => x.type = "goal")),
  "Встречи: " + length(filter(rows, (x) => x.type = "meeting"))
FROM ""
WHERE created > date(today) - dur(30 days)
GROUP BY true
```

---

**Навигация:** [[🤖 AI Context Guide]] | [[📋 Processing Rules]] | [[🏠 Home]]
