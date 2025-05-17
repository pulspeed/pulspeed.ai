# 🚀 Pulspeed

Pulspeed is a service for **automated website performance monitoring**, analyzing Lighthouse metrics, and generating AI-powered optimization recommendations using GPT.

It tracks key web performance metrics, builds historical graphs, detects blocking scripts, and suggests actionable improvements for faster load and better UX.

---

## 🧑‍💻 Who is it for?

Pulspeed is useful for:

- 💼 **Product and tech teams** — monitor performance regressions after releases
- 🧪 **QA engineers** — compare speed before and after optimization
- 📊 **SEO specialists** — track PageSpeed metrics affecting rankings
- 🔧 **Frontend developers** — get clear Lighthouse-based improvement tasks
- 🛡 **DevOps/SRE** — track TTFB and server responsiveness

---

## 📦 Features

- Scheduled monitoring (daily / weekly)
- Support for Desktop and Mobile strategies
- Tracks core Lighthouse metrics:
  - First Contentful Paint (FCP)
  - Largest Contentful Paint (LCP)
  - Time to Interactive (TTI)
  - Total Blocking Time (TBT)
  - Time to First Byte (TTFB)
  - Cumulative Layout Shift (CLS)
- Performance history graphs
- GitHub webhook integration on push
- AI-powered action items
- Multi-site and multi-user support

---

## 📌 Getting Started

1. Register at [pulspeed.ai](https://pulspeed.ai)
2. Add your site and choose scan frequency
3. (Optional) Connect GitHub webhook
4. Monitor performance and apply AI recommendations

---

## 🧩 API

### 🔐 Authentication

All requests require `Authorization: Bearer {token}`  
(you can get a token in your account settings)

---

### 📥 `POST /api/webhook`

Trigger a scan on repository push event (e.g. from GitHub):

```http
POST /api/webhook
Content-Type: application/json
Authorization: Bearer {token}
```

Example body:

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

Get the user's sites:

```http
GET /api/sites
Authorization: Bearer {token}
```

---

### 📈 `GET /api/sites/{id}/snapshots`

List snapshots for a site:

```http
GET /api/sites/42/snapshots
Authorization: Bearer {token}
```

Example response:

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

Get AI-powered recommendations based on the latest scan:

```http
GET /api/sites/42/recommendations
Authorization: Bearer {token}
```

---

## 📦 Open Source?

The core service is closed-source.  
Some tools (CLI, webhook utilities, lightweight agent) may be open-sourced later.

---

## 📬 Contact

- email: [pulspeed.dev@proton.me](mailto:pulspeed.dev@proton.me)
- issues: via GitHub Issues
- Telegram (optional): t.me/pulspeed_ai

---

## ✨ Roadmap

- [x] Cron & webhook scanning
- [x] Performance charts
- [x] AI-based recommendations
- [ ] Slack/Telegram notifications
- [ ] GitHub/GitLab repo integration
- [ ] Lighthouse diff between commits
- [ ] REST & Webhook UI playground

---

## 🧠 Team & CI Integration

Pulspeed can be integrated into CI/CD pipelines: run scans on push and block deployments if TTI, LCP, or TBT get worse.
