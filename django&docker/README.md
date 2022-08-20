# Online-Recording-System
```
sudo apt update -y
sudo apt upgrade -y
```
```
sudo apt install python3-pip python3-dev libpq-dev postgresql postgresql-contrib nginx curl file
```
---
> ### virtual environment
```
sudo apt-get install python3-pip
```
```
sudo -H pip3 install virtualenv 
```
```
virtualenv venv 
```
```
virtualenv -p /usr/bin/python3.8 venv
```
```
source venv/bin/activate
```
```
pip install django gunicorn psycopg2-binary pillow
```
> *in settings.py*
```
STATIC_ROOT = BASE_DIR / 'static'
```
___
```
sudo chmod +x manage.py
```
```
vi manage.py
```
> SHIFT + ;    -> set ff=unix   ->  SHIFT + ;      ->    wq   
> so as the result you can run:
```
./manage.py migrate
```
___

> ### packages
---
```
 pip3 install django
 ```
```
 pip3 install django-crispy-forms
 ```
```
 pip install psycopg2-binary
 ```
 > ### RUN
 ---
```
python3 manage.py createsuperuser
```
```
python3 manage.py makemigrations
```
```
python3 manage.py migrate
```
>##### **try to modify inbound or outbound rules**
```
python3 manage.py runserver 172.31.5.254:8000
```

---
> ### Database
```
sudo -u postgres psql
```
```
CREATE DATABASE posgresx;
```
```
CREATE USER deep_matrix WITH PASSWORD '1';
```
```
ALTER ROLE deep_matrix SET client_encoding TO 'utf8';
```
```
ALTER ROLE deep_matrix SET default_transaction_isolation TO 'read committed';
```
```
ALTER ROLE deep_matrix SET timezone TO 'UTC';
```
```
GRANT ALL PRIVILEGES ON DATABASE posgresx TO deep_matrix;
```
```
\q
```
---
[No Port](https://www.digitalocean.com/community/tutorials/how-to-set-up-django-with-postgres-nginx-and-gunicorn-on-ubuntu-18-04) 
