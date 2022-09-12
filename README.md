# py-flask-app-smpl-redis-dbg Flask application. Debug додатку, що запущено в контейнері

В якосіт шаблона викорситано [ python-sample-vscode-flask-tutorial](https://github.com/microsoft/python-sample-vscode-flask-tutorial)


## Підготовка до запуску локально

- створити віртуальну environment

```bash
py -m venv env
```

- ЗАвантажити потрібні бібліотеки


```bash

py -m pip install -r requirements.txt

```



## Розроблені API

### Health check GET  /api/health

Використовується для перевірки працездатності сервісу

Повертає JSON

```json
{
  "success": true
}
```

### Отримати всі ключі в БД GET api/key

Повертає перелік всіх ключів в БД redis у вигляді масиву:

- Запит

   без параметрів

- Обов'язкові заголовки http в запиті

```text

    content-type: application/json

```

- Відповідь

```json
{
  "list": ["shhkey2", "shkey1", "APICALLS", "book1", "myhash", "jsondata", "get", "test1", "counter", "xcntr", "sh-book","gey"]
}

```

### Створити новий ключ та значення в БД POST api/key

- Запит

- Обов'язкові заголовки http в запиті

```text

    content-type: application/json


```json
{"keyname": "xkey1", "keyvalue": "xkeyvalue"}

```

- Успішна відповідь

```json
{
  "redis_result": true
}

```