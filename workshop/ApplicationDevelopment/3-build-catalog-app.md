# EPPS6354 Information Management workshop

## III. Database functions


# [Catalog](https://developer.mozilla.org/en-US/docs/Learn/Server-side/Django)
[MVC]: https://mdn.mozillademos.org/files/13931/basic-django.png "MVC"
[MVC Flow](https://mdn.mozillademos.org/files/13931/basic-django.png)
1. Create an app named catalog
    * Create app ``` python manage.py startapp catalog ```
    * Check ```cd mysite``` and look for catalog folder/directory
    * Edit the file views.py in catalog using nano (MacOS) or notepad (Windows) (Note the different dashes in different OS's:
      | MacOS         | Windows   | 
      |:-------------:|:-------------:| 
      | nano catalog/views.py       |notepad catalog\views.py |
    * Paste the following to the end of the views.py file  
    ```python
    
   from django.http import HttpResponse
   from django.template import loader
   from .models import Department
   from django.shortcuts import render
    from django.http import HttpResponse
    def index(request):
        return HttpResponse("Hello, world. You're at the catalog index.")
    def dept(request):
        departments = Department.objects.all()
        template = loader.get_template('catalog/dept.html')
        context = {
            'department_list': departments,
        }
        return HttpResponse(template.render(context, request))   
    ```
    * Create a page for data output: catalog/templates/catalog/dept.html
    in catalog directory:
    - cd catalog
    - mkdir templates
    - cd templates
    - mkdir catalog
    - cd catalog # Note this is another catalog folder/directory
    - Create the file catalog/templates/catalog/dept.html using nano (MacOS) or notepad (Windows):
| MacOS         | Windows   | 
      |:-------------:|:-------------:| 
      | nano dept.html      |notepad dept.html|
    * Create the new file  
    * Paste the following to the dept.html file 
       
    ```html
    {% load static %}
    
    <link rel="stylesheet" type="text/css" href="{% static 'catalog/style.css' %}">
    
    {% if department_list %}
        <table ="1">
    <tr><th>Department</th><th>Building</th></tr>
        {% for dept in department_list %}
            <tr>
                <td>{{ dept.dept_name }}</td>
                <td>{{ dept.building }}</td>
            </tr>
        {% endfor %}
        </table>
    {% else %}
        <p>No Departments are available.</p>
    {% endif %}
   
    ```
   * Create a urls.py file in catalog folder/directory
   | MacOS         | Windows   | 
      |:-------------:|:-------------:| 
      | nano mysite/catalog/urls.py      |notepad mysite\catalog\urls.py|
   * Paste the following to the urls.py file 
       

   ```python
   from django.urls import path
   from . import views
   urlpatterns = [
        path('', views.index, name='index'),
   ]
    ```
   
   * Change to mysite directory
   * ``` cd ..```
   * Edit the main routing file mysite/urls.py
   * Full path Mac: mysite/mysite/urls.py | Windows mysite\mysite\urls.py
   | MacOS         | Windows   | 
      |:-------------:|:-------------:| 
      | nano urls.py      |notepad  urls.py|
  
   ```python
    from django.contrib import admin
    from django.urls import include, path

    urlpatterns = [
        path('catalog/', include('catalog.urls')),
        path('admin/', admin.site.urls),
    ]
    ```
   * In terminal, make sure you stop the webserver (press Ctrl-C to stop), restart it with ``` python manage.py runserver```
2. List Departments
    * Edit catalog/urls.py
    * Full path: Mac: mysite/catalog/urls.py | Windows mysite\catalog\urls.py
    ```python
    from django.urls import path
    from . import views

    urlpatterns = [
        path('', views.index, name='index'),
        path('dept', views.dept, name='dept'),
    ]
    ```
    * Edit catalog/models.py
    * Full path: Mac: mysite/catalog/models.py | Windows mysite\catalog\models.py
    ```python
    from django.db import models

    class Department(models.Model):
        dept_name = models.CharField(primary_key=True, max_length=20)
        building = models.CharField(max_length=15, blank=True, null=True)
        budget = models.DecimalField(max_digits=12, decimal_places=2, blank=True, null=True)

        class Meta:
            managed = False
            db_table = 'department'
    ```
    * Edit mysite/settings.py
    * Full path: Mac: mysite/mysite/settings.py | Windows mysite\mysite\settings.py
    ```python
    INSTALLED_APPS = [
        'catalog.apps.CatalogConfig',
        'django.contrib.admin',
        'django.contrib.auth',
        'django.contrib.contenttypes',
        'django.contrib.sessions',
        'django.contrib.messages',
        'django.contrib.staticfiles',
    ]
   ```
    * Edit catalog/admin.py
    * Full path: Mac: mysite/catalog/admin.py | Windows mysite\catalog\admin.py
    ```python
       from django.contrib import admin
       from .models import Department

       admin.site.register(Department)
   ```
    * visit ```http://localhost:8000/catalog/dept```

<div align="left"><a href="https://github.com/datageneration/informationmanagement/blob/master/workshop/ApplicationDevelopment/2-connect-database.md"><-- Back</a></div>
<div align="right"><a href="https://github.com/datageneration/informationmanagement/blob/master/workshop/ApplicationDevelopment/4-add-pages.md"> Next--></a></div>

