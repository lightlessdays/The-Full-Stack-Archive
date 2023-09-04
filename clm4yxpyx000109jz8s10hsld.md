---
title: "Building our own RESTful API"
datePublished: Mon Sep 04 2023 14:20:02 GMT+0000 (Coordinated Universal Time)
cuid: clm4yxpyx000109jz8s10hsld
slug: building-our-own-restful-api
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1693837143135/566b4f21-4e37-468f-bf42-d763acba3340.jpeg
tags: backend, apis, node-js

---

API stands for Application Programming Interface which is a software intermediary that allows two software programs to connect and talk to each other.

REST stands for REpresentational State Transfer. REST is simply an architectural style on how an API should behave and look. So whenever we call a REST or RESTful API, the server provides us or the client with the representation of the state of the requested resources.

There are a few request option that REST API provides us :

* GET — According to the endpoints and parameters that we pass, the API returns some data.
    
* PUT — It looks for the record in the provided URI and updates the existing record. If the record is not present, it creates a new one.
    
* POST — It creates and adds a new record in the database.
    
* DELETE — It removes the requested record in the given URI.
    
* PATCH — It updates the individual fields of a record.
    

Now let’s fold up our sleeves and get started to build a REST API with Django Rest Framework.

## 🕵️ Django Configuration

Make sure that you have installed Python in your system. I generally use PyCharm to do my work. You can use any IDE you like.

First, we will install `pipenv`.

```bash
$ pip install pipenv
```

Next, let us install Django.

```bash
$ pip install django
```

Next, let us activate the environment

```bash
$ pipenv shell
```

And now let us create a new Django Project.

```bash
$ django-admin startproject myrestapi
```

Now we can go to the folder in our project containing the `manage.py` file and run the following command to start our server:

```bash
$ python manage.py runserver
```

