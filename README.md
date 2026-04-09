# SHIFT Lab — Тестовое задание Back-End (CRM-система)

## Описание
Упрощённая CRM-система для управления продавцами и их транзакциями с функциями аналитики.

## Реализованная функциональность
- Полный CRUD для сущностей **Seller** и **Transaction**
- Soft delete (сохранение историчности данных)
- Аналитика:
  - Самый продуктивный продавец за любой период (день, месяц, квартал, год)
  - Список продавцов, у которых сумма всех транзакций за выбранный период меньше указанной суммы
  - **Сложная задача** — определение лучшего периода для продавца (диапазон с максимальным количеством транзакций)

## Технологии
- Java 17
- Spring Boot 3.3.4
- Spring Data JPA + Hibernate
- H2 Database (in-memory) / PostgreSQL
- Gradle
- Lombok
- JUnit 5 + Mockito

## Запуск проекта

```bash
./gradlew clean bootRun
```

Приложение доступно по адресу: **http://localhost:8080**

H2 Console: [http://localhost:8080/h2-console](http://localhost:8080/h2-console)  
(JDBC URL: `jdbc:h2:mem:testdb`, User: `sa`, Password: пусто)

## API

**Продавцы**
- `GET    /api/sellers`
- `GET    /api/sellers/{id}`
- `POST   /api/sellers`
- `PUT    /api/sellers/{id}`
- `DELETE /api/sellers/{id}`

**Транзакции**
- `GET    /api/transactions`
- `GET    /api/transactions/{id}`
- `POST   /api/transactions`
- `GET    /api/transactions/seller/{sellerId}`

**Аналитика**
- `GET /api/analytics/most-productive?start=YYYY-MM-DDTHH:mm:ss&end=YYYY-MM-DDTHH:mm:ss`
- `GET /api/analytics/sellers-below-sum?start=...&end=...&threshold=...`
- `GET /api/analytics/seller/{sellerId}/best-period`

## Тестирование

```bash
./gradlew test
```

Все тесты проходят успешно (покрытие критической логики > 60%).

## Структура проекта
- `entity/` — JPA-сущности
- `repository/` — репозитории
- `service/` — бизнес-логика и аналитика
- `controller/` — REST-контроллеры
- `dto/` — DTO
- `exception/` — обработка ошибок
