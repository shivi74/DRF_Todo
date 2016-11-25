### Create the project directory or clone the code
    mkdir drf_todo
    cd drf_todo
or
    clone this repository

### Create a virtualenv to isolate our package dependencies locally
    virtualenv env
    source env/bin/activate  # On Windows use `env\Scripts\activate`

### Install Dependencies into the virtualenv
    pip install django
    pip install djangorestframework
    pip install psycopg2 # Because we are using postgres as database

### Set up a new project with a single application
> Note: This would be there if you've cloned the code
    django-admin.py startproject todo .  # Note the trailing '.' character
    django-admin.py startapp api

### Create a database into Postgres
    sudo -u postgres psql
    create database todo;

### Changes in settings
```python
INSTALLED_APPS = (
    ...
    'rest_framework',
    'api'
)

REST_FRAMEWORK = {
    'DEFAULT_PERMISSION_CLASSES': ('rest_framework.permissions.IsAdminUser',),
    'PAGE_SIZE': 10
}
```

### Initial migrations in database
    python manage.py migrate

### Making your API
1. Create task model (api/models.py)
2. Create model serializer (api/serializers.py)
3. Create list and detail view for task (api/tasks.py)
4. Create api urls (api/urls.py)
5. Modify project urls to import api urls (drf_tofo/urls.py)

### Create and apply migrations
    python manage.py makemigrations
    python manage.py migrate

### Run your localhost server
    python manage.py runserver

### Curl commands to perform API operations
    curl http://localhost:9000/api/tasks/
    curl -X POST http://localhost:9000/api/tasks/ -d "title=hello world&description=a whole new world"
    curl -X PUT http://localhost:9000/api/tasks/1 -d "title=hello world&description=be nice"
    curl -X PUT http://localhost:9000/api/tasks/1 -d "title=hello world&description=be nice&completed=True"
    curl -X DELETE http://localhost:9000/api/tasks/1
