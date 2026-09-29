# 11. Список ADR

В данном разделе хранятся Architecture Decision Records (ADR) — документы,
фиксирующие существенные архитектурные решения проекта.

Каждый ADR содержит контекст возникновения решения, выбранный вариант,
рассмотренные альтернативы и последствия принятого решения.

## Список ADR

| ADR | Решение | Статус |
|---|---|---|
| [ADR-001](ADR-001-architecture-style.md) | Выбор доменно-ориентированной сервисной архитектуры | Accepted |
| [ADR-002](ADR-002-event-driven.md) | Использование event-driven взаимодействия | Accepted |
| [ADR-003](ADR-003-synchronous-api.md) | Использование синхронного API для пользовательских запросов | Accepted |
| [ADR-004](ADR-004-api-gateway.md) | API Gateway как единая точка входа | Accepted |
| [ADR-005](ADR-005-offline-first.md) | Offline-first регистрация тренировок | Accepted |
| [ADR-006](ADR-006-domain-data-ownership.md) | Владение данными соответствующим бизнес-компонентом | Accepted |
| [ADR-007](ADR-007-integration-layer.md) | Выделение интеграционного слоя | Accepted |
| [ADR-008](ADR-008-async-processing.md) | Асинхронная обработка аналитики, достижений и уведомлений | Accepted |
| [ADR-009](ADR-009-geospatial-search.md) | Отдельный механизм географического поиска пользователей | Proposed |
| [ADR-010](ADR-010-location-data-privacy.md) | Защита геолокационных данных и управление согласием | Accepted |
| [ADR-011](ADR-011-regional-deployment.md) | Региональное развёртывание системы | Proposed |
| [ADR-012](ADR-012-cdn.md) | Использование CDN | Proposed |
| [ADR-013](ADR-013-observability.md) | Централизованные логи, метрики и distributed tracing | Accepted |

## Статусы

- `Proposed` — решение рассматривается.
- `Accepted` — решение принято.
- `Deprecated` — решение больше не рекомендуется.
- `Superseded` — решение заменено другим ADR.