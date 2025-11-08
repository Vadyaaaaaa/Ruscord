# Инструкция по развертыванию RuDis

## 🌐 Варианты развертывания

### Вариант 1: Vercel (Frontend) + Railway (Backend) - Рекомендуется

#### Frontend на Vercel:
1. Зайдите на [vercel.com](https://vercel.com)
2. Войдите через GitHub
3. Нажмите "New Project"
4. Импортируйте репозиторий `Vadyaaaaaa/RuDis`
5. **Root Directory:** выберите `client`
6. **Build Command:** `npm run build`
7. **Output Directory:** `build`
8. **Install Command:** `npm install`
9. Добавьте переменную окружения:
   - `REACT_APP_API_URL` = `https://your-backend-url.railway.app`

#### Backend на Railway:
1. Зайдите на [railway.app](https://railway.app)
2. Войдите через GitHub
3. Нажмите "New Project" -> "Deploy from GitHub repo"
4. Выберите репозиторий `Vadyaaaaaa/RuDis`
5. В настройках проекта:
   - **Root Directory:** `server`
   - **Start Command:** `node index.js`
6. Добавьте переменные окружения:
   - `PORT` = `5000` (или любой другой)
   - `NODE_ENV` = `production`
7. Railway автоматически предоставит URL для вашего API

### Вариант 2: Netlify (Frontend) + Render (Backend)

#### Frontend на Netlify:
1. Зайдите на [netlify.com](https://netlify.com)
2. Войдите через GitHub
3. Нажмите "New site from Git"
4. Выберите репозиторий
5. Настройки:
   - **Base directory:** `client`
   - **Build command:** `npm run build`
   - **Publish directory:** `client/build`
6. Добавьте переменную окружения:
   - `REACT_APP_API_URL` = ваш URL бэкенда

#### Backend на Render:
1. Зайдите на [render.com](https://render.com)
2. Войдите через GitHub
3. Нажмите "New" -> "Web Service"
4. Подключите репозиторий
5. Настройки:
   - **Root Directory:** `server`
   - **Build Command:** `npm install`
   - **Start Command:** `node index.js`
   - **Environment:** Node

### Вариант 3: Heroku (Full Stack)

1. Установите Heroku CLI
2. Войдите: `heroku login`
3. Создайте приложение: `heroku create rudis-app`
4. Добавьте buildpacks:
   ```bash
   heroku buildpacks:add heroku/nodejs --app rudis-app
   ```
5. Настройте `Procfile` в корне проекта:
   ```
   web: cd server && node index.js
   ```
6. Настройте `package.json` в корне:
   ```json
   {
     "scripts": {
       "start": "cd server && node index.js",
       "heroku-postbuild": "cd client && npm install && npm run build"
     }
   }
   ```
7. Деплой: `git push heroku main`

## 🔧 Настройка CORS

Убедитесь, что в `server/index.js` настроен CORS для вашего фронтенда:

```javascript
const io = socketIo(server, {
  cors: {
    origin: "https://your-frontend-url.vercel.app", // или другой URL
    methods: ["GET", "POST"]
  }
});

app.use(cors({
  origin: "https://your-frontend-url.vercel.app"
}));
```

## 📝 Важные замечания

1. **База данных:** Текущая реализация использует JSON файл. Для продакшена рекомендуется:
   - MongoDB Atlas (бесплатный tier)
   - PostgreSQL на Railway/Render
   - Supabase

2. **Переменные окружения:** Создайте файл `.env` на сервере:
   ```
   PORT=5000
   JWT_SECRET=your-secret-key
   NODE_ENV=production
   ```

3. **Socket.io:** Убедитесь, что WebSocket соединения разрешены на вашем хостинге.

## 🚀 Быстрый старт (Vercel + Railway)

1. **Backend (Railway):**
   - Создайте проект на Railway
   - Подключите GitHub репозиторий
   - Root: `server`
   - Получите URL (например: `https://rudis-backend.railway.app`)

2. **Frontend (Vercel):**
   - Создайте проект на Vercel
   - Root: `client`
   - Добавьте переменную: `REACT_APP_API_URL=https://rudis-backend.railway.app`
   - Деплой!

3. **Обновите CORS** в `server/index.js` с URL вашего фронтенда

Готово! 🎉

