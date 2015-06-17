## Getting Started

### Requirements

 - python3.4

### Setup

 Install dependencies
```
 pip install -r requirements
```
 Install python applications
```
 python setup.py install
```
 Initialize db (ONLY FOR THE FIRST TIME, May need to setting up db connection first)
```
 initialize_thub_db development.ini
```
##### Run application in localhost:6543 with gunicorn

 Development environment:
```
 gunicorn --paste development.ini
```
 Production environment:
```
 gunicorn --paste production.ini
```

## Setting up DB connection and Alembic

 Setup your database and copy its url
 
 Change sqlalchemy.url in development.ini / production.ini / alembic.ini to that url
 
 For example:
 ```
 sqlalchemy.url = 'postgresql://scott:tiger@localhost:5432/mydatabase'
 ```
###### Environment variable 'DATABASE_URL' will override this setting, if environment variable is set, just leave sqlalchemy.url unchange (BUT DO NOT LEAVE IT BLANK)

  Do the db migration
  ```
  alembic upgrade head
  ```
## Deploy to Heroku

 Create an addon of heroku-postgresql
 ```
 heroku addons:create heroku-postgresql:hobby-dev
 ```
 Heroku will set the postgresql url path to environment variable 'DATABASE_URL'
 No need to change sqlalchemy.url in any .ini files
 
 Procfile:
 ```
 web: gunicorn --paste production.ini -b :${PORT}
 ```
 Do the db migration:
 ```
 heroku run alembic upgrade head
 ```
 
