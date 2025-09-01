# LifeOS - Структура для Obsidian

#structure #obsidian #documentation

## 🧠 Философия организации для Obsidian

Структура оптимизирована для работы в Obsidian с упором на:
- **Связи через вики-ссылки** вместо иерархии папок
- **Теги для категоризации** и быстрого поиска
- **MOCs (Maps of Content)** для навигации
- **Плоская структура папок** для упрощения

## 📁 Физическая структура папок

```
lifeos/
├── 🏠 Home.md                    # Главная навигация
├── 👤 Profile MOC.md             # Карта профиля
├── 💼 Work MOC.md                # Карта работы
├── 🌟 Life MOC.md                # Карта жизни  
├── 📚 Learning MOC.md            # Карта обучения
│
├── Profile/                      # ⭐ Личная информация
│   ├── Personal_Info.md          # #profile #personal #identity
│   ├── Values_Principles.md      # #profile #values #principles
│   ├── Личная_карта.md          # #profile #map
│   ├── Identity_Documents/       # Документы
│   └── Photos_Media/             # Медиафайлы
│
├── Work/                         # 💼 Работа и финансы  
│   └── README.md                 # #work #career #money #business
│
├── Life/                         # 🌟 Жизнь
│   └── README.md                 # #life #goals #health #relationships
│
├── Learning/                     # 📚 Обучение
│   └── README.md                 # #learning #education #hobbies
│
├── Templates/                    # 📝 Шаблоны Obsidian
│   ├── Daily Note.md             # #template #daily
│   ├── Project.md                # #template #project  
│   ├── Person.md                 # #template #person
│   └── Goal.md                   # #template #goal
│
└── Attachments/                  # 📎 Медиафайлы
```

## 🗺️ Логическая структура (MOCs)

### 🏠 Home - Центральная навигация
- Точка входа в систему
- Ссылки на все MOCs
- Быстрые ссылки
- Основные теги

### 👤 Profile MOC - Карта личности
**Теги:** `#profile #personal #identity #values`
- Основная информация
- Ценности и принципы
- Документы и медиа
- Связи с другими MOCs

### 💼 Work MOC - Карта работы
**Теги:** `#work #career #money #finance #business #project`
- Профессиональная деятельность
- Финансовое планирование  
- Бизнес проекты
- Карьерное развитие

### 🌟 Life MOC - Карта жизни
**Теги:** `#life #goals #health #relationships #planning #habits`
- Жизненные цели
- Здоровье и благополучие
- Отношения и контакты
- Планирование времени

### 📚 Learning MOC - Карта развития  
**Теги:** `#learning #education #books #courses #hobbies #creativity #tools`
- Знания и обучение
- Творчество и хобби
- Инструменты и системы
- Исследования

## 🏷️ Система тегов

### Иерархия тегов
```
#profile
  └── #personal #identity #values #principles

#work  
  └── #career #money #finance #business #project #skills

#life
  └── #goals #health #relationships #planning #habits #family

#learning
  └── #education #books #courses #hobbies #creativity #tools

#meta
  └── #moc #template #index #daily
```

### Временные теги
- `#2024` `#2025` - по годам
- `#Q1` `#Q2` `#Q3` `#Q4` - по кварталам  
- `#january` `#february` - по месяцам
- `#daily` - ежедневные заметки

## 🔗 Принципы связывания

### 1. MOCs связывают контент
Каждый MOC содержит ссылки на релевантные заметки и подтемы.

### 2. Двунаправленные связи
Заметки ссылаются друг на друга для создания сети знаний.

### 3. Навигационные ссылки
В каждой заметке есть навигация к родительским MOCs.

### 4. Тематические кластеры
Связанные заметки группируются по темам через теги и ссылки.

## ✨ Преимущества для Obsidian

### 🔍 Быстрый поиск
- Поиск по тегам: `tag:#work`
- Поиск по ссылкам: `[[Home]]`
- Полнотекстовый поиск

### 📊 Визуализация связей
- График связей показывает структуру знаний
- Локальный граф для каждой заметки
- Анализ связей между темами

### 🚀 Эффективная навигация
- MOCs как карты для больших областей
- Быстрый переход через вики-ссылки
- Навигация по тегам

### 📝 Гибкое создание контента
- Шаблоны для типовых заметок
- Автоматическое связывание
- Динамические запросы через Dataview

---

**Навигация:** [[🏠 Home]] | **Создано:** {{date}}