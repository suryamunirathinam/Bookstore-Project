# Bookstore-Project
Django for professtional Chapter 3


python3.7 -m pip install pip 
pip3.7 install pipenv
#To use 3.7 pipenv
pipenv --python 3.7
pipenv install django==2.2.7 psycopg2-binary==2.8.4
pipenv shell
django-admin startproject bookstore_project .
python manage.py runserver 
exit


# exit container 
touch Dockerfile
touch docker-compose.yml


#Dockerfile
FROM python:3.7

ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

WORKDIR /code

COPY Pipfile Pipfile.lock /code/
RUN pip install pipenv && pipenv install --system

COPY . /code/

#docker-compose.yml
version: "3.7"

services:
  web:
    build: .
    command: python /code/manage.py runserver 0.0.0.0:8000
    volumes:
      - .:/code
    ports:
      - 8000:8000
    depends_on:
      - db
  db:
    image: postgres:11
    volumes:
      - postgres_data:/var/lib/postgresql/data/
    environment:
      - "POSTGRES_HOST_AUTH_METHOD=trust"

volumes:
  postgres_data:

########
docker-compose up -d --build

##################
There are four steps for adding a custom user model to our project:
1. Create a CustomUser model
2. Update settings.py
3. Customize UserCreationForm and UserChangeForm
4. Add the custom user model to admin.py

