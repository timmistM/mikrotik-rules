# mikrotik-rules

Централизованные правила маршрутизации для Clash Verge и MikroTik.

## Структура

```
mikrotik-rules/
├── rules/                  # Правила для rule-providers
│   ├── ai.yaml             # Claude, OpenAI, Gemini, Grok, Perplexity, Runway
│   ├── discord.yaml        # Discord + голосовые серверы
│   ├── telegram.yaml       # Telegram IP-диапазоны
│   ├── youtube.yaml        # YouTube + Google Video
│   ├── meta.yaml           # Facebook, Instagram, WhatsApp
│   ├── gaming.yaml         # Roblox, Unity, ARVI Playtests
│   └── other.yaml          # RuTracker, RustDesk, ProtonVPN, etc.
├── warp/                   # Shared WARP конфигурация
│   └── warp_proxies.yaml   # WARP-1, WARP-2, WARP-3
├── scripts/                # Автоматизация MikroTik
│   └── mikrotik_sync.rsc   # Скрипт синхронизации address-list
└── README.md
```

## Использование в Clash Verge

### Rule-providers (в конфиге клиента)

```yaml
rule-providers:
  ai-rules:
    type: http
    behavior: classical
    url: https://raw.githubusercontent.com/timmistM/mikrotik-rules/main/rules/ai.yaml
    path: ./ruleset/ai.yaml
    interval: 3600

rules:
  - RULE-SET,ai-rules,🤖 AI
```

### WARP proxy-provider

```yaml
proxy-providers:
  warp:
    type: http
    url: https://raw.githubusercontent.com/timmistM/mikrotik-rules/main/warp/warp_proxies.yaml
    path: ./providers/warp.yaml
    interval: 86400
    health-check:
      enable: true
      url: http://speed.cloudflare.com/
      interval: 300
```

## Обновление

Правила кешируются локально. Обновление происходит по `interval` (в секундах).
Рекомендуемые значения:
- `3600` (1 час) — для правил (rules)
- `86400` (24 часа) — для WARP прокси

**Скорость работы не страдает** — при загрузке сайтов Clash обращается к локальному кешу.

## Добавление нового сервиса

1. Добавить домены/IP в соответствующий файл в `rules/`
2. Commit + Push
3. Все клиенты подхватят при следующем обновлении по interval