Next, go to [`http://127.0.0.1:8000/`](http://127.0.0.1:8000/) in your browser to see the server live. It should look something like this:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693777127003/ee202b31-8cbe-4d05-9046-8c4ccab8ff8e.png align="center")

## 🚂 Creating an API App

Let us create a new separate app for API.

```bash
$ python manage.py startapp api
```

First and foremost thing to do after we create an app in django project is to register it in the project level settings file.

Let us register it now in `myrestapi/settings.py` file

```bash
INSTALLED_APPS = [
    'api', #added here
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
]
```

Django ORM creates a sql commands for us whenever we create a new models in our project. But before making any new models, we need to migrate it because django project itself comes with some cool models built-in beforehand.

So let us migrate them now.

```bash
$ python manage.py migrate
```

Before going any further let us create a superuser which will allow us to check out out models in the cool built-in admin interface.

```bash
$ python manage.py createsuperuser
```

Start the django server to verify the credentials.

```bash
$ python manage.py runserver
```

Head over to the [http://127.0.0.1:8000/admin/](http://127.0.0.1:8000/admin/)

![](https://miro.medium.com/v2/resize:fit:593/1*Osh5FgZaKT78q-ZkoWdnXA.png align="center")

Now login with the credentials created before and you will be able to see:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693825981143/86b2e5b2-0fc9-455e-adb2-d0c8fc90226d.png align="center")

## 🫥Creating a Model in the API App

Now create our first model. Open up the file `api/models.py` and type in the following:

```python
from django.db import models

# Create your models here.
class Detectives(models.Model):
    name = models.CharField(max_length=50)
    location=models.CharField(max_length=50)

    def __str__(self):
        return  self.name
```

`name` and `location` are the strings which are in the form of CharField. The `str` method returns `instance` of the model `Detective`, in this case, a name and we can put other fields as per the requirement.

We just created a new model. Whenever we update existing model or create a new one, we need to make the migrations so that django will make the necessary commands.

```python
$ python manage.py makemigrations
```

```python
$ python manage.py migrate
```

Shortly before we saw the cool Django admin page. But it will not show our newly created model. So let us add two lines of code in `api/admin.py` file.

```python
from django.contrib import admin
from .models import Detective
# Register your models here.

admin.site.register(Detective)
```

Now run the Django server and goto [http://127.0.0.1:8000/admin/](http://127.0.0.1:8000/admin/)

Let us create some new detectives on the admin page. Click on **“Add**” and you are ready to go.

## 🚹 Django REST Framework

Let us install Django Rest Framework so that we can serialize our records in the databases.

```python
$ pipenv install djangorestframework
```

Again register the newly installed app in the myrestapi/settings.py file.

```python
INSTALLED_APPS = [
    'api',
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'rest_framework' #add this
]
```

Now let us serialize the Detective Model. Serialization is the process of converting database records into the JSON formatted values so that user can understand them.

This all will be handled by rest framework. All we need to do is some configuration work. We have to connect the Django Rest framework and the models that we created before.

Create a new file as `serializers.py` in the `api/` directory. Add the following lines of code to the file:

```python
from rest_framework import serializers
from  .models import Detectives

class DetectiveSerializer(serializers.HyperlinkedModelSerializer):
    class Meta:
        model=Detectives
        fields=('name','location')
```

Now all left is to display the data in the browser. For that we have to some configuration urls and views file.

Head over to the api/views.py file and add the following code to it:

```python
from rest_framework import viewsets
from serializers import DetectiveSerializer
from .models import Detectives

class DetectiveViewSet(viewsets.ModelViewSet):
    queryset = Detectives.objects.all().order_by('name')
    serializer_class = DetectiveSerializer
```

We have to specify the url at the project level file at first. Django looks up to site urls at first to resolve the requested url address. Head over to the file `myrestapi/urls.py`.

```python
from django.contrib import admin
from django.urls import path
from django.urls import include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('',include('api.urls'))
]
```

We included `api.urls` in the project level urls file. But wait... Where is that file? We have to create that now in the app-level directory which in case of our project is `api`.

Create a new file name as `urls.py` inside the app/ directory and add the following code to it:

```python
from rest_framework import routers
from django.urls import path
from django.urls import include
from . import views

router = routers.DefaultRouter()
router.register(r'detectives',views.DetectiveViewSet)

urlpatterns =[
    path ( ' ' , include(router.urls)),
    path ('api—auth/',include('rest_framework.urls' , namespace='rest_framework'))

]
```

Start up the Django server again and head over to [http://127.0.0.1:8000/](http://127.0.0.1:8000/)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693834112063/3c487f3f-e7d1-42f7-907d-8983cec49846.png align="center")

Head over to [http://127.0.0.1:8000/detectives/?format=json](http://127.0.0.1:8000/detectives/?format=json) to see the .JSON data.

We can also get the individual detective API with the format

[http://127.0.0.1:8000/detectives/&lt;id&gt;](http://127.0.0.1:8000/detectives/<id>) where id is the unique key for our detectives which is automatically assigned by Django models.

This is all great. Now, let us see how to host this on a server.

## Hosting API Project

Deploying a Django project on PythonAnywhere is a lot like running a Django project on your own PC. You'll use a virtualenv, just like you probably do on your own PC, you'll have a copy of your code on PythonAnywhere which you can edit and browse and commit to version control.

The main thing that's different is that, instead of using the Django dev server with [`manage.py`](http://manage.py) `runserver` and viewing your site on [localhost](http://localhost), you'll create what we call a *Web app* via the Web tab in our UI, and then configure it with a *WSGI file* whose job is simply to import your Django project.

And then your site will be live on the real, public Internet. woo!

Here's an overview of the steps involved.

1. Upload your code to PythonAnywhere
    
2. Set up a virtualenv and install Django and any other requirements
    
3. Set up your web app using the **manual config** option
    
4. Add any other setup (static files, environment variables etc)
    

Assuming your code is already on a code sharing site like GitHub or Bitbucket, you can just clone it from a **Bash Console**:

```python
$ git clone https://github.com/myusername/myproject.git
```

In your Bash console, create a virtualenv, naming it after your project, and choosing the version of Python you want to use:

```python
$ mkvirtualenv --python=/usr/bin/python3.10 mysite-virtualenv
$ pip install django
```