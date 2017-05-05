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
git remote add origin git@github.com:tylerhardy/taskbuster.git  <-- Connects the local git repository to the one on GitHub
git push -u origin master                                       <-- Pushes the local repository to the master on GitHub
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

# Different Environments and Settings
## Different Virtual Environments
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
## Different Settings
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
Navigate to where the tb_dev and tb_test virtual environments are located.  Modify the activate.bat file for each one and append the following:

`tb_dev` environment:
```batch tb_dev
set "DJANGO_SETTINGS_MODULE=taskbuster.settings.development"            <-- The enviroment setting to point to the development Django settings.
```
`tb_test` environment:
```batch tb_test
set "DJANGO_SETTINGS_MODULE=taskbuster.settings.testing"                <-- The enviroment setting to point to the test Django settings.
```

## Production Settings -- Debug False
Cut the `DEBUG` variable from the `base.py` and copy it into the `development.py` and `testing.py` setting files.  Copy the same variable but set to `False` into the `production.py` and `staging.py` setting files.
```py
# SECURITY WARNING: don't run with debug turned on in production!
DEBUG = True # True for development.py and testing.py and False for production.py and staging.py
```

## Django security and the Secret Key

# Django App
Apps can live anywhere on your Python path.  Apps are typically created in the same direcotry as manage.py.  This is so it can be imported as its own top-level module, rather than a submodule of 'taskbuster'.  Following the Django tutorial, an app called 'polls' will be created:
```shell
python manage.py startapp polls             <-- Create a new app called 'polls' within the Django project.
```

## Projects vs. Apps
What is the difference between a *Project* and an *App*?  An *App* is a **Web application** that does something (forum, blog, store, etc...). A *Project* is a collection of configuration and apps for a particular website.  A project can contain multiple apps.  An app can be in multiple projects.
