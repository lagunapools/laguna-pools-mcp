# Laguna Pools MCP Server

**AI-менеджер по продаже композитных бассейнов** — MCP сервер для интеграции с Claude Desktop, Cursor, ChatGPT и другими AI-ассистентами.

[![MCP](https://img.shields.io/badge/MCP-2025--03--26-blue)](https://modelcontextprotocol.io)
[![JSON-RPC](https://img.shields.io/badge/Protocol-JSON--RPC%202.0-green)](https://www.jsonrpc.org)
[![Tools](https://img.shields.io/badge/Tools-14-orange)](https://mcp.laguna-pools.ru/api/mcp/)
[![Resources](https://img.shields.io/badge/Resources-3-purple)](https://mcp.laguna-pools.ru/api/mcp/)
[![Prompts](https://img.shields.io/badge/Prompts-2-teal)](https://mcp.laguna-pools.ru/api/mcp/)

## Что это?

MCP (Model Context Protocol) сервер, который превращает AI-ассистента в профессионального менеджера по продаже бассейнов Laguna Pools. Архитекторы, дизайнеры и частные клиенты получают:

- **Подбор бассейна** по размерам участка, назначению, бюджету и климату
- **Расчёт комплектации «под ключ»** — бассейн + фильтрация + покрывало + камень + мебель
- **BIM/CAD файлы** для проектов — DWG, OBJ, RFA, 3DS
- **Поиск дилера** в 175 городах России
- **Отправка заявки** дилеру прямо из AI-чата

## Быстрый старт

### Claude Desktop

Добавьте в `claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "laguna-pools": {
      "url": "https://mcp.laguna-pools.ru/api/mcp/"
    }
  }
}
```

### Cursor

Settings → MCP → Add Server:
- **Type:** HTTP
- **URL:** `https://mcp.laguna-pools.ru/api/mcp/`

### Другие клиенты

Любой MCP-совместимый клиент может подключиться по URL:

```
https://mcp.laguna-pools.ru/api/mcp/
```

Протокол: JSON-RPC 2.0 over HTTP.

## Инструменты (14)

### AI-менеджер по продажам

| Инструмент | Описание |
|-----------|----------|
| `recommend_pool` | Подбор бассейна по параметрам: размер участка, назначение (семья/спорт/баня/СПА), бюджет, климат, количество людей |
| `calculate_total` | Калькулятор «под ключ»: бассейн + фильтр + покрывало + камень + мебель. Реальные цены |
| `submit_lead` | Отправка заявки дилеру. Клиент получит обратный звонок |

### Каталог бассейнов

| Инструмент | Описание |
|-----------|----------|
| `search_pools` | Поиск по размерам, бюджету, типу (бассейн/купель), климату |
| `get_pool_specs` | Характеристики модели: размеры, объём, вес, серии, гарантия 25 лет |
| `get_pool_price` | Цены серий PREMIUM и PREMIUM NORD |
| `get_bim_files` | BIM/CAD файлы: DWG (AutoCAD), OBJ (3D), RFA (Revit), 3DS |

### Продукция и сервис

| Инструмент | Описание |
|-----------|----------|
| `find_dealer` | Дилер в городе (175 городов России) |
| `get_repair_services` | Ремонт бассейнов, покрытия ecoFINISH |
| `get_furniture` | Композитная мебель: лежаки, лавочки, столешницы |
| `get_slides` | Горки и водопады |
| `get_filters` | Фильтрационные установки LPF (400–900 мм) |
| `get_accessories` | Покрывала, LagunaBox, Hot Tub |
| `list_tools` | Список всех инструментов |

## Примеры использования

### Подбор бассейна для архитектора

```
Пользователь: Проектирую загородный дом в Краснодаре.
Участок 12×8 метров, семья 4 человека.
Какой бассейн подойдёт?
```

AI вызовет `recommend_pool` с параметрами:
```json
{
  "area_length": 12,
  "area_width": 8,
  "city": "Краснодар",
  "purpose": "family",
  "people": 4
}
```

### Расчёт стоимости

```
Пользователь: Сколько будет стоить Laguna 7 с фильтрацией и покрывалом?
```

AI вызовет `calculate_total`:
```json
{
  "model": "laguna7",
  "series": "premium",
  "include_filter": true,
  "include_cover": true
}
```

### BIM файлы для проекта

```
Пользователь: Нужен DWG чертёж Laguna 8 для AutoCAD
```

AI вызовет `get_bim_files`:
```json
{
  "model": "laguna8"
}
```

## Модели бассейнов

| Модель | Размеры | Глубина | Объём | Тип |
|--------|---------|---------|-------|-----|
| Laguna 9 | 9.4 × 3.7 м | 1.1–1.8 м | 37.3 м³ | Бассейн |
| Laguna 8 | 8.2 × 3.65 м | 1.1–1.8 м | 32.7 м³ | Бассейн |
| Laguna 7 | 7.0 × 3.4 м | 1.1–1.7 м | 28.0 м³ | Бассейн |
| Laguna 6 | 6.2 × 3.25 м | 1.1–1.55 м | 19.6 м³ | Бассейн |
| Laguna 5 | 5.0 × 2.85 м | 1.05–1.5 м | 13.1 м³ | Бассейн |
| Laguna 4 | 4.0 × 2.6 м | 1.05–1.5 м | 14.0 м³ | Бассейн |
| Laguna 3 | 3.0 × 2.3 м | 1.0–1.5 м | 7.0 м³ | Купель |
| Laguna 2 | 2.0 × 1.65 м | 0.85 м | 5.8 м³ | Купель |

Две серии: **PREMIUM** (стандарт) и **PREMIUM NORD** (утепление Frozen Guard для холодного климата до -40°C).

## Ресурсы (Resources)

Сервер предоставляет 3 ресурса для чтения данных:

| URI | Описание |
|-----|----------|
| `laguna://catalog/pools` | Каталог всех моделей бассейнов (размеры, вес, объём) |
| `laguna://catalog/prices` | Прайс-лист на все товары из базы данных |
| `laguna://dealers` | Список дилеров с городами и контактами |

Шаблоны URI:
- `laguna://pool/{model}` — спецификация конкретной модели (laguna2..laguna9)
- `laguna://dealer/{city}` — дилер в конкретном городе

## Промпты (Prompts)

| Промпт | Описание |
|--------|----------|
| `recommend_pool` | Подбор бассейна: город, кол-во человек, назначение, бюджет |
| `calculate_project` | Расчёт проекта «под ключ»: модель, серия |

## Технические детали

- **Протокол:** JSON-RPC 2.0 (MCP 2025-03-26)
- **Версия сервера:** 2.1.0
- **Транспорт:** HTTP/HTTPS
- **Endpoint:** `https://mcp.laguna-pools.ru/api/mcp/`
- **Discovery:** `https://mcp.laguna-pools.ru/.well-known/mcp.json`
- **REST:** `https://mcp.laguna-pools.ru/api/mcp/?tool={name}&param=value`
- **Capabilities:** tools, resources, prompts, logging
- **Цены:** реальные, из базы данных, обновляются ежедневно
- **Дилеры:** 175 городов России

### Поддерживаемые MCP-методы

| Метод | Описание |
|-------|----------|
| `initialize` | Инициализация сервера, capabilities |
| `ping` | Проверка доступности |
| `notifications/initialized` | Подтверждение инициализации |
| `tools/list` | Список инструментов (14) |
| `tools/call` | Вызов инструмента |
| `resources/list` | Список ресурсов (3) |
| `resources/read` | Чтение ресурса по URI |
| `resources/templates/list` | Шаблоны URI |
| `prompts/list` | Список промптов (2) |
| `prompts/get` | Получение промпта с аргументами |
| `completion/complete` | Автодополнение |
| `logging/setLevel` | Уровень логирования |
| `roots/list` | Корневые URI |
| `shutdown` | Завершение |

## REST API

Помимо JSON-RPC, поддерживается простой REST:

```bash
# Поиск бассейнов до 7 метров
curl "https://mcp.laguna-pools.ru/api/mcp/?tool=search_pools&max_length=7&type=pool"

# Расчёт комплектации
curl "https://mcp.laguna-pools.ru/api/mcp/?tool=calculate_total&model=laguna7&include_filter=1&include_cover=1"

# Подбор для семьи в Москве
curl "https://mcp.laguna-pools.ru/api/mcp/?tool=recommend_pool&city=Москва&purpose=family&people=4"

# BIM файлы
curl "https://mcp.laguna-pools.ru/api/mcp/?tool=get_bim_files&model=laguna8"
```

## Контакты

- **Телефон:** 8 (800) 222-64-08 (бесплатно по России)
- **Сайт:** [laguna-pools.ru](https://laguna-pools.ru)
- **Email:** art-online-shop@yandex.ru
- **Для архитекторов:** [laguna-pools.ru/designer-architect](https://laguna-pools.ru/designer-architect)

## Лицензия

MIT
