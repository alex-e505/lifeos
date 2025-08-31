# 🧠 База знаний amoCRM

Экспертная база знаний по интеграциям и автоматизации amoCRM.

## 📚 Структура базы знаний

### 🎯 Основные разделы
```
Knowledge_Base/
├── 📘 AmoCRM_Basics/           # Основы работы с amoCRM
├── 🔗 API_Documentation/       # Документация по API
├── 🛠️ Integration_Patterns/    # Паттерны интеграций
├── 💾 Code_Examples/           # Примеры кода
├── 🔧 Tools_Libraries/         # Инструменты и библиотеки
├── 🐛 Troubleshooting/         # Решение проблем
├── 📋 Best_Practices/          # Лучшие практики
├── 🎓 Training_Materials/      # Обучающие материалы
├── 📊 Case_Studies/            # Разборы проектов
└── 🆕 Updates_News/            # Обновления и новости
```

## 📘 AmoCRM Основы

### Архитектура системы
- **Сущности:** Сделки, Контакты, Компании, Задачи
- **Воронки:** Настройка этапов продаж
- **Поля:** Кастомные поля и их типы
- **Пользователи:** Роли и права доступа
- **Интеграции:** API, виджеты, хуки

### Базовые концепции
- **Pipeline (воронка)** - последовательность этапов
- **Entity (сущность)** - объект системы (сделка, контакт)
- **Custom fields** - дополнительные поля
- **Webhooks** - уведомления о событиях
- **Widgets** - дополнительные приложения

### Типовые задачи
1. **Настройка воронок** - создание этапов продаж
2. **Кастомизация полей** - добавление нужных полей
3. **Настройка прав** - управление доступом
4. **Автоматизация** - создание бизнес-процессов
5. **Интеграции** - подключение внешних систем

## 🔗 API Documentation

### REST API v4
- **Базовый URL:** `https://subdomain.amocrm.ru/api/v4/`
- **Аутентификация:** OAuth 2.0
- **Формат данных:** JSON
- **Лимиты:** 7000 запросов/час
- **SDK:** Официальные библиотеки

### Основные эндпоинты
```
GET /api/v4/leads              # Получить сделки
POST /api/v4/leads             # Создать сделки
PATCH /api/v4/leads            # Обновить сделки
GET /api/v4/contacts           # Получить контакты
GET /api/v4/companies          # Получить компании
GET /api/v4/tasks              # Получить задачи
GET /api/v4/users              # Получить пользователей
GET /api/v4/webhooks           # Управление хуками
```

### Авторизация OAuth 2.0
```php
// Получение токена
$token = getAccessToken($client_id, $client_secret, $auth_code);

// Использование в запросах
$headers = [
    'Authorization: Bearer ' . $token['access_token'],
    'Content-Type: application/json'
];
```

### Webhooks (уведомления)
```json
{
    "account_id": 123456,
    "events": [
        {
            "type": "lead:status_changed",
            "entity_id": 789,
            "entity_type": "lead",
            "created_at": 1234567890
        }
    ]
}
```

## 🛠️ Паттерны интеграций

### 1. Синхронизация данных
**Задача:** Двусторонняя синхронизация между amoCRM и внешней системой

**Решение:**
- Webhooks для отслеживания изменений
- Очередь задач для обработки
- Mapping полей между системами
- Conflict resolution при коллизиях

### 2. Импорт лидов из форм
**Задача:** Автоматическое создание сделок из веб-форм

**Решение:**
```php
// Обработчик формы
function processWebForm($formData) {
    $lead = [
        'name' => $formData['company'] . ' - заявка с сайта',
        'price' => 0,
        'custom_fields_values' => [
            ['field_id' => 123, 'values' => [['value' => $formData['phone']]]],
            ['field_id' => 124, 'values' => [['value' => $formData['email']]]]
        ]
    ];
    
    return createLead($lead);
}
```

### 3. Интеграция с 1C
**Задача:** Обмен данными между amoCRM и 1C

**Компоненты:**
- **Обмен клиентами** - синхронизация контактов/компаний
- **Обмен заказами** - передача сделок в 1C
- **Обмен товарами** - справочники номенклатуры
- **Финансовая сверка** - сопоставление платежей

### 4. Email-маркетинг интеграция
**Задача:** Интеграция с системами email-рассылок

**Функции:**
- Автоматическая сегментация контактов
- Синхронизация статусов подписки
- Отслеживание событий (открытия, клики)
- Создание лидов из кампаний

### 5. IP-телефония
**Задача:** Интеграция с АТС

**Возможности:**
- Click-to-call из карточки клиента
- Автоматическое создание задач после звонков
- Запись разговоров в карточке
- Статистика звонков по менеджерам

## 💾 Примеры кода

### Базовый класс для работы с API
```php
class AmoCRMClient {
    private $accessToken;
    private $subdomain;
    
    public function __construct($subdomain, $accessToken) {
        $this->subdomain = $subdomain;
        $this->accessToken = $accessToken;
    }
    
    public function makeRequest($method, $endpoint, $data = null) {
        $url = "https://{$this->subdomain}.amocrm.ru/api/v4{$endpoint}";
        
        $headers = [
            'Authorization: Bearer ' . $this->accessToken,
            'Content-Type: application/json'
        ];
        
        $curl = curl_init();
        curl_setopt_array($curl, [
            CURLOPT_URL => $url,
            CURLOPT_HTTPHEADER => $headers,
            CURLOPT_RETURNTRANSFER => true,
            CURLOPT_CUSTOMREQUEST => $method,
            CURLOPT_POSTFIELDS => $data ? json_encode($data) : null
        ]);
        
        $response = curl_exec($curl);
        curl_close($curl);
        
        return json_decode($response, true);
    }
}
```

