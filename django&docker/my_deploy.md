```
sudo nano Dockerfile
```

```
FROM python:3.8

ENV PYTHONUNBUFFERED 1

WORKDIR /path/

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
      - ./data
    environment:
      - POSTGRES_DB=postgres21
      - POSTGRES_USER=postgres21
      - POSTGRES_PASSWORD=postgres21
  web: 
    build: .
    command: python3 manage.py runserver 0.0.0.0:8000
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
        'NAME': 'postgres21',
        'USER': 'postgres21',
        'PASSWORD': 'postgres21',
        'HOST': 'db',
        'PORT': 5432
    }
}

```

```
sudo ufw allow 80
```

```
sudo ufw allow 8000
```

> pipeline

```
name: build-project-time

on:
  push:
    branches: [ "main" ]
  pull_request:
    branches: [ "main" ]


jobs:
  build:
    runs-on: self-hosted

    steps:
 
      - uses: actions/checkout@v2
    
#       - name: Stop backend_web_1 container
#         run: | 
#             docker stop backend_web_1
          
#       - name: Delete backend_web_1 container
#         run: |
#           docker rm backend_web_1
          
      - name: Run Docker-Compose
        run: |
          docker-compose up --build -d
          
      - name: Makemigrations
        run: |
          docker-compose run web python3 manage.py makemigrations
          
      - name: Migrate
        run: |
          docker-compose run web python3 manage.py migrate
          
      - name: Collectstatic
        run: |
          docker-compose run web python3 manage.py collectstatic --noinput
          
          

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

---
```
sudo groupadd chmod
```
```
su - ${USER}
```
```
sudo usermod -aG chmod devops
```
