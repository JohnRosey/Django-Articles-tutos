## **Converting any HTML template into a Django template  for Macos**

 - Create a new django project by:
`django-admin startproject MyProject`

 - cd into the project `cd MyProject/` and start an app main:
`python manage.py startapp main`
 

 - cd again in `Myproject` folder and create there a folder 'main'
 - cd `main`  and create `template` folder there
 - cd `template` and create `main` folder again
 - copy and paste all your html template files in main
 - create `static` folder there and copy and paste your js , css img folder or files
 - In `setting.py` file of MyProject in TEMPLATES section  add in DIRS :
   ` TEMPLATES =  [ {
      'DIRS':  [os.path.join(BASE_DIR, "MyProject/main/template"),], `
      add also :
`STATICFILES_DIRS=[os.path.join(BASE_DIR,"MyProject/main/template/static")  ]`

## The file structure will now look something like this:




We need to include the line  `{% load static %}`  at the top of the html page in order to be able to use the static tag.

We need to include the app in the  `settings.py`  file by adding  `'main.apps.MainConfig'`  in the INSTALLED_APPS list and add a view for creating rendering the index page

 -  In MyProject/main/views.py
`from django.shortcuts import render`
`def index (request):`
`return render(request, 'main/index.html')`
 - and also add a url route for the same, create a file urls.py in MyProject/main/ and add the following code :
 `from . import views`
`from django.urls import path`
`app_name = 'main'`
`urlpatterns = [`
 `path('', views.index, name='index'),`
`]`
- now finally we need to add the following in the MyProject/MyProject/urls.py :
`from django.contrib import admin`
`from django.urls import path, include`
`urlpatterns = [`
`path('admin/', admin.site.urls),`
 `path('', include('main.urls', namespace='main')),]`
## # The djangify
**It exists a python package [djangify](https://pypi.org/project/djangify/) which can be installed by:  
`pip install djangify`**
after installing the package just run the following command from your shell inside the MyProject directory:

`djangify -d main/templates/main`

the tool will create a folder "Modified_files" in which there will be HTML with every CSS, JS reference converted to the django compatible reference, replacing the index.html in the main/templates/main/ with the same named file in main/templates/main/Modified_files/ we can easily see the same output as above.

## Migrating the changes and running server

 

 

    python manage.py migrate
    python manage.py runserver

Please feel free to drop a message at [Ohuru](https://ohuru.tech/) in order to avail various development services offered by us.
Sources:
https://dev.to/amartyadev/converting-any-html-template-into-a-django-template-25ob
