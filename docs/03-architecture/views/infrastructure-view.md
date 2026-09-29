# 14.4. Инфраструктурное представление

Инфраструктурное представление показывает основные инфраструктурные компоненты
системы.

На данном этапе архитектура не привязана к конкретному облачному провайдеру.

```mermaid
flowchart TB

    Users[Global Users]

    Users --> CDN[CDN / Edge]
    Users --> WAF[WAF / Load Balancer]

    WAF --> Gateway[API Gateway]

    subgraph Region[Cloud Region]

        Gateway --> Services[Application Services]

        Services --> Cache[Distributed Cache]
        Services --> DB[(Databases)]
        Services --> Broker[Event Broker]

        Broker --> Workers[Async Workers]

        Workers --> DB

        Services --> Storage[Object Storage]

    end

    Services --> Observability[Logs / Metrics / Tracing]

    Services --> External[External APIs / Devices]
```

# CDN / Edge

Может использоваться для:

- статических ресурсов;
- изображений;
- публичного контента;
- снижения задержки для глобальной аудитории.

---

# WAF / Load Balancer

Отвечает за:

- защиту внешнего периметра;
- распределение входящей нагрузки;
- маршрутизацию запросов.

---

# API Gateway

Предоставляет единую точку входа в backend API.

---

# Application Services

Содержат основные бизнес-компоненты платформы.

Компоненты должны иметь возможность масштабироваться независимо.

---

# Event Broker

Используется для асинхронного обмена событиями между компонентами.

---

# Distributed Cache

Используется для данных, которые:

- часто читаются;
- допускают кеширование;
- не требуют постоянного обращения к основному хранилищу.

Примеры:

- рейтинги;
- справочники;
- популярные группы.

---

# Object Storage

Может использоваться для хранения:

- изображений;
- больших объектов;
- пользовательских файлов;
- экспортированных данных.

---

# Observability

Система должна централизованно собирать:

- logs;
- metrics;
- traces;
- alerts.

---

# Региональное развёртывание

Так как приложение ориентировано на глобальную аудиторию, архитектура должна
допускать развёртывание компонентов в нескольких регионах.

```mermaid
flowchart TB

    Global[Global Routing]

    Global --> EU[EU Region]
    Global --> US[US Region]

    EU --> EUApp[Application Services]
    US --> USApp[Application Services]
```

Конкретный вариант:

- active-active;
- active-passive;
- разделение данных по регионам;

должен определяться отдельным ADR после появления количественных требований
по нагрузке и доступности.