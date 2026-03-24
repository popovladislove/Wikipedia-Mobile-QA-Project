# Примеры request / response для Wikipedia Mobile QA Project

В этом документе приведены примеры запросов к публичному MediaWiki API, которые можно использовать для дополнительной валидации данных при тестировании Wikipedia Mobile.

---

## 1. Поиск статьи по запросу

### Request
**Method:** GET

```http
GET https://en.wikipedia.org/w/api.php?action=query&list=search&srsearch=Python&format=json
