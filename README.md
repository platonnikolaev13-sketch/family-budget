# 💰 Семейный бюджет

Многопользовательское приложение для учёта семейных расходов и доходов.

## Возможности

- 🔐 Регистрация и вход (логин + пароль)
- 👨‍👩‍👧‍👦 Одна семья — один общий бюджет
- 🔑 Вход по коду приглашения (передать близким)
- 💵 Учёт **доходов** и **расходов**
- 📊 Статистика: по категориям, дням, участникам
- 📈 График расходов по дням месяца
- 🎯 Бюджеты и лимиты по категориям (с индикацией перерасхода)
- 📤 Экспорт в **Excel** и **JSON**
- 📂 Импорт из JSON
- 🔄 **Real-time** — все члены семьи видят изменения мгновенно
- 📱 Работает как приложение (PWA-режим через браузер)

## Локальный запуск

```bash
pip install -r requirements.txt
python app.py
```
Открыть http://localhost:5000

## Деплой на Render.com (бесплатно)

1. Залейте проект на GitHub
2. [render.com](https://render.com) → **New → Web Service**
3. Подключите репозиторий
4. **Build Command:** `pip install -r requirements.txt`
5. **Start Command:** `gunicorn -w 1 --threads 8 -b 0.0.0.0:$PORT app:app`
6. **Environment Variables:**
   - `SECRET_KEY` = любая случайная строка (например, из [random.org](https://www.random.org/strings/))
   - `DB_PATH` = `/data/budget.db`
7. **Add Disk** (обязательно для сохранения данных!):
   - Settings → Disks → **Add Disk**
   - Name: `data`
   - Mount Path: `/data`
   - Size: 1 GB (free)
8. **Create Web Service**

## Как пользоваться семьёй

1. Один член семьи **регистрируется** → выбирает «Создать семью» → задаёт название
2. В разделе **«Настройки»** он видит **код приглашения** (например, `AB7K2XM9`)
3. Передаёт код остальным — они регистрируются → «Войти по коду» → вводят его
4. Все видят общие расходы/доходы **в реальном времени** 🔄

## Стек

- **Backend:** Flask + Flask-SocketIO + SQLite
- **Frontend:** Vanilla JS + Chart.js + Socket.IO
- **Auth:** сессии Flask + Werkzeug password hashing
- **Excel:** openpyxl