### Создание сделки с контактом
```php
function createLeadWithContact($name, $phone, $email, $price = 0) {
    $client = new AmoCRMClient($subdomain, $accessToken);
    
    // Создаем контакт
    $contact = [
        'name' => $name,
        'custom_fields_values' => [
            ['field_id' => PHONE_FIELD_ID, 'values' => [['value' => $phone]]],
            ['field_id' => EMAIL_FIELD_ID, 'values' => [['value' => $email]]]
        ]
    ];
    
    $contactResult = $client->makeRequest('POST', '/contacts', [$contact]);
    $contactId = $contactResult['_embedded']['contacts'][0]['id'];
    
    // Создаем сделку
    $lead = [
        'name' => "Заявка от {$name}",
        'price' => $price,
        'pipeline_id' => PIPELINE_ID,
        'status_id' => STATUS_ID,
        '_embedded' => [
            'contacts' => [['id' => $contactId]]
        ]
    ];
    
    return $client->makeRequest('POST', '/leads', [$lead]);
}
```

### Обработчик webhook
```php
function processWebhook($webhookData) {
    foreach ($webhookData['events'] as $event) {
        switch ($event['type']) {
            case 'lead:status_changed':
                handleLeadStatusChange($event['entity_id']);
                break;
                
            case 'lead:added':
                handleNewLead($event['entity_id']);
                break;
                
            case 'contact:updated':
                handleContactUpdate($event['entity_id']);
                break;
        }
    }
}

function handleLeadStatusChange($leadId) {
    $client = new AmoCRMClient($subdomain, $accessToken);
    $lead = $client->makeRequest('GET', "/leads/{$leadId}");
    
    // Логика обработки изменения статуса
    if ($lead['status_id'] == CLOSED_WON_STATUS) {
        sendToAccountingSystem($lead);
        createWelcomeTask($lead);
    }
}
```

## 🔧 Инструменты и библиотеки

### Официальные SDK
- **PHP:** amocrm/amocrm-api-library
- **Python:** amoCRM-python-api  
- **JavaScript:** amocrm-api-js
- **C#:** AmoCrm.Api

### Полезные инструменты
- **Postman Collection** - готовые запросы для тестирования
- **amoCRM Webhook Tester** - инструмент для отладки webhooks
- **OAuth 2.0 Generator** - генератор токенов
- **Field ID Finder** - поиск ID полей

### Вспомогательные библиотеки
- **Guzzle** (PHP) - HTTP клиент
- **Requests** (Python) - HTTP библиотека
- **Axios** (JS) - HTTP клиент для браузера/Node.js

## 🐛 Troubleshooting

### Частые ошибки

#### 401 Unauthorized
**Причины:**
- Неверный access token
- Истекший токен
- Неправильный subdomain

**Решение:**
```php
// Проверка и обновление токена
if ($response['status'] == 401) {
    $newToken = refreshAccessToken($refreshToken);
    // Повторить запрос с новым токеном
}
```

#### 400 Bad Request  
**Причины:**
- Неверная структура JSON
- Обязательные поля не заполнены
- Неверные ID полей

**Отладка:**
```php
// Логирование запроса для анализа
error_log('Request: ' . json_encode($requestData));
error_log('Response: ' . $response);
```

#### 429 Too Many Requests
**Причины:**
- Превышен лимит запросов (7000/час)

**Решение:**
```php
// Реализация backoff стратегии
function makeRequestWithRetry($client, $method, $endpoint, $data, $maxRetries = 3) {
    for ($i = 0; $i < $maxRetries; $i++) {
        $response = $client->makeRequest($method, $endpoint, $data);
        
        if ($response['status'] != 429) {
            return $response;
        }
        
        sleep(pow(2, $i)); // Exponential backoff
    }
    
    throw new Exception('Rate limit exceeded after retries');
}
```

### Диагностика проблем

#### Проверка подключения
```php
function testConnection($subdomain, $accessToken) {
    $client = new AmoCRMClient($subdomain, $accessToken);
    $response = $client->makeRequest('GET', '/account');
    
    if (isset($response['id'])) {
        echo "Подключение успешно! Account ID: " . $response['id'];
    } else {
        echo "Ошибка подключения: " . json_encode($response);
    }
}
```

#### Проверка webhook
```php
function validateWebhook($webhookData, $secretKey) {
    $receivedHash = $_SERVER['HTTP_X_AMO_SIGNATURE'] ?? '';
    $calculatedHash = hash_hmac('sha1', $webhookData, $secretKey);
    
    return hash_equals($receivedHash, $calculatedHash);
}
```

## 📋 Лучшие практики

### Безопасность
- **Всегда проверяйте** подпись webhook
- **Не храните** access token в коде
- **Используйте HTTPS** для всех запросов
- **Ограничивайте права** OAuth приложения

### Производительность
- **Батчинг запросов** - отправка нескольких сущностей за раз
- **Кэширование** справочных данных
- **Асинхронная обработка** webhook
- **Мониторинг** лимитов API

### Надежность
- **Retry логика** для критичных операций
- **Логирование** всех взаимодействий
- **Валидация данных** перед отправкой
- **Graceful degradation** при недоступности API

### Код
```php
// Хорошо: батчинг запросов
$leads = [
    ['name' => 'Lead 1', 'price' => 1000],
    ['name' => 'Lead 2', 'price' => 2000],
    ['name' => 'Lead 3', 'price' => 3000]
];
$result = $client->makeRequest('POST', '/leads', $leads);

// Плохо: отдельные запросы
foreach ($leads as $lead) {
    $client->makeRequest('POST', '/leads', [$lead]);
}
```

---
*Создано: {{ date }}*
