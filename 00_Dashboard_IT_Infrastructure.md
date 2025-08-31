---
dashboard_type: "project_tracking"
project: "IT Infrastructure"
last_updated: 2025-01-31
tags: ["#infrastructure", "#dashboard", "#project"]
---

# 🖥️ Dashboard: IT-инфраструктура

## 🎯 Текущий статус проекта

```dataview
TABLE project_status, priority, estimated_time, target_completion
FROM "13_Business/Operations"
WHERE contains(tags, "#infrastructure")
```

## 🔥 Критичные задачи на сегодня

```dataview
TASK
FROM "13_Business/Operations/IT_Infrastructure_Project"
WHERE contains(line, "Критический") AND !completed
```

## 📅 Задачи этой недели

```dataview
TASK  
FROM "13_Business/Operations/IT_Infrastructure_Project"
WHERE contains(line, "Неделя 1-2") AND !completed
```

## ⚠️ Просроченные или блокирующие

```dataview
TASK
FROM "13_Business/Operations/IT_Infrastructure_Project" 
WHERE contains(line, "dependencies") AND !completed
```

## 📊 Прогресс по компонентам

### 🌐 VPN Сервер
- **Статус:** Планирование
- **Прогресс:** 0/6 задач
- **Время:** 0/20 часов

### 🛡️ AdGuard Home  
- **Статус:** Планирование
- **Прогресс:** 0/6 задач
- **Время:** 0/8 часов

### 🗂️ Self-hosted Git
- **Статус:** Планирование
- **Прогресс:** 0/6 задач
- **Время:** 0/12 часов

### 🔐 Vaultwarden
- **Статус:** Планирование
- **Прогресс:** 0/7 задач
- **Время:** 0/15 часов

## 💰 Бюджет

- **Месячные расходы:** $30
- **Единоразовые:** $15
- **Статус бюджета:** ✅ Утвержден

## 🔄 Следующие действия

1. **Сегодня:** Выбрать VPS провайдера
2. **Завтра:** Заказать сервер
3. **Эта неделя:** Настроить базовую безопасность
4. **Следующая неделя:** Развернуть VPN

## 📞 Контакты и ресурсы

- **VPS провайдеры:** Hetzner, DigitalOcean, Vultr
- **Документация:** Сохранена в Knowledge_Base
- **Backup план:** 3-2-1 правило
- **Support:** Self-managed

---

*Обновляется автоматически через Dataview*  
*Последнее обновление: {{ date }}*
