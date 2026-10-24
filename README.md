# mikrotik-rules

Свои списки правил для Clash Verge (клиенты на ПК). Крупные списки (YouTube, Google, Meta,
Telegram, Discord, Roblox, Anthropic, OpenAI, Gemini) клиенты берут напрямую из
[MetaCubeX/meta-rules-dat](https://github.com/MetaCubeX/meta-rules-dat) — здесь только то,
чего там нет или что нужно дополнительно.

## Структура

```
mikrotik-rules/
├── rules/
│   ├── ai.yaml          # Claude/Anthropic (домены и IP), OpenAI, Grok, Ideogram, Perplexity, Runway, Intercom
│   ├── google_ai.yaml   # Gemini, AI Studio, NotebookLM, DeepMind
│   ├── discord.yaml     # Discord + диапазоны голоса/стримов
│   ├── telegram.yaml    # Telegram: домены и IP-диапазоны
│   ├── youtube.yaml     # YouTube
│   ├── meta.yaml        # Instagram, Facebook, WhatsApp
│   ├── gaming.yaml      # Roblox, Unity Remote Config, ARVI Playtests
│   └── other.yaml       # RuTracker, RustDesk, ProtonVPN, UPGEN SVN, Soundcore
└── README.md
```

## Использование в Clash Verge

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

Правила кешируются локально и обновляются по `interval` (секунды). На скорость не влияют:
при открытии сайтов Clash смотрит в локальный кеш.

## WARP

WARP здесь больше не раздаётся: у каждого пользователя свои учётки в его приватном конфиге.
Одна учётка WARP = одно устройство, иначе устройства выбивают друг друга.

## Добавление нового сервиса

1. Добавить домены/IP в нужный файл в `rules/`.
2. Commit + Push.
3. Клиенты подхватят при следующем обновлении (до часа).
