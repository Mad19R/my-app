openapi: 3.0.0
info:
  title: API Сервиса Пользователей
  description: Учебная спецификация API для демонстрации на GitHub Pages
  version: 1.0.0
paths:
  /users:
    get:
      summary: Получить список пользователей
      responses:
        '200':
          description: Успешный ответ со списком
  /users/{id}:
    get:
      summary: Получить информацию о пользователе по ID
      parameters:
        - name: id
          in: path
          required: true
          schema:
            type: integer
      responses:
        '200':
          description: Данные пользователя найдена
        '404':
          description: Пользователь не найден
