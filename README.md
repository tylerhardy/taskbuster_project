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
        __init__.py         <-- taskbuster/__init__.py: An empty file that tells Python that this directory should be considered a Python package.
        settings.py         <-- taskbuster/settings.py: Settings/configuration for the Django project.
        urls.py             <-- taskbuster/urls.py: The URL declarations for the Django project.
        wsgi.py             <-- taskbuster/wsgi.py: An entry-point for WSGI-compatible web servers to serve your project.
    polls/                  <-- The polls/ directory is the Django app that was created with the [manage.py startapp polls] command
        __init__.py         <-- polls/__init__.py: An empty file that tells Python that this directory should be considered a Python package.
        admin.py            <-- polls/admin.py: 
        apps.py             <-- polls/apps.py: 
        models.py           <-- polls/models.py: 
        tests.py            <-- polls/tests.py: 
        views.py            <-- polls/views.py: 
        migrations/         <-- The polls/migrations/ directory 
            __init__.py     <-- polls/migrations/__init__.py: An empty file that tells Python that this directory should be 
                            --- considered a Python package.
```

# Project Setup
Input the following commands into the shell prompt:
```shell
mkdir taskbuster_project                    <-- Creates the taskbuster_project directory.
cd taskbuster_project                       <-- Change directory into the taskbuster_project folder.
virtualenv venv                             <-- Create the python virtual environment for venv.
ve                                          <-- Alias to activate the virtual environment
pip install Django                          <-- Install Django within the virtual environment
pip freeze > requirements.txt               <-- Export all pip installed packages to a text file.
Django-admin.py startproject taskbuster .   <-- Create a Django project, the '.' tells Django to not create a project root folder.
vs .gitignore                               <-- Alias to create the .gitignore file with visual studio code.
git init                                    <-- Initialize the git repository.
vs README.md                                <-- Alias to create the README.md file with visual studio code.
```

## Updating `.gitignore`
copy the following into `.gitignore`:
```
__pycache__/                                <-- Ignores any and all __pycache__ directories.
venv/                                       <-- Ignores the virtual environment directory for venv.
vtest/                                      <-- Ignores the virtual environment directory for vtest.
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

## Test the Django Project
```shell
python manage.py runserver                  <-- Start the Django development server.
```
Open a new browser tab and navigate to: `http://localhost:8000/`.  If everything is working correctly the page will show **It worked!**.

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

# Django App
Apps can live anywhere on your Python path.  Apps are typically created in the same direcotry as manage.py.  This is so it can be imported as its own top-level module, rather than a submodule of 'taskbuster'.  Following the Django tutorial, an app called 'polls' will be created:
```shell
python manage.py startapp polls             <-- Create a new app called 'polls' within the Django project.
```

## Projects vs. Apps
What is the difference between a *Project* and an *App*?  An *App* is a **Web application** that does something (forum, blog, store, etc...). A *Project* is a collection of configuration and apps for a particular website.  A project can contain multiple apps.  An app can be in multiple projects.

