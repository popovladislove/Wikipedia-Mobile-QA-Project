# Примеры request / response для Wikipedia Mobile QA Project

В этом документе приведены примеры запросов к публичному MediaWiki API, которые можно использовать для дополнительной валидации данных при тестировании Wikipedia Mobile.

---

## 1. Поиск статьи по запросу

### Request
**Method:** GET

```http
GET https://en.wikipedia.org/w/api.php?action=query&list=search&srsearch=Python&format=json
```

## Что проверяем
- API доступен
- поиск возвращает релевантные результаты
- статья по запросу существует
## Пример ожидаемого response
```json
{
  "batchcomplete": "",
  "query": {
    "searchinfo": {
      "totalhits": 12345
    },
    "search": [
      {
        "ns": 0,
        "title": "Python (programming language)",
        "pageid": 23862
      }
    ]
  }
}
```
## Что валидируем
- status code = 200
- query.search не пустой
- среди результатов есть статья Python (programming language)

# 2. Получение статьи по названию
## Request
**Method:** GET
```http
GET https://en.wikipedia.org/w/api.php?action=query&titles=Python_(programming_language)&format=json
```
## Что проверяем
- статья существует
- API возвращает данные страницы
## Пример ожидаемого response
```json
{
  "batchcomplete": "",
  "query": {
    "pages": {
      "23862": {
        "pageid": 23862,
        "ns": 0,
        "title": "Python (programming language)"
      }
    }
  }
}
```
## Что валидируем
- status code = 200
- в query.pages есть объект страницы
- title = Python (programming language)

# 3. Проверка языковых ссылок статьи
## Request
**Method:** GET
```http
GET https://en.wikipedia.org/w/api.php?action=query&prop=langlinks&titles=Python_(programming_language)&lllimit=10&format=json
```
## Что проверяем
- статья имеет альтернативные языковые версии
- можно валидировать наличие переводов

## Пример ожидаемого response
```json
{
  "batchcomplete": "",
  "query": {
    "pages": {
      "23862": {
        "pageid": 23862,
        "title": "Python (programming language)",
        "langlinks": [
          {
            "lang": "ru",
            "*": "Python"
          },
          {
            "lang": "de",
            "*": "Python"
          }
        ]
      }
    }
  }
}
```
## Что валидируем
- status code = 200
- присутствует массив langlinks
- есть как минимум одна альтернативная локализация

# 4. Проверка несуществующего запроса
## Request
**Method:** GET
```http
GET https://en.wikipedia.org/w/api.php?action=query&list=search&srsearch=asdasd_non_existing_query_123&format=json
```
## Что проверяем
- API корректно отвечает даже на несуществующий поисковый запрос
- результат поиска может быть пустым

## Пример ожидаемого response
```json
{
  "batchcomplete": "",
  "query": {
    "searchinfo": {
      "totalhits": 0
    },
    "search": []
  }
}
```
## Что валидируем
- status code = 200
- query.search может быть пустым
- API не падает и не возвращает некорректный формат
# 5. Проверка доступности API
## Request
**Method:** GET
```http
GET https://en.wikipedia.org/w/api.php?action=query&meta=siteinfo&format=json
```
## Что проверяем
- API доступен
- возвращаются общие сведения о сайте
## Пример ожидаемого response
```json
{
  "batchcomplete": "",
  "query": {
    "general": {
      "mainpage": "Main Page",
      "sitename": "Wikipedia"
    }
  }
}
```
## Что валидируем
- status code = 200
- присутствует объект general
- API доступен и отвечает корректно
