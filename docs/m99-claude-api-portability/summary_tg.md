🛡️ <b>Модуль M99 (PRO): Защита от блокировок, миграция истории и Claude через API</b>

Когда все инструкции (<i>Projects</i>) и история решений заперты внутри <code>claude.ai</code>, любой бан аккаунта превращается в потерю рабочего контекста (<i>Single Point of Failure</i>).

—

📦 <b>1. Подготовка к блокировке и перенос истории (<code>conversations.json</code>)</b>
• Экспорт в Клоде: <code>Settings → Privacy → Export data</code> → файл <code>conversations.json</code>.
• Прямого импорта этого JSON нет ни в ChatGPT, ни в Google Gemini.
• <b>Рабочие пути миграции:</b>
  - <b>Open WebUI / LibreChat (self-hosted):</b> конвертация через Python-скрипт (<code>openwebui-importer</code>) в дерево <code>parentId</code>/<code>childrenIds</code> — переносит ветки диалогов целиком.
  - <b>Gemini / NotebookLM / ChatGPT:</b> конвертация <code>conversations.json → Markdown (.md)</code> и загрузка как базы знаний.
• <b>Золотое правило:</b> «Own Your Context» — держите регламенты и ключевые ТЗ в локальных <code>.md</code>-файлах (Git / Antigravity), а не только в облачных проектах.

—

🌐 <b>2. Claude API в неподдерживаемых странах: пути и риски</b>
• Политика <i>Supported Regions</i> едина для <code>claude.ai</code>, <code>Claude Code</code> и <code>Console API</code> (физическое нахождение, юрлицо и контроль ≥50%).
• <b>Прямой Console (<code>api.anthropic.com</code>):</b> заголовки <code>x-api-key</code> и <code>anthropic-version</code>, все фичи с первого дня (Prompt Caching, Batches -50%), но при регистрации из неподдерживаемой страны остается риск бана и заморозки депозита.
• <b>API Gateway (OpenRouter / LiteLLM):</b> единый OpenAI-совместимый формат, проброс <code>cache_control</code> и авто-Fallback на Gemini/GPT при ошибке <code>429</code>.
• <b>Облака (AWS Bedrock / GCP Vertex AI):</b> корпоративный Data Residency и IAM-биллинг, но часть новых фич API (Files API, Batches) появляется позже.

—

⚖️ <b>3. Ограничения API vs подписка Claude.ai Pro ($20/мес)</b>
• <b>Stateless:</b> API не помнит диалог — вы обязаны слать историю <code>messages</code> на каждом шаге (без <b>Prompt Caching</b> это в разы дороже подписки!).
• <b>Нет GUI-фич:</b> нет <i>Projects</i>, <i>Memory</i> и <i>Artifacts</i>.
• <b>Лимиты:</b> вместо 5-часовых окон действуют тройные лимиты <b>RPM / ITPM / OTPM</b> + алгоритм Token Bucket (всплеск запросов дает <code>429</code>).
• <b>Безопасность:</b> ставьте жесткий <b>Spend Limit</b> на ключ, иначе баг в цикле агента сожжет баланс за минуты.

—

🔗 <b>Интерактивный урок, схемы и калькулятор:</b>
<a href="https://DmitryMita.github.io/ai-academy-lessons/m99-claude-api-portability/">https://DmitryMita.github.io/ai-academy-lessons/m99-claude-api-portability/</a>
🎧 <i>Внутри — подкаст наставника (64kbps, темп -15%) и тест для самопроверки.</i>
