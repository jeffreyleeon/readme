## Getting Started

### Requirements

 - python3.4

### Config

####Environment Variables

 - DATABASE_URL
 
 In development.ini / production.ini / alembic.ini, set followings
 ```
github_client_id =
github_secret_id =
github_redirect_uri =

trello_api_key =
trello_api_secret =
trello_redirect_uri =
 ```
 
### Setup

 Install dependencies
```
 pip install -r requirements
```
 Install python applications
```
 python setup.py install
```
 Initialize db (ONLY FOR THE FIRST TIME, May need to setting up db connection
 first)
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
 
 Change `sqlalchemy.url` in development.ini / production.ini / alembic.ini to 
 that url
 
 Run `createdb thub` for development env if you are using postgresql


###### Environment variable `DATABASE_URL` will override the `sqlalchemy.url`.

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
