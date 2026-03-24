# API тест-кейсы

Для валидации данных используются публичные endpoints экосистемы MediaWiki / Wikimedia.

## API-TC-001
**Название:** Поиск статьи по запросу  
**Метод:** GET  
**Endpoint:** /w/api.php?action=query&list=search&srsearch=Python&format=json

**Ожидаемый результат:**
- статус-код 200;
- в ответе присутствует список статей;
- в выдаче есть релевантные результаты по запросу Python.

---

## API-TC-002
**Название:** Получение информации о статье по названию  
**Метод:** GET  
**Endpoint:** /w/api.php?action=query&titles=Python_(programming_language)&format=json

**Ожидаемый результат:**
- статус-код 200;
- статья существует;
- в ответе есть pageid или данные страницы.

---

## API-TC-003
**Название:** Проверка существования языковой версии статьи  
**Метод:** GET  
**Endpoint:** /w/api.php?action=query&prop=langlinks&titles=Python_(programming_language)&lllimit=10&format=json

**Ожидаемый результат:**
- статус-код 200;
- в ответе присутствуют языковые ссылки;
- у статьи есть альтернативные языковые версии.

---

## API-TC-004
**Название:** Проверка ответа на несуществующий запрос  
**Метод:** GET  
**Endpoint:** /w/api.php?action=query&list=search&srsearch=asdasd_non_existing_query_123&format=json

**Ожидаемый результат:**
- статус-код 200;
- ответ возвращается в корректном формате;
- список результатов пуст или содержит 0 релевантных совпадений.

---

## API-TC-005
**Название:** Проверка доступности API  
**Метод:** GET  
**Endpoint:** /w/api.php?action=query&meta=siteinfo&format=json

**Ожидаемый результат:**
- статус-код 200;
- API доступен;
- возвращаются базовые данные о сайте.

---

## API-TC-006
**Название:** Проверка корректной обработки article title в запросе  
**Метод:** GET  
**Endpoint:** /w/api.php?action=query&titles=Python_(programming_language)&format=json

**Ожидаемый результат:**
- статус-код 200;
- статья определяется корректно;
- title совпадает с ожидаемым значением.
