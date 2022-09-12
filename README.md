# py-flask-app-smpl-redis
Flask app та його взаємодія з redis

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

##  Запуск локально в developent mode при наявності redis  на laptop

- Створити env variable в terminal VSC

    * PowerShell
```bash
$env:FLASK_APP="hello_app.webapp"
$env:RDS_HOST="redis-host"
$env:RDS_PORT=6379
$env:RDS_PSW="22"



$env:FLASK_APP

```

    * CMD
```bash
SET FLASK_APP=hello_app.webapp
SET RDS_HOST=redis-host
SET RDS_PORT=6379
SET RDS_PSW=22
ECHO %FLASK_APP%

```

Для запуска в режимі debug  налаштувати  **.vscode/launch.json**


```json
      {
            "name": "Python: Flask",
            "type": "python",
            "request": "launch",
            "module": "flask",
            "env": {
                "FLASK_APP": "hello_app.webapp",
                "FLASK_ENV": "development",
                "FLASK_DEBUG": "0",
                "RDS_HOST": "redis-host",
                "RDS_PORT": 6379,
                "RDS_PSW": "22"
            },
            "args": [
                "run",
                "--no-debugger",
                "--no-reload"

            ],
            "jinja": true
        }

```


- Запуск в режимі development

```bash
python -m flask run
```

- Запуск в режимі DEBUG

 Запуск описано за лінком: [Створення найпростішого скрипта для flask app та запуск applicaiton з індивідуальн ою назвою в режимі DEBUG](https://pavlo-shcherbukha.github.io/posts/2022-09-02/python-flask-1/#p-6).


Сервіс стартує локально за адресою: http://localhost:5000

Rest API  доступне  за адресою: http://localhost:5000/api


- Запук за допомгою docker-compose

Склонувати репозиторій на локальну станцію командою git clone
При бажанні відкоригувати параметри в **docker-compose.yaml**.
Запустити cmd **sh-composer-up.cmd** або виконати команду: 

```text
docker compose up --build smplapp-srvc-redis
```

Сервіс стартує локально за адресою: http://localhost:8081

Rest API  доступне  за адресою: http://localhost:8081/api


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