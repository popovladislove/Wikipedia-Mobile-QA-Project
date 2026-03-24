# Примеры request / response для Wikipedia Mobile QA Project

В этом документе приведены примеры запросов к публичному MediaWiki API, которые можно использовать для дополнительной валидации данных при тестировании Wikipedia Mobile.

---

## 1. Поиск статьи по запросу

### Request
**Method:** GET

```http
GET https://en.wikipedia.org/w/api.php?action=query&list=search&srsearch=Python&format=json
```

# Что проверяем
- API доступен
- поиск возвращает релевантные результаты
- статья по запросу существует
# Пример ожидаемого response
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
# Что валидируем
- status code = 200
- query.search не пустой
- среди результатов есть статья Python (programming language)

# 2. Получение статьи по названию
## Request
**Method:** GET

GET https://en.wikipedia.org/w/api.php?action=query&titles=Python_(programming_language)&format=json

Что проверяем
статья существует
API возвращает данные страницы
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
