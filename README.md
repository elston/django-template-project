Шаблонный Postgres/python3/Django проект под vagrant

 1. Создание bootstrap.sh
- virtualenvwrapper (окружение посадить в /vagrant/.env):
- postgresql
    - БД  $PROJECT
    - user:  django
    - pass: django
- в /vagrant создать $PROJECT
    - settings.py:
        - LANGUAGE_CODE - 'ru-RU'
        - TIME_ZONE — 'Europe/Moscow'
        - настройки движка под созданную в постгресс БД
        - логи — в /vagrant/$PROJECT/logs/django.log
        - статика в /vagrant/$PROJECT/static/
        - templates в /vagrant/$PROJECT/templates/
        - настройки логов:
            LOGGING = {
                'version': 1,
                'disable_existing_loggers': False,
                'formatters': {
                    'standard': {
                        'format' : '[%(asctime)s] %(levelname)s [%(name)s:%(lineno)s] %(message)s',
                        'datefmt' : '%d/%b/%Y %H:%M:%S'
                    },
                    'simple': {
                        'format': '%(levelname)s %(message)s'
                    },
                },
                'filters': {
                    'require_debug_true': {
                        '()': 'django.utils.log.RequireDebugTrue',
                    },
                }, 
                'handlers': {
                    'console': {
                        'level': 'DEBUG',
                        'filters': ['require_debug_true'],
                        'class': 'logging.StreamHandler',
                        'formatter': 'simple'
                    },
                    'file': {
                        'level': 'DEBUG',
                        'class': 'logging.FileHandler',
                        'filename': LOG_FILE,
                    },
                },
                'loggers': {
                    'name_of_project': {
                        'handlers': ['console','file'],
                        'level': 'DEBUG',
                        'propagate': True,
                        'formatter': 'standard',
                    },
                },
            }



2. После создания нужно открыть админку и добавить несколько пользователей

3. На хост машине запустить скрипт и выгрузить пользователей в текстовый файл в json-формате в  /vagrant/$PROJECT/data/__d__$name_of_table.json

4. Проект оформить в виде mercurial репозитория на bitbucket, для  каммитов написать скрипт где на входе задается комментарий или ничего , в этом случае  подставляется  'this is a comment' .

5. Все изменения на хост-машине задокументировать в виде bash-скрипта.