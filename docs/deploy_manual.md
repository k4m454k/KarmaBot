# KarmaBot run without docker

* install python 3.9+

* create [virtual environment](https://docs.python.org/3/tutorial/venv.html)

* ```python -m pip install -r requirements.txt```

* create .env file with Environment variables or export that variables:
  * `KARMA_BOT_TOKEN` - api token for tg bot
  * fill `WEBHOOK_HOST`, `WEBHOOK_PORT`, `WEBHOOK_PATH`, `LISTEN_IP`, `LISTEN_PORT` if you need to run with webhook
  * DB_TYPE one of "sqlite", "postgres", "mysql"
  * if you are using sqlite you have to specify `DB_PATH`
  * in other case you need to specify `LOGIN_DB`, `PASSWORD_DB`, `DB_NAME`, `DB_HOST` (can skip, default is localhost), 
    `DB_PORT` (can skip, default is default port for a current db (example: 5432 for postgres))

* ```python -m app```

  * possible command line arguments:
    * -p - using polling instead webhook
    * -s - skip updates that accumulated on tg servers
    * -a - autoreload bot when source code changed. Use it only in development mode

* to create tables in database run:

```python initialize.py```

# Karmabot deploy manual with a docker:

* install docker and docker-compose

* Optional for webhook:

  * install https://github.com/bomzheg/nginx-le

  * add karmabot.conf to nginx-le bots path (etc/bots)
  
* create .env file with environment variables like in #KarmaBot run without docker
  

```docker-compose up --build -d```

* to  create tables in database run :

```docker-compose exec KarmaBot python initialize.py```


# The secondary setup:
in `app.config.__init__.py`:
* create chat in telegram and place it chat_id in 
[LOG_CHAT_ID](https://github.com/bomzheg/KarmaBot/blob/d5dcf3f6faead1b1b277143857ea9cdc6a872257/app/config.py#L48)
* on next line you can place same or another chat_id in `DUMP_CHAT_ID`
* to generate invite links, the bot must have administrator rights
* fill `SUPERUSERS` and `GLOBAL_ADMIN_ID` with yours
* you can change `PLUS_WORDS`, `PLUS_TRIGGERS`, `PLUS_EMOJI`, `MINUS`, `MINUS_EMOJI`. 
it must be iterable, better is set or frozenset
