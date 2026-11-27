🛠 <b>Модуль 2 (BASE → PRO): Инженерная база «Скрипт vs Система»</b>

Разовый скрипт на ноутбуке работает, пока открыта крышка и не пропал Wi-Fi. Чтобы превратить автоматизацию в надёжного цифрового сотрудника 24/7 или коммерческий SaaS, код переезжает на боевую инфраструктуру.

—

🔑 <b>1. Гигиена разработки (CLI, <code>.env</code> и <code>git worktree</code>)</b>
• <b><code>.env</code> (сейф секретов):</b> все API-ключи и токены лежат отдельно от кода и закрыты через <code>.gitignore</code>.
• <b><code>git worktree</code>:</b> создаёт отдельную рабочую папку для каждой ветки при общей базе <code>.git</code> — два ИИ-агента работают параллельно без конфликтов файлов.

—

🚀 <b>2. 4 ступени эволюции: Скрипт → Система</b>
1. <b>Скрипт</b> (<code>python run.py</code>) — разовый запуск вручную.
2. <b>Веб-сервер</b> (<code>FastAPI</code> + <code>Uvicorn</code>) — круглосуточный приём HTTP-запросов от ботов и <code>n8n</code>.
3. <b>Фоновый демон</b> (<code>systemd</code> с <code>Restart=always</code> / <code>cron</code>) — автоподъём после сбоя и работа по расписанию.
4. <b>Очередь задач</b> (<code>Redis</code> + воркеры) — защита от зависания при резком наплыве клиентов.

—

🐳 <b>3. Docker, Ubuntu VPS и Nginx Reverse Proxy</b>
• <b>Docker Compose:</b> поднимает <code>n8n</code>, базу и бота за 30 секунд. Постоянные данные живут в <b>Volumes</b>, порт <code>127.0.0.1:5678</code> закрыт от интернета.
• <b>Безопасность VPS:</b> вход строго по <b>SSH-ключам</b> (пароли отключены) + файрвол <b>UFW</b> (открыты только порты <code>22</code>, <code>80</code>, <code>443</code>).
• <b>Nginx + Certbot (SSL):</b> «стойка ресепшена» на входе — выдаёт <b>HTTPS</b> (обязательно для Telegram <b>Webhooks</b>), проксирует через <code>proxy_pass</code> и пропускает <b>WebSocket</b> заголовками <code>Upgrade</code> и <code>Connection</code>.

—

🔗 <b>Интерактивный урок, пошаговый инспектор конфигов и симулятор сбоев:</b>
<a href="https://DmitryMita.github.io/ai-academy-lessons/m02-script-vs-system/">https://DmitryMita.github.io/ai-academy-lessons/m02-script-vs-system/</a>
🎧 <i>Внутри — подкаст наставника (64kbps, темп -7% с паузами) и 4 проверочных вопроса.</i>
