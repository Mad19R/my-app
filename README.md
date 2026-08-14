# Analytics & Management API Documentation

Публичный демонстрационный проект системного и бизнес-аналитика. Проект представляет собой интерактивную документацию OpenAPI (Swagger UI), задеплоенную на GitHub Pages и интегрированную с действующим REST API и облачной релянционной базой данных PostgreSQL.

🔗 **Live Demo (Swagger UI):** [https://mad19r.github.io/my-app/](https://mad19r.github.io/my-app/)

---

## 📐 Архитектура системы


* **Frontend / Docs:** GitHub Pages, Swagger UI Dist.
* **Backend:** Python 3, FastAPI, Uvicorn, psycopg2. 
* **Database:** PostgreSQL (Neon Serverless DB). https://console.neon.tech/app/projects/small-breeze-79092907
* **Specification:** OpenAPI 3.0.3.

---

## 🗄️ Схема базы данных (ERD)

### Таблица `users`
| Поле | Тип | Ограничения | Описание |
| :--- | :--- | :--- | :--- |
| `id` | SERIAL | PRIMARY KEY | Уникальный ID пользователя |
| `name` | VARCHAR(100) | NOT NULL | Имя пользователя |
| `email` | VARCHAR(100) | UNIQUE, NOT NULL | Электронная почта |
| `created_at` | TIMESTAMP | DEFAULT CURRENT_TIMESTAMP | Дата создания |

### Таблица `products`
| Поле | Тип | Ограничения | Описание |
| :--- | :--- | :--- | :--- |
| `id` | SERIAL | PRIMARY KEY | Уникальный ID товара |
| `title` | VARCHAR(150) | NOT NULL | Название товара |
| `price` | NUMERIC(10,2) | CHECK >= 0 | Стоимость |
| `stock` | INT | DEFAULT 0 | Остаток на складе |

### Таблица `orders`
| Поле | Тип | Ограничения | Описание |
| :--- | :--- | :--- | :--- |
| `id` | SERIAL | PRIMARY KEY | Уникальный ID заказа |
| `user_id` | INT | FOREIGN KEY -> users(id) | ID покупателя |
| `product_id` | INT | FOREIGN KEY -> products(id) | ID товара |
| `quantity` | INT | CHECK > 0 | Количество |
| `status` | VARCHAR(50) | DEFAULT 'created' | Статус заказа |
| `created_at` | TIMESTAMP | DEFAULT CURRENT_TIMESTAMP | Дата заказа |

---

## 🚀 Функциональность API

* `GET /users` — Получение списка зарегистрированных пользователей.
* `POST /users` — Регистрация нового пользователя.
* `PUT /users/{id}` — Изменение профиля пользователя.
* `DELETE /users/{id}` — Удаление пользователя из базы данных.
* `GET /orders` — Извлечение агрегированных данных по заказам с расчетом суммы (SQL JOIN).
* `POST /orders` — Оформление нового заказа.



Демонстрационный проект системного и бизнес-аналитика. Проект представляет собой интерактивную документацию OpenAPI (Swagger UI), задеплоенную на GitHub Pages, с автоматизированным CI/CD тестированием (Newman), REST API на Python и облачной реляционной базой данных PostgreSQL.

🔗 **Live Demo (Swagger UI):** [https://mad19r.github.io/my-app/](https://mad19r.github.io/my-app/)  
⚙️ **Production API (Render):** `https://my-backend-534k.onrender.com`

---

````markdown
# E-Commerce Analytics & Management API Documentation

Демонстрационный проект системного и бизнес-аналитика. Проект представляет собой интерактивную документацию OpenAPI (Swagger UI), задеплоенную на GitHub Pages, с автоматизированным CI/CD тестированием (Newman), REST API на Python и облачной реляционной базой данных PostgreSQL.

🔗 **Live Demo (Swagger UI):** [https://mad19r.github.io/my-app/](https://mad19r.github.io/my-app/)  
⚙️ **Production API (Render):** `https://my-backend-534k.onrender.com`

---

## 📐 1. Архитектура системы (Sequence Diagram)

```mermaid
sequenceDiagram
    autonumber
    actor Client as Пользователь / Swagger UI
    participant GHP as GitHub Pages (Frontend)
    participant API as FastAPI (Render)
    participant DB as PostgreSQL (Neon)

    Note over Client, GHP: Загрузка документации
    Client->>GHP: Запрос страницы /my-app
    GHP-->>Client: Чтение openapi.yaml и отрисовка Swagger UI

    Note over Client, DB: Выполнение API запросов
    Client->>API: HTTP GET /orders
    API->>DB: SQL SELECT (JOIN users, products, orders)
    DB-->>API: Набор строк (Raw Data)
    API-->>Client: HTTP 200 OK (JSON Массив)

erDiagram
    USERS ||--o{ ORDERS : "places"
    PRODUCTS ||--o{ ORDERS : "included_in"

    USERS {
        int id PK "SERIAL"
        string name "VARCHAR(100)"
        string email "VARCHAR(100) UNIQUE"
        timestamp created_at "DEFAULT CURRENT_TIMESTAMP"
    }

    PRODUCTS {
        int id PK "SERIAL"
        string title "VARCHAR(150)"
        numeric price "NUMERIC(10,2)"
        int stock "DEFAULT 0"
    }

    ORDERS {
        int id PK "SERIAL"
        int user_id FK "REFERENCES users(id)"
        int product_id FK "REFERENCES products(id)"
        int quantity "CHECK > 0"
        string status "DEFAULT 'created'"
        timestamp created_at "DEFAULT CURRENT_TIMESTAMP"
    }
    ```
