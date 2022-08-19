```
sudo nano Dockerfile
```
```
FROM python:3.8

ENV PYTHONUNBUFFERED 1

WORKDIR /home/ubuntu/new_tut

COPY . .

RUN python -m pip install --upgrade pip setuptools wheel

RUN pip install -r req.txt

```

```
sudo nano docker-compose.yml
```
```
version: "3.8"

services:
  db:
    image: postgres
    volumes:
      - ./data/db:/var/lib/postgresql/data
    environment:
      - POSTGRES_DB=postgres1
      - POSTGRES_USER=postgres1 
      - POSTGRES_PASSWORD=postgres1
  web: 
    build: .
    command: python3 manage.py runserver 0.0.0.0:8000
    volumes:
      - .:/code
    ports:
      - "8000:8000"
    depends_on:
      - db 
```
> in settings.py
```
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'postgres1',
        'USER': 'postgres1',
        'PASSWORD': 'postgres1',
        'HOST': 'db',
        'PORT': 5432
    }
}

```
```
sudo apt-get install nginx
```
```
sudo ufw allow 80
```
```
sudo ufw allow 8000
```
---
```
docker-compose up -d
```
```
docker-compose run web python3 manage.py makemigrations
```
```
docker-compose run web python3 manage.py migrate
```
```
docker-compose run web python3 manage.py collectstatic
```
```
docker-compose run web python3 manage.py createsuperuser
```

```
docker-compose up -d --build
```
[link](https://www.youtube.com/watch?v=jyapP2Yy0AQ)
### :bulb: Update application in docker container
[n](https://stackoverflow.com/questions/47854463/docker-got-permission-denied-while-trying-to-connect-to-the-docker-daemon-socke)
