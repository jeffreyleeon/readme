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
 ###### Environment variable 'DATABASE_URL' will override this setting, if environment variable is set, just leave sqlalchemy.url unchange (DO NOT LEAVE IT BLANK)


## Deploy to Heroku
