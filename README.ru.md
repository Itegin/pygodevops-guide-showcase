<div align="center">

# PyGoDevOps-guide

**Самостоятельный трекер обучения по плану Python → Go → DevOps.**
12 фаз · 77 уроков · прогресс по трекам · написан и развёрнут на собственном домашнем сервере.

🇬🇧 [English version](README.md) · [Живой сайт](https://itgnroadmap.duckdns.org:9443/resume) · [Itegin](https://github.com/Itegin)

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![Flask](https://img.shields.io/badge/Flask-000000?style=flat-square&logo=flask&logoColor=white)
![SQLite](https://img.shields.io/badge/SQLite-003B57?style=flat-square&logo=sqlite&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)
![nginx](https://img.shields.io/badge/nginx-009639?style=flat-square&logo=nginx&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-2088FF?style=flat-square&logo=githubactions&logoColor=white)
![Source](https://img.shields.io/badge/Source-private-lightgrey?style=flat-square&logo=lock&logoColor=white)

</div>

---

### Что это

Flask-сайт, который я написал для себя, чтобы отслеживать прогресс по личному плану обучения «Python + Go → DevOps»: 12 фаз, 77 уроков, чекбокс на урок, прогресс-бар по каждому треку. Каждый урок — это Markdown-теория плюс опциональные шаги практики, проверки и квиз-самопроверка. Это не «сделай по туториалу», а рабочий продукт, которым я пользуюсь ежедневно — код, аутентификация, админка и CI написаны мной.

Этот репозиторий — **только витрина**: исходники закрыты (почему — [ниже](#почему-исходники-закрыты)). Здесь описание проекта и ссылка на живой рабочий сайт.

### Возможности

| | |
|---|---|
| **Мультипользовательский** | Своя аутентификация (без flask-login), на сессиях, роль администратора |
| **Гостевой режим** | Общий гостевой аккаунт в один клик — можно попробовать сайт без регистрации |
| **Трекинг прогресса** | Прогресс-бары по трекам, чекбокс на урок, заметки к урокам |
| **Формат урока** | Markdown-теория + опциональные шаги Практики / Проверки + опциональный квиз-самопроверка |
| **Админка** | Черновик → публикация для редактируемых секций страниц, правка текста по полям |
| **Аналитика** | Счётчик просмотров без cookies и без хранения IP (HMAC-хеш посетителя за день) |
| **Progressive enhancement** | Каждый чекбокс — настоящая HTML-форма; JS только ускоряет |

### Стек

Flask 3.1 · стандартный `sqlite3` (без ORM) · Markdown · gunicorn в Docker · чистый JS + написанный вручную CSS — без фронтенд-фреймворка, без сборщика, без Tailwind.

CI на каждый пуш: `ruff check`, `pytest`, сборка Docker-образа.

### Архитектура

```mermaid
flowchart LR
    U[Браузер посетителя] -->|HTTPS, TLS| N[nginx]
    N -->|reverse proxy| G[gunicorn]
    G --> F[Flask-приложение]
    F --> DB[(SQLite, на Docker volume)]
    CI[GitHub Actions] -->|ruff + pytest + docker build| F
```

Контейнер слушает только localhost; nginx терминирует TLS и единственный смотрит наружу. Весь стек крутится на домашнем сервере, доступном снаружи несмотря на CGNAT через SSH-туннель.

### Почему исходники закрыты

Это личный проект, которым я активно пользуюсь и продолжаю дорабатывать — код закрыт, а вот результат открыт: живой сайт доступен всем. Если хочется обсудить, как это устроено — [пишите](https://github.com/Itegin).

---

<sub>© Itegin. Текст и описание в этом репозитории приведены для ознакомления; сама разработка и её исходный код не лицензированы для повторного использования.</sub>
