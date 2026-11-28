🛠 <b>Модуль 2 (PRO): Инженерная база «Скрипт vs Система» — Production VPS, Docker &amp; Nginx</b>

Скрипт на ноутбуке работает до первой закрытой крышки или обрыва Wi-Fi. Чтобы автоматизация, парсеры, Telegram-боты и оркестры <code>n8n</code> работали 24/7 без сбоев, код переезжает в боевой Production-стек.

—

🔑 <b>1. Разработка: <code>.env</code> Fail-Fast и <code>git worktree</code></b>
• <b><code>.env</code> + <code>pydantic-settings</code>:</b> секреты под правами <code>chmod 600</code> + валидация при старте (падает сразу при ошибке конфигурации, а не на живом клиенте).
• <b><code>git worktree</code>:</b> изолированные папки для параллельных ИИ-агентов при общей базе <code>.git</code>. Помни про <code>git worktree remove</code> и <code>git worktree prune</code> после ручного удаления папки.

—

🚀 <b>2. Эволюция стека и Docker Compose</b>
1. <b>Script → FastAPI + Uvicorn → <code>systemd</code> (<code>Restart=always</code>) → Redis + ARQ/Celery</b> (защита от <code>504</code> при долгой генерации LLM).
2. <b>Ловушка Docker &amp; UFW:</b> пиши <code>"127.0.0.1:5678:5678"</code> — иначе Docker откроет порт через <code>iptables</code> в обход UFW.
3. <b>Race Condition БД:</b> <code>healthcheck</code> (<code>pg_isready</code>) + <code>depends_on: { postgres: { condition: service_healthy } }</code>.
4. <b>n8n v2.35+:</b> <code>N8N_WEBHOOK_URL</code> и <code>N8N_PROXY_HOPS=1</code>.

—

🛡️ <b>3. VPS Hardening, Nginx Reverse Proxy и отладка</b>
• <b>VPS:</b> SSH строго по ключам <code>Ed25519</code> (<code>PasswordAuthentication no</code>) + <code>UFW</code> (только порты <code>22</code>, <code>80</code>, <code>443</code>).
• <b>Nginx:</b> <code>map $http_upgrade $connection_upgrade</code>, <code>X-Forwarded-Proto $scheme</code>, <code>proxy_read_timeout 3600s</code>, SSL через <code>Certbot</code> (<code>/.well-known/acme-challenge/</code>).
• <b>Диагностика:</b> <code>502</code> = бэкенд упал (смотри <code>ss -tulpn</code> / <code>journalctl</code>); <code>504</code> = бэкенд завис; Telegram Webhook — <code>getWebhookInfo</code>.

—

🔗 <b>Интерактивный урок, инспектор конфигов PRO и симулятор инцидентов:</b>
<a href="https://DmitryMita.github.io/ai-academy-lessons/m02-script-vs-system-pro/">https://DmitryMita.github.io/ai-academy-lessons/m02-script-vs-system-pro/</a>
🎧 <i>Внутри — подкаст наставника (64kbps, темп -7% с паузами), терминальные трассировки и 4 PRO-проверки.</i>
