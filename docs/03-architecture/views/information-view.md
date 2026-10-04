# 14.2. Информационное представление

Информационное представление описывает основные информационные сущности системы
и отношения между ними.

Это концептуальная информационная модель, а не физическая схема базы данных.
Связи между сущностями не подразумевают общие таблицы или междоменные SQL-запросы.

```mermaid
erDiagram

    USER ||--o{ TRAINING : performs
    USER ||--o{ EQUIPMENT : owns
    USER ||--o{ TRAINING_PLAN : has
    USER ||--o{ DEVICE_CONNECTION : connects
    USER ||--o{ GROUP_MEMBERSHIP : has
    GROUP ||--o{ GROUP_MEMBERSHIP : contains
    USER }o--o{ CHALLENGE : participates

    TRAINING ||--o{ TRAINING_METRIC : contains
    TRAINING ||--o| ROUTE : has

    CHALLENGE ||--o{ CHALLENGE_RESULT : contains
    USER ||--o{ CHALLENGE_RESULT : produces

    USER ||--o{ ACHIEVEMENT : earns
    USER ||--o{ NOTIFICATION : receives
    USER ||--o{ RECOMMENDATION : receives
    PROMOTION }o--o{ REGION : targets
```

# Основные сущности

## User

Основная информация:

- UserId;
- профиль;
- спортивные интересы;
- регион;
- privacy settings.

---

## Training

Основная информация:

- TrainingId;
- UserId;
- SportType;
- StartTime;
- EndTime;
- Distance;
- Status.

---

## TrainingMetric

Хранит отдельные показатели тренировки.

Примеры:

- heart rate;
- speed;
- oxygen;
- cadence.

Основная информация:

- Timestamp;
- MetricType;
- Value;
- Source.

---

## Route

Содержит информацию о маршруте тренировки.

Маршрут и географические точки рассматриваются как чувствительная
пользовательская информация.

---

## Equipment

Основная информация:

- EquipmentId;
- Type;
- Model;
- PurchaseDate;
- Usage.

---

## Challenge

Основная информация:

- ChallengeId;
- Rules;
- Period;
- Region;
- Participants.

---

## TrainingPlan

Содержит план тренировок пользователя:

- TrainingPlanId;
- UserId;
- цели и виды спорта;
- расписание;
- статус плана.

Владелец — Training Planning.

---

## DeviceConnection

Описывает подключение пользователя к устройству или внешнему источнику:

- DeviceConnectionId;
- UserId;
- поставщик и идентификатор источника;
- предоставленные разрешения;
- состояние подключения и синхронизации.

Владелец — Integration Layer. Секреты подключения не раскрываются в информационной модели.

---

## GroupMembership

Явно представляет участие пользователя в группе:

- UserId;
- GroupId;
- роль;
- статус участия.

Владелец — Social & Groups.

---

## Promotion

Описывает промо или контентное предложение:

- PromotionId;
- содержание;
- период доступности;
- региональный и спортивный targeting context.

Связь с Region концептуально задаёт регионы показа. Другие условия targeting
не детализируются в отдельные сущности. Владелец — Promotions.

---

## Region

Региональный контекст для пользователя, соревнования и правил показа промо.
Конкретная детализация регионов и правил определяется при выходе на новые рынки.

---

# Владение данными

Каждая доменная область является владельцем своих данных.

```text
Profile          -> User data
Training         -> Training data
Social           -> Social graph
Social           -> Group memberships
Gamification     -> Challenges / Achievements
Planning         -> Training plans
Integration Layer -> Device connections
Equipment        -> Equipment data
Promotions       -> Campaigns
```

Компоненты не должны напрямую обращаться к хранилищам данных других доменных
областей.

Обмен информацией выполняется через:

- API;
- доменные события.
