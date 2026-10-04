# 14.1. Функциональное представление

Функциональное представление показывает основные функциональные части системы
и ответственность каждой из них.

```mermaid
flowchart LR

    App[Mobile App] --> API[API Gateway]

    API --> User[Identity & Profile]
    API --> Training[Training]
    API --> Social[Social & Groups]
    API --> Game[Challenges & Gamification]
    API --> Planning[Training Planning]
    API --> Equipment[Equipment]
    API --> Promo[Promotions]

    Training -->|TrainingCompleted via Outbox| Bus[Event Bus]
    Bus -->|TrainingCompleted| Analytics[Analytics]
    Bus -->|TrainingCompleted| Game
    Bus -->|TrainingCompleted| Recommendations[Recommendations]
    Game -->|AchievementEarned| Bus
    Bus -->|AchievementEarned| Notify[Notifications]
    Analytics --> Recommendations
    Equipment --> Recommendations
    Recommendations --> Planning
    Recommendations --> Promo

    External[External Systems]
        --> Integrations[Integration Layer]

    Integrations --> Training
    Integrations --> Promo
```

Диаграмма показывает логические доменные границы целевой архитектуры.
Training сохраняет тренировку и Outbox Event в одной транзакции; событие
публикуется через Outbox Publisher (ADR-014). Ответ пользователю не зависит
от вторичных consumers. Event Bus и Event Broker обозначают один механизм
асинхронного обмена событиями во всех представлениях.

## Identity & Profile

Отвечает за:

- профиль пользователя;
- настройки;
- спортивные интересы;
- настройки приватности.

## Training

Отвечает за:

- регистрацию тренировок;
- историю тренировок;
- основные спортивные показатели;
- маршруты.

## Social

Отвечает за:

- друзей;
- группы;
- поиск спортсменов;
- совместные активности.

## Gamification

Отвечает за:

- достижения;
- соревнования;
- челленджи;
- рейтинги.

## Analytics

Отвечает за:

- статистику;
- агрегированные показатели;
- сравнение результатов;
- прогресс пользователя.

## Recommendations

Отвечает за персонализацию и рекомендации.

## Planning

Отвечает за планы и расписание тренировок.

## Equipment

Отвечает за спортивный инвентарь пользователя.

## Promotions

Отвечает за:

- новости;
- акции;
- региональные предложения.

## Notifications

Отвечает за отправку уведомлений, включая уведомления о достижениях по
`AchievementEarned` от Gamification, с учётом пользовательских настроек приватности.

## Integration Layer

Отвечает за интеграцию с:

- спортивными устройствами;
- фитнес-функциями мобильных платформ;
- существующими приложениями компании.
