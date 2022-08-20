```yaml
name: action

on:
  push:
    branches: 
      - main
      - devops
      
  pull_request:
    branches: [ "main" ]

  workflow_dispatch:

jobs:
  build:
    runs-on: self-hosted

    steps:
    
      - name: cleanup
        run : |
          sudo chown -R $USER:$USER $GITHUB_WORKSPACE          
        
      - uses: actions/checkout@v2
      
      - name: Create env file
        run : |
          virtualenv env    
      
      - name: Activate venv
        run : |
          source env/bin/activate
          
          
      - name: Install required packages #1
        run : |
          pip3 install django gunicorn psycopg2-binary   
          
         
#      - name: Install required packages #2
#        run : |
#          pip3 install -r req.txt    
          
      - name:   Installing Django
        run : |
          pip3 install django
          
          
      - name:   Installing Crispy Forms
        run : |
          pip3 install django-crispy-forms
          
      - name:   Installing Psycopg2
        run : |
           pip3 install psycopg2-binary
         
      - name: Collectstatic
        run : |
          python3 manage.py collectstatic
          
      - name: Makemigrations
        run : | 
          python3 manage.py makemigrations
          
      - name: Migrate
        run : |
          python3 manage.py migrate
      - name: Run
        run : |
          python3 manage.py runserver 70.34.207.94:8000

#       - name: Restart gunicorn
#         run : |
#           sudo systemctl restart gunicorn


#       - name: Restart nginx
#         run : |
#           sudo systemctl restart nginx

```
