# Настройка GitHub Pages для Ruscord

## Шаги для активации деплоя:

1. **Перейдите в настройки репозитория:**
   - Откройте https://github.com/Vadyaaaaaa/Ruscord/settings/pages

2. **Настройте GitHub Pages:**
   - В разделе "Source" выберите "GitHub Actions"
   - Сохраните изменения

3. **Настройте переменные окружения (опционально):**
   - Перейдите в Settings → Secrets and variables → Actions
   - Добавьте секрет `VITE_API_URL` с URL вашего backend сервера
   - Например: `https://your-backend.railway.app` или `https://your-backend.render.com`

4. **Дождитесь завершения деплоя:**
   - После пуша в ветку `main` автоматически запустится workflow
   - Проверьте статус в разделе "Actions" вашего репозитория
   - После успешного деплоя сайт будет доступен по адресу:
     `https://vadyaaaaaa.github.io/Ruscord/`

## Важно:

- **Backend нужно задеплоить отдельно** (GitHub Pages поддерживает только статические сайты)
- Рекомендуемые сервисы для backend: Railway, Render, Fly.io
- После деплоя backend, обновите секрет `VITE_API_URL` в настройках репозитория

## Локальная разработка:

Для локальной разработки backend должен быть запущен на `http://localhost:3001`

