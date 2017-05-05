# taskbuster Django Project
My Django as well as other helpful notes.
https://docs.djangoproject.com/en/1.11/intro/tutorial01/
http://www.marinamele.com/taskbuster-django-tutorial

# File Structure
My ideal Django folder structure
```
taskbuster_project/         <-- The outer taskbuster_project/ root directory is just a container for the project. 
                            --- Its name doesn't matter to Django, and it can be changed.
    env/                    <-- The env/ directory is where the Python3 virtual environement (env) is housed.
    .git/                   <-- The .git/ directory is the git repository.
    .gitignore              <-- The .gitignore file is the git ignore list.
    README.md               <-- The README.md file is the readme of the project.
    requirements.txt        <-- The requirements.txt file is a list of all pip installed packages.
    manage.py               <-- manage.py: A command-line utility that lets you interact with this Django project in various ways.
    taskbuster/             <-- The inner taskbuster/ directory is the actual Python package for your the. It's name is the Python package name.
        __init__.py         <-- taskbuster/__init__.py: An empty file indicating that this folder is a Python package.
        settings.py         <-- taskbuster/settings.py: Settings/configuration for the Django project.
        urls.py             <-- taskbuster/urls.py: The URL declarations for the Django project.
        wsgi.py             <-- taskbuster/wsgi.py: An entry-point for WSGI-compatible web servers to serve your project.
    polls/                  <-- The polls/ directory is the Django app that was created with the [manage.py startapp polls] command
        __init__.py         <-- polls/__init__.py: An empty file indicating that this folder is a Python package.
        admin.py            <-- polls/admin.py: 
        apps.py             <-- polls/apps.py: 
        models.py           <-- polls/models.py: 
        tests.py            <-- polls/tests.py: 
        views.py            <-- polls/views.py: 
        migrations/         <-- The polls/migrations/ directory 
            __init__.py     <-- polls/migrations/__init__.py: An empty file indicating that this folder is a Python package.
```

# Setup
## Global Setup
Install Python3, virtualenv, virtualenvwrapper-win

## Project Setup
Input the following commands into the shell prompt:
```shell
mkdir taskbuster_project                    <-- Creates the taskbuster_project directory.
cd taskbuster_project                       <-- Change directory into the taskbuster_project folder.
mkvirtualenv tb_dev                         <-- Create the python virtual environment for tb_dev.
ve tb_dev                                   <-- Alias to activate the virtual environment
pip install Django                          <-- Install Django within the virtual environment
Django-admin.py startproject taskbuster .   <-- Create a Django project, the '.' tells Django to not create a project root folder.
vs .gitignore                               <-- Alias to create the .gitignore file with visual studio code.
git init                                    <-- Initialize the git repository.
vs README.md                                <-- Alias to create the README.md file with visual studio code.
```

## Updating `.gitignore`
copy the following into `.gitignore`:
```
__pycache__/                                <-- Ignores any and all __pycache__ directories.
*.sqlite3                                   <-- Ignores the sqlite3 databases.
```

## Initializing `.git`
Initialize the repository:
```shell
git status                                  <-- Retrieves the git repository status
git add .                                   <-- Adds all files, folders, and subfolders from current (root) folder and down.
git commit -m "Initializing git"            <-- Commits the changes and appends the change with a message.
```

## Connecting `.git` to Github
Connect local to GitHub repository:
```shell
git remote add origin git@github.com:tylerhardy/taskbuster_project.git  <-- Connects the local git repository to the one on GitHub
git push -u origin master                                               <-- Pushes the local repository to the master on GitHub
```
To remote a remote url:
```shell
git remote -v
git remote rm <name>
```
## Test Driven Development
http://www.marinamele.com/taskbuster-django-tutorial/taskbuster-working-environment-and-start-django-project

### Setup Environemnt
```shell
mkvirtualenv tb_test                    <-- Create the python virtual environment for tb_test.
ve tb_test                              <-- Alias to activate the tb_test virtual environment.
pip install django                      <-- Install Django.
pip install --upgrade selenium          <-- Install selenium.
mkdir functional_tests                  <-- Create the 'functional_tests' directory.
cd functional_tests                     <-- Change directory into the functional_tests directory.
vs all_users.py                         <-- Create a new file called 'all_users.py' and open in Visual Studio Code.
```
Download the chome webdriver to work with selenium: https://sites.google.com/a/chromium.org/chromedriver/downloads. Extract the file and place it into the windows root directory (C:\Windows\).

