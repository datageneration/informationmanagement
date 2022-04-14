1. Confirm Web Server is running
    * ``` cd epps6354 ```
    * Run Webserver ``` python manage.py runserver ```
    * In your favorite browser, go to ``` http://127.0.0.1:8000/ ``` 
    * admin ``` http://127.0.0.1:8000/admin ```
    
2. Connect to Database
    * Install python-postgres database engine/connector ``` pip install psycopg2 ```
      | MacOS         | Windows   | 
      |:-------------:|:-------------:| 
      | nano mysite/settings.py       |notepad mysite\settings.py |
    * Edit the file mysite/settings.py using nano (MacOS) or notepad (Windows)
      * You can use your favorite editor and find the file in Finder (Mac) or File Explorer (Windows)   
    * Once you open the file, find "DATABASES" dictionary, use copy and paste and change it to:
    ```python      
        DATABASES = {
        'default': {
            'ENGINE': 'django.db.backends.postgresql',
            'NAME': 'postgres',
            'USER': 'postgres',
            'PASSWORD': 'mysecretpassword',
            'HOST': 'localhost',
            'PORT': '5432',
            }
        } 
    ```
    * Be sure to change to your PostgreSQL password
    * Restart Web Server ```python manage.py runserver ```
    
3. ORM ( Object-Relational Mapping )
    * Stop Django server
    * Create and apply SQL to database ```python manage.py migrate ```
    * Create super user ```python manage.py createsuperuser```
    * Restart Web Server ```python manage.py runserver ```
    * Inspect Models, visit ``` http://127.0.0.1:8000/admin ```
    * Login using your superuser credentials 

<div align="left"><a href="https://github.com/datageneration/informationmanagement/blob/master/workshop/ApplicationDevelopment/2-connect-database.md"><-- Back</a></div>
<div align="right"><a href="https://github.com/datageneration/informationmanagement/blob/master/workshop/ApplicationDevelopment/3-build-catalog-app.md"> Next--></a></div>
