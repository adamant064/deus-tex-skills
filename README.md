# Deus Tex — Skills Hub

Стандартизированные скиллы для ИИ-агентов. Формат **`.deus`**: манифест, права, совместимость, тесты, аудит.

**Живой хаб:** <https://api.deus-tex.ru/skills/index.json>

---

## Что это

Каждый скилл — самодостаточный JSON-манифест с процедурой. Агент читает манифест, видит **права** (`permissions`), **что требует подтверждения** (`execution_policy.human_confirmation`) и **чем проверялся** (`test_suite`). Никаких скрытых payload: код, если он есть, лежит рядом текстом.

## Формат

```json
{
  "name":            "example-skill",
  "summary":         "одна фраза — что делает",
  "version":         "1.0.0",
  "trust_level":     "public | restricted",
  "manifest":        { "inputs": [], "outputs": [] },
  "permissions":     { "filesystem": "", "network": "", "shell": "", "secrets": "" },
  "compatibility":   { "harness": [], "models": [], "os": [], "mcp": "" },
  "test_suite":      { "kind": "", "checks": [], "status": "" },
  "execution_policy":{ "human_confirmation": [] },
  "audit_trail":     { "author": "", "license": "", "sha256_16": "" },
  "endpoint":        "/skills/example-skill.json"
}
```

## Уровни доверия

| `trust_level` | Что значит |
|---|---|
| `public` | Общая практика. Ничего личного, ничего системного. |
| `restricted` | Касается инфраструктуры, файлов или личных данных. Читать права перед запуском. |

## Каталог

**19 скиллов.**

| Скилл | Доверие | Что делает |
|---|---|---|
| [`autonomous-continuation`](https://api.deus-tex.ru/skills/autonomous-continuation.json) | public | Метод: как агент действует самостоятельно, не спрашивая разрешения на внутреннее. Границы автономии, цикл execute-ver... |
| [`home-control`](https://api.deus-tex.ru/skills/home-control.json) | 🔒 restricted | Управление Home Assistant из агента без облака: включить/выключить устройства, узнать датчики, сказать голосом через ... |
| [`incremental-vector-index-build`](https://api.deus-tex.ru/skills/incremental-vector-index-build.json) | public | Инкрементальная индексация растущего локального корпуса в векторный индекс без полного пересчёта. |
| [`local-image-inspection`](https://api.deus-tex.ru/skills/local-image-inspection.json) | public | Локальный осмотр изображений: описание, чтение текста со скриншотов и ошибок — без облака. |
| [`local-voice-bridge`](https://api.deus-tex.ru/skills/local-voice-bridge.json) | public | Локальный мост распознавания речи: диагностика «микрофон не даёт текст», подключение STT. |
| [`managed-browser-profile-recovery`](https://api.deus-tex.ru/skills/managed-browser-profile-recovery.json) | public | Восстановление управляемого браузерного профиля: «профиль не запущен», потерянный логин, протухшие ссылки. |
| [`mcp-server-from-python-core`](https://api.deus-tex.ru/skills/mcp-server-from-python-core.json) | public | Обернуть существующее Python-приложение в локальный stdio MCP-сервер. |
| [`model-context-window`](https://api.deus-tex.ru/skills/model-context-window.json) | public | Настройка окна контекста модели и лимита активного ввода при давлении на CPU/RAM. |
| [`nvr-mcp-integration`](https://api.deus-tex.ru/skills/nvr-mcp-integration.json) | 🔒 restricted | Интеграция NVR с MCP: события камер, детекция объектов, диагностика «пишет, но не детектит». |
| [`openclaw-core-upgrade`](https://api.deus-tex.ru/skills/openclaw-core-upgrade.json) | public | Обновление ядра OpenClaw и починка неудавшегося или пропущенного апгрейда. |
| [`paired-node-command-execution`](https://api.deus-tex.ru/skills/paired-node-command-execution.json) | public | Выполнение shell-команды на спаренном узле (Windows/Linux/macOS) с гейтвея. |
| [`personal-messaging-access`](https://api.deus-tex.ru/skills/personal-messaging-access.json) | 🔒 restricted | Личный доступ к Telegram/email: развести бота и аккаунт, проверить scope, транспорт, отправку и приём. |
| [`preflight-inventory`](https://api.deus-tex.ru/skills/preflight-inventory.json) | public | Порядок проверки возможностей перед любой задачей: сначала готовые скиллы и инструменты, потом арсенал, и только зате... |
| [`scheduled-job-lifecycle`](https://api.deus-tex.ru/skills/scheduled-job-lifecycle.json) | public | Управление автоматизациями: heartbeat, cron, задачи «every» — создание, правка, удаление. |
| [`secret-exposure-audit`](https://api.deus-tex.ru/skills/secret-exposure-audit.json) | public | Аудит путей утечки учётных данных в дочерние процессы, конфиги и логи. Без раскрытия значений. |
| [`self-hosted-web-search-provider`](https://api.deus-tex.ru/skills/self-hosted-web-search-provider.json) | public | Свой поисковый провайдер вместо отказавшего web_search (429, квота, отключён). |
| [`session-context-cost-control`](https://api.deus-tex.ru/skills/session-context-cost-control.json) | public | Снижение расхода токенов: длинные сессии, раздутый контекст, дорогой tool-loop. |
| [`shared-host-routing-change`](https://api.deus-tex.ru/skills/shared-host-routing-change.json) | public | Изменение сетевой маршрутизации и реверс-прокси на хосте, где живут другие прод-сервисы. |
| [`virtualbox-vm-recovery`](https://api.deus-tex.ru/skills/virtualbox-vm-recovery.json) | public | Восстановление зависшей VirtualBox VM, не монтирующегося .vdi, headless-гостя без ответа. |

## Как использовать

```bash
# весь индекс
curl -s https://api.deus-tex.ru/skills/index.json

# один скилл
curl -s https://api.deus-tex.ru/skills/home-control.json
```

Или локально из этого репозитория: `skills/<name>.json`.

## Смежные проекты

- **[Frandex_VLM](https://github.com/adamant064/Frandex_VLM)** — движок индексации медиа и векторизации из эмбеддингов. Питает скилл [`incremental-vector-index-build`](skills/incremental-vector-index-build.json): тот описывает *процедуру* инкрементальной сборки индекса, Frandex — *рабочую реализацию*.

## Атрибуция

Автор: Gella / Quant Studio. Каждая запись несёт свою лицензию в `audit_trail.license`. Читать и применять — можно. Выдавать за своё — нет.
