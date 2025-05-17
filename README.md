# 🚀 Pulspeed

Pulspeed — это сервис для **автоматического мониторинга производительности сайтов**, анализа метрик Lighthouse и генерации рекомендаций по оптимизации с помощью AI (GPT).  

Система отслеживает ключевые показатели сайта, строит графики изменений, выявляет проблемные скрипты и предлагает конкретные шаги по улучшению скорости загрузки и UX.

---

## 🧑‍💻 Кому это нужно?

Pulspeed полезен:

- 💼 **Продуктовым и техлид-командам** — следить за деградацией метрик после релизов
- 🧪 **QA-инженерам** — находить тяжелые страницы и замерять скорость до и после оптимизации
- 📊 **SEO-специалистам** — отслеживать метрики Google PageSpeed как фактор ранжирования
- 🔧 **Фронтенд-разработчикам** — получать actionable-рекомендации на основе Lighthouse
- 🛡 **DevOps/SRE** — следить за TTFB и временем ответа сервера

---

## 📦 Возможности

- Автоматический мониторинг по cron (ежедневно / еженедельно)
- Поддержка Desktop и Mobile стратегии сканирования
- Отображение ключевых Lighthouse-метрик:
  - First Contentful Paint (FCP)
  - Largest Contentful Paint (LCP)
  - Time to Interactive (TTI)
  - Total Blocking Time (TBT)
  - Time to First Byte (TTFB)
  - Cumulative Layout Shift (CLS)
- Графики изменения метрик во времени
- Вебхуки при пуше в репозиторий (например, GitHub Actions)
- Рекомендации и action items на базе GPT
- Поддержка нескольких сайтов и пользователей

---

## 📌 Быстрый старт

1. Зарегистрируйтесь на [pulspeed.ai](https://pulspeed.ai)
2. Добавьте свой сайт и выберите частоту сканирования
3. (Опционально) подключите GitHub webhook
4. Наблюдайте за метриками и внедряйте AI-рекомендации

---

## 🧩 API

### 🔐 Аутентификация

Все запросы требуют `Authorization: Bearer {token}`  
(токен можно получить в личном кабинете пользователя)

---

### 📥 `POST /api/webhook`

Получение пуш-события для триггера сканирования сайта (например, из GitHub):

```http
POST /api/webhook
Content-Type: application/json
Authorization: Bearer {token}
```

Пример тела запроса:

```json
{
  "event": "push",
  "repository": {
    "name": "my-project"
  }
}
```

---

### 📊 `GET /api/sites`

Получить список сайтов пользователя:

```http
GET /api/sites
Authorization: Bearer {token}
```

---

### 📈 `GET /api/sites/{id}/snapshots`

Получить список сканов сайта:

```http
GET /api/sites/42/snapshots
Authorization: Bearer {token}
```

Пример ответа:
```json
[
  {
    "id": 123,
    "taken_at": "2024-06-01T12:34:56Z",
    "fcp": 1234,
    "lcp": 1450,
    "tti": 3200,
    "tbt": 310,
    "ttfb": 140,
    "cls": 0.12,
    "score": 0.84
  }
]
```

---

### 📘 `GET /api/sites/{id}/recommendations`

Получить рекомендации от AI по последнему сканированию:

```http
GET /api/sites/42/recommendations
Authorization: Bearer {token}
```

---

## 📦 Open Source?

Основной сервис — закрытый.  
Часть компонентов (CLI, webhook utils, возможно, легковесный агент-сканер) планируется открыть.

---

## 📬 Обратная связь

- email: [pulspeed.dev@proton.me](mailto:pulspeed.dev@proton.me)
- issues: через GitHub Issues
- Telegram (опционально): t.me/pulspeed_ai

---

## ✨ Roadmap

- [x] Сканы по cron и webhook
- [x] Графики производительности
- [x] AI-рекомендации
- [ ] Slack/Telegram-нотификации
- [ ] Импорт из GitHub/GitLab
- [ ] Lighthouse diff на основе git-коммитов
- [ ] REST & Webhook UI Playground

---

## 🧠 Поддержка командной интеграции

Pulspeed можно интегрировать в CI/CD: запускать скан при пуше и блокировать релиз, если TTI, LCP или TBT ухудшились.
