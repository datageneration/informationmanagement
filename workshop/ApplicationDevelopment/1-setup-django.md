# EPPS6354 Information Management workshop

This workshop demonstrates developing an application using database server, webserver and application server.

## I. Setup environment and web server

1. Prerequisites
    * PostgreSQL
    * pgAdmin
    * Anaconda
    * Python 3.x, pip
    * PyCharm (optional)
2. install [Django](https://docs.djangoproject.com/en/3.0/intro/install/)
    * ``` pip -V``` # Check Python package manager available
    * ```python -m venv epps6354``` # Set up virtual environment for project
       | MacOS         | Windows   | 
      |:-------------:|:-------------:| 
      |```cd epps6354/bin``` | ```cd epps6354\Scripts```|
      |```activate```        | ```activate.bat```       |
  
      * Installation guides
      | [MacOS](https://docs.djangoproject.com/en/3.2/topics/install/)         | [Windows](https://docs.djangoproject.com/en/3.2/howto/windows/)   | 
      
    * ```python -m pip install Django``` # Install Django
    * ```pip install psycopg2-binary ``` # Install PostgreSQL database adapter
    * ```python -m django --version```  # Check if Django installed
3. Initiate a project (Read this [Tutorial](https://docs.djangoproject.com/en/3.0/intro/tutorial01/) for building a Django project for the first time)
    * Initiate project structure``` django-admin startproject mysite ```
    * ``` cd mysite ``` (check if manage.py is in the folder/directory)
    * Run Webserver ``` python manage.py runserver ```
    * In your favorite browser, go to ``` http://127.0.0.1:8000/ ``` 
    * admin ``` http://127.0.0.1:8000/admin ```

--> [next](https://github.com/datageneration/informationmanagement/blob/master/workshop/ApplicationDevelopment/2-connect-database.md)
