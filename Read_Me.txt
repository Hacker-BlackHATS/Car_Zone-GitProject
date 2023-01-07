**SetUp Virtual Environment
1. Create Folder.
2. Open Git Bash inside the folder.
3. Inside Git Bash:
>> python -m venv env
# env is the name of our environment
>> source env/Scripts/activate
For MAC Users:
>> source ./env/bin/activate
4. To come out of the virtual environment
>> deactivate

$$ Activate virtual environment env $$

** Install Dependencies
1. pip install django==3.0.7
# To Follow this course use the above version of django.

** Create Django Project
1. django-admin startproject carzone .
# carzone is the project name
# We have write this dot(.) because otherwise it will create multiple folders.
2. To check if django is working or not.
>> python manage.py runserver
{
ImportError: DLL load failed while importing _sqlite3: The specified module could not be found.
If this error comes :
Locate the sqlite3.dll file. In my case it was in following folder:
[C:\Users\DELL-PC\anaconda3\Library\bin]
where [C:\Users\DELL-PC\anaconda3] is the folder where Anaconda was installed

Add this to PATH in environment variables, and it should work then.
}

3. To Open Django in the Web Browser, type this in the address bar:
>> 127.0.0.1:8000

^
In this project we will be creating 3-4 apps:
1. Pages App : Contact pages, Service pages
2. Cars App
3. Contacts App
4. Accounts App
^

** Creating Pages App
1. Command
>> python manage.py startapp pages
# App name is pages
2. As soon as we create a app, the first thing we need to do is:
Go to the Project folder (carzone) --> settings.py
Here in the INSTALLED_APPS, we have to add this app.
'pages.apps.PagesConfig',
# The PagesConfig came from 
We have created the pages app,
Inside the pages folder we have apps.py file.
Open it and you will see a class with PagesConfig as class name.
So what ever the class name is we have to copy it and paste it there.
<app_name>.apps.<class_name_in_apps.py_file_inside_app_folder>
We will do this for every app.

Next is URLs, now if you notice in pages app folder we do not have any urls.py file.
We have urls.py in main project folder.
So create a new file inside pages app folder, name it urls.py and edit it.

Now the urls.py file in project folder will look like:

from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('pages.urls')),
]

When someone request for the home page, the control will go to pages app and 
inside pages app we have urls.py which will be called.

Now configure this in pages app urls.py file as:

from django.urls import path
from . import views

urlpatterns = [
    path('', views.home, name='home'),
]

Now we need to create views called home inside views.py file in pages app folder.
pages/views.py file will look like:

from django.shortcuts import render

def home(request):
    return render(request, 'pages/home.html')  # pages/home.html -> Template

Right now we do not have pages/home.html folder.
So first create a new folder called templates inside CarZone_Project folder.
Inside templates folder create another folder called pages.
Inside templates/pages folder create home.html file.
templates/pages/home.html file :

<h1>HOME PAGE</h1>
<h4>Hello World</h4>

Since we had created this template folder, we have to tell the project 
folder settings.py file that we have created a templates folder and 
we need to give it a template directory name.
Inside carzone/settings.py file add templates folder name inside 
TEMPLATES list -> 'DIRS' : ['templates'],

Now run the server and you will see the home page.
