[![Tests](https://github.com/tokarevsas31/ml_fastapi_tests/actions/workflows/python-app.yml/badge.svg)](https://github.com/tokarevsas31/ml_fastapi_tests/actions/workflows/python-app.yml)

# Документация для кода Sentiment Analysis API

## Описание

Данный код представляет собой веб-приложение FastAPI для анализа тональности текста. Он использует предобученную модель трансформера для классификации текста на положительный или отрицательный.

## Зависимости

- fastapi: Веб-фреймворк для создания API.
- transformers: Библиотека для работы с предобученными моделями трансформеров.
- pydantic: Библиотека для валидации данных и сериализации моделей.
- typing: Модуль для поддержки аннотаций типов.

## Модели данных

### Item

Модель данных для представления единичного текста.

- text (str): Текст для анализа тональности.

### BatchItem

Модель данных для представления пакета текстов.

- texts (List[str]): Список текстов для анализа тональности.

## Маршруты API

### GET /

Возвращает приветственное сообщение.

- Возвращает:
  - message (str): Приветственное сообщение.

### POST /predict/

Выполняет анализ тональности для единичного текста.

- Параметры запроса:
  - item (Item): Текст для анализа тональности.
- Возвращает:
  - text (str): Анализируемый текст.
  - sentiment (str): Метка тональности ("POSITIVE" или "NEGATIVE").
  - score (float): Оценка уверенности модели (от 0 до 1).

### GET /predict/

Выполняет анализ тональности для текста, переданного через параметр запроса.

- Параметры запроса:
  - text (str): Текст для анализа тональности (обязательный, минимальная длина: 1).
- Возвращает:
  - text (str): Анализируемый текст.
  - sentiment (str): Метка тональности ("POSITIVE" или "NEGATIVE").
  - score (float): Оценка уверенности модели (от 0 до 1).


### POST /predict_batch/

Выполняет анализ тональности для пакета текстов.

- Параметры запроса:
  - item (BatchItem): Список текстов для анализа тональности.
- Возвращает:
  - Список результатов анализа тональности для каждого текста:
    - text (str): Анализируемый текст.
    - sentiment (str): Метка тональности ("POSITIVE" или "NEGATIVE").
    - score (float): Оценка уверенности модели (от 0 до 1).


### GET /health/

Проверяет состояние работоспособности приложения.

- Возвращает:
  - status (str): Статус работоспособности ("OK").

## Использование

1. Установите зависимости: fastapi, transformers, pydantic.
2. Запустите приложение с помощью команды uvicorn main:app --reload.
3. Откройте веб-браузер и перейдите по адресу http://localhost:8000/docs для просмотра интерактивной документации API.
4. Используйте соответствующие маршруты для анализа тональности текста.

Пример запроса для анализа тональности единичного текста:

POST /predict/
```json
{
  "text": "I love this product!"
}
```

Пример ответа:
```json
{
  "text": "I love this product!",
  "sentiment": "POSITIVE",
  "score": 0.9875
}
```