### First TDD Test
In the `all_users.py` file input the following:
```py
# -*- coding: utf-8 -*-                                         # Indicates the coding of the file.
from selenium import webdriver                                  # Imports 'selenium' and 'unittest', a Python library for testing.
import unittest

class NewVisitorTest(unittest.TestCase):                        # Creats a 'TestCase' class, named 'NewVisitorTest'.

    def setUp(self):                                            # A 'setUp' method that initializes the test.
        self.browser = webdriver.Chrome()                      # Opens the browser.
        self.browser.implicitly_wait(3)                         # Waits 3 seconds if needed (if the page is not loaded).

    def tearDown(self):                                         # A 'tearDown' method that runs after each test.
        self.browser.quit()                                     # Closes the browser.

                                                                # The 'setUp' and 'tearDown' methods run at the beginning and at the end of each 'test' method.

    def test_it_worked(self):                                   # A method that starts with 'test'.
        self.browser.get('http://localhost:8000')
        self.assertIn('Welcome to Django', self.browser.title)  # Asserts that the title of the webpage has 'Welcome to Django' in it.

if __name__ == '__main__':                                      # Only if Python runs the file directly (not imported) it will execute the function 'unittest.main()'.  
                                                                # This function launches the 'unittest Test runner', that identifies the different tests defined by looking for methods that start with 'test'.
    unittest.main(warnings='ignore')                            # The 'unittest.main() function is called with the optional parameter "warnings='ignore'" to avoid a ResourceWarning message.
```
Run the test:
```shell
python all_users.py                         <-- Performs the test specified above.
```
The test should come back with an error.  Start the Django development server and rerun the test.
```shell
python manage.py runserver                  <-- Start the Django development server.
python all_users.py                         <-- Performs the test specified above.
```
The test should come back passing.  You can manually test the server by opening a new browser tab and navigate to: `http://localhost:8000/`.  If everything is working correctly the page will show **It worked!**.

## Common Django Commands
```shell
python -m Django --version                  <-- Checks which version of Django is installed
Django-admin startproject taskbuster        <-- Create a Django project.
python manage.py runserver                  <-- Start the Django development server.
python manage.py runserver 8080             <-- Start the Django development server with a different port number.
python manage.py startapp polls             <-- Create a new app within the Django project.
python manage.py migrate                    <-- Command to 
python manage.py makemigrations appname     <-- Command to 
```

# Environment Requirments and Django Settings
## Virtual Environments Requirements
```shell
mkdir requirements                                                      <-- Creat new folder called 'requirements'.
cd requirements                                                         <-- Change directory to the requiremenst folder.
echo Django==1.11 >> base.txt                                           <-- Create the 'base.txt' file with the echo string.
echo -r base.txt | tee -a development.txt testing.txt production.txt    <-- Append all files with "-r base.txt".
echo selenium==3.4.1 >> testing.txt                                     <-- Create the 'testing.txt' file with the echo string.
..                                                                      <-- Go up a directory.
ve tb_dev                                                               <-- Activate the development virtual environment.
pip install -r requirements/development.txt                             <-- Install the development.txt requirements.
d                                                                       <-- Deactivate the development virtual environment.
ve tb_test                                                              <-- Activate the testing virtual environment.
pip install -r requirements/testing.txt                                 <-- Install the testing.txt requirements.
d                                                                       <-- Deactivate the testing virtual environment.
```
## Split Django Settings
Create a settings folder within the taskbuster folder (not the taskbuster_proj folder).
```shell
mkdir taskbuster\settings                   <-- Create new folder called 'settings' within the 'taskbuster' directory.
cd taskbuster\settings                      <-- Change directory to the taskbuster\settings\ folder.
touch __init__.py                           <-- Create an emtpy __init__.py file.
echo # -*- coding: utf-8 -*- | tee -a development.py testing.py production.py staging.py    <-- Append files with the echo string.
echo from .base import * | tee -a development.py testing.py production.py staging.py        <-- Append files with the echo string.
mv ../settings.py base.py                   <-- Move the settings.py from up-one-level directory into the current directory as base.py.
```
## Modify Virtual Environment Activate Script
Navigate to where the **tb\_dev** and **tb\_test** virtual environments are located.  Modify the `activate.bat` file for each one and append the following:

