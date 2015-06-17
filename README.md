## Getting Started

### Requirements

##### - python3.4

### Setup

##### Install dependencies

> pip install -r requirements

##### Install python applications

> python setup.py install

##### Run application in localhost:6543 with gunicorn

###### Development environment:

> gunicorn --paste development.ini

###### Production environment:

> gunicorn --paste production.ini

## Setting up DB connection and Alembic

## Deploy to Heroku