`tb_dev` environment:
```batch tb_dev
set "DJANGO_SETTINGS_MODULE=taskbuster.settings.development"            <-- The enviroment setting to point to the development Django settings.
```
`tb_test` environment:
```batch tb_test
set "DJANGO_SETTINGS_MODULE=taskbuster.settings.testing"                <-- The enviroment setting to point to the test Django settings.
```

## Debug Settings
Cut the `DEBUG` variable from the `base.py` and copy it into the `development.py` and `testing.py` setting files.  Copy the same variable but set to `False` into the `production.py` and `staging.py` setting files.
```py
# SECURITY WARNING: don't run with debug turned on in production!
DEBUG = True # True for development.py and testing.py and False for production.py and staging.py
```

## Secret Key
Copy and remove the secret key from `base.py` and paste it in a new file called `secret.py`.
```py
# SECURITY WARNING: keep the secret key used in production secret!
SECRET_KEY = '<secret key>'                 #-- Django's secret key.
```
In the `base.py` file paste the following:
```py
from .secret import *                       #-- Imports everything from the settings.secret module (settings/secret.py)
```

## Static Files
Create a new folder within the `taskbuster/` directory called `static`.  This folder will contain all the static files that are global for the whole project, such as CSS or javascript files.
```shell
cd taskbuster                               <-- Change directory to 'taskbuster'.
mkdir static                                <-- Create a new directory called 'static'.
```
To tell Django to point to this location open `base.py` file and append the following after STATIC_URL:
```py
STATICFILES_DIRS = (
    os.path.join(BASE_DIR, 'static'),
)
```

## Template Settings
Create a new folder within the `taskbuster/` directory called `templates`.  This folder will contain all the templates that will be used throughout all of the project.
```shell
cd taskbuster                               <-- Change directory to 'taskbuster'.
mkdir templates                             <-- Create a new directory called 'templates'.
```
Update the `base.py` setting file to point Django to the global template folder:
```py
'DIRS': [os.path.join(BASE_DIR, 'templates')],          # Tells Django where else to look for template folders.
```

## HTML5 Boilerplate and Twitter Bootstrap
http://www.initializr.com/

- Move the files `index.html`, `404.html`, `humans.txt` and `robots.txt` into the `taskbuster/templates` folder.
- Change the name of `index.html` to `base.html`. The index file is usually the template of your Home page, but we will use it as a base template — all our site templates will inherit from this base template.
- Move the other files and folders into the `taskbuster/static` folder
- If you have an icon you would like to use for your app, replace it for the favicon.ico file (I recommend you use the same name).
- I also removed the files apple-touch-icon.png, browserconfig.xml, tile-wide.png and tile.png.

## Home Page with Test Driven Development - Test First
Convert the folder function_tests into a Python package by including an empty file named `__init__.py` inside.
```shell
cd functional_tests                     <-- Change directory to 'functional_tests'.
touch __init__.py                       <-- Creates an empty file named '__init__.py'.
```
With `functional_tests` a Python package we can now run our functional tests with:
```shell
git mv functional_tests/all_users.py functional_tests/test_all_users.py     <-- Renames the file with git so it will start with 'test'.
python manage.py test functional_tests                                      <-- Runs the test runner to find files that start with 'test'.
```

### Modify First TDD Test
```py
# -*- coding: utf-8 -*-
from selenium import webdriver
from django.core.urlresolvers import reverse
from django.contrib.staticfiles.testing import LiveServerTestCase

class NewVisitorTest(LiveServerTestCase):

    def setUp(self):
        self.browser = webdriver.Chrome()
        self.browser.implicitly_wait(3)

    def tearDown(self):
        self.browser.quit()

    def get_full_url(self, namespace):
        return self.live_server_url + reverse(namespace)

    def test_home_title(self):
        self.browser.get(self.get_full_url('home'))
        self.assertIn('TaskBuster', self.browser.title)

    def test_h1_css(self):
        self.browser.get(self.get_full_url('home'))
        h1 = self.browser.find_element_by_tag_name('h1')
        self.assertEqual(h1.value_of_css_property('color'), "rgba(200, 50, 255, 1)")
```
- Define an auxiliar function named `get_full_url` that takes one argument, the `namespace`.
  - A `namespace` is an identifier for a url.
  - `self.live_server_url` gives you the local host url (http://localhost:8021). 
  - Revers gives you the **relative** url of a given namespace (/).
  - The resulting function gives you the absolute url of that namespace (the sum of the previous two (http://localhost:8021/)).
- The `test_home_title` method tests that the home page title contains the word 'TaskBuster'.
- The `test_h1_css` method tests that the h1 text has the desired color.
- `if __name__ == '__main__'` statement was removed as `functional_tests` is now a package that will run with the Django test runner.

## Home Page with Test Driven Development - Code Next
Open `taskbuster/urls.py` and append the following:
```py
from .views import home                 # Using '.views' instead of 'taskbuster.views' is that making it relative we can change the name 
                                        # of the project without fear of breaking something.
urlpatterns = [
    ...
    url(r'^$', home, name='home')       # 
    ...
]
```
Create a file in `taskbuster/` called `views.py`.  Input the following:
```py
def home(request):
    return ""
```
Create a new file in `taskbuster` folder called `test.py` and input the follwoing code:
```py
# -*- coding: utf-8 -*-
from django.test import TestCase
from django.core.urlresolvers import reverse

class TestHomePage(TestCase):
    def test_uses_index_template(self):
        response = self.client.get(reverse('home'))
        self.assertTemplateUsed(response, 'taskbuster/index.html')

    def test_uses_base_template(self):
        response = self.client.get(reverse('home'))
        self.assertTemplateUsed(response, 'base.html')
```
Run the test we just created with the following command:
```shell
python manage.py test taskbuster.test
```
Create the `taskbuster/index.html` template:
```shell
cd taskbuster/templates
mkdir taskbuster
touch taskbuster\index.html
```
Open `taskbuster\views.py` and add the following:
```py
# -*- coding: utf-8 -*-
from django.shortcuts import render

def home(request):
    return render(request, 'taskbuster/index.html', {})
```
Where we have used the shortcut `render`, which lets you load a template, create a context adding a bunch of variables by default, such as information about the current logged-in user, or the current language, render it and return an **HttpResponse**, all in one function.

Modify `base.html` file and change the `<title></title>` to the follwoing:
```html
        <title>{% block title %}{% endblock title %}</title>
```
These two template tags, `{% block title %}` and `{% endblock title %}` mark the beginning and the end of a content block, which contents can be replaced by child templates.

Modify `index.html` file and make it inherit from the `base.html` file and add a title.
```html
{% extends 'base.html' %}
{% block title %}TaskBuster Django Tutorial{% endblock title %}
```

Open `taskbuster/static/css/main.css` and add the following:
```css
.jumbotron h1 {
    color: rgba(200, 50, 255, 1);
}
```

Open `base.html` and add the following at the beginning of the file:
```html
{% load staticfiles %}
```

Change links to the static files and scripts of javascript to:
```html
...
<link rel="stylesheet" href="{% static 'css/bootstrap.min.css' %}">
...
<link rel="stylesheet" href="{% static 'css/bootstrap-theme.min.css' %}">
<link rel="stylesheet" href="{% static 'css/main.css' %}">
...
<script src="{% static 'js/vendor/modernizr-2.8.3-respond-1.4.2.min.js' %}"></script>
...
<script src="{% static 'js/vendor/bootstrap.min.js' %}"></script>

<script src="{% static 'js/main.js' %}"></script>
...
```

Open `test_all_users.py` and modify the following:
```py
- from django.test import LiveServerTestCase
+ from django.contrib.staticfiles.testing import StaticLiveServerTestCase
 
- class HomeNewVisitorTest(LiveServerTestCase):
+ class HomeNewVisitorTest(StaticLiveServerTestCase):
```

