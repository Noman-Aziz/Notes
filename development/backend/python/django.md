# Django

### Introduction

Django is a high-level Python web framework that enables rapid development of secure and maintainable websites. It allows you to develop websites and web applications in a matter of hours.

Django can automatically compile HTML code, therefore making it possible for anyone without any advanced knowledge in markup languages to develop a website. Additionally, Django is arguably one of the most secure developing frameworks, which in the right configuration, can strongly resist against SQL injections and XSS.

***

### Creating Project

run `django-admin startproject {project_name}` in order to start your project. (Replace {project\_name} with your prefered name).

Run `python3 manage.py migrate` to automatically configure new files.

After creating the project you can see that Django creates a file `manage.py` and a file directory named after your project.

***

### Manage.py

`manage.py` is a command-line utility that lets you interact with your Django project in various ways. It is especially handy in creating web-apps, managing databases, and most importantly running the server.

Basic syntax for using this utility is `python3 manage.py {command}`

#### Commands

* `runserver` : Runserver is the most important command used with manage.py; It allows you to deploy your website on the server.
* `createsuperuser` : This command allows you to create an admin account for your Django web admin panel.
* `startapp` : Startapp allows you to initialize an app for your project. Django projects can have infinite number of apps. Basic syntax:
  * `python3 manage.py startapp {app_name}`

***

### Operation of Django Websites

***

### Creating Website

1. Create an app using a command.
2. Head over to **settings.py** and include your **app name** in _INSTALLED\_APPS_:
   *
3. Head over to `urls.py` (located in the main folder!) and include a path to your app there:
   *
   * Note that {app\_name} should be replaced with your app's name.
4. Create file `urls.py` inside your app folder
   *
   * We create a variable called `urlpatterns` in which we state names of our directories. `views.index` calls index function from `views.py` to be executed therefore creating some output response for HTTP request.
   * For example, if we are willing to create a directory called "archive", with function "main", we would include this in urls.py:
     * `path('archive/', views.main, name ='main')`
   * NOTE: Paths with blank directory ('') are going to call the function whenever the app is accessed at https://IP/{app\_name}; any other directories are going to extend the link, for example, the archives directory I used above would be located in `https://IP/articles/archive`.
   * `views.py` is responsible for carrying out functions which are called using urls.py
5. Now let's create a simple HTTP response function in `views.py` for our app.
   *
6. Migrate your changes by running `python3 manage.py migrate`
   * Your app is now located in the https://IP:8000/{app\_name}

***

### Templates

Create a folder named templates in your app's folder and place a file named `base.html` into it. Base.html is going to play a role of a simply configured HTML example which in the long run, allows us to omit work with HTML.

Content of base.html is pretty basic and stays the same most of the time:&#x20;

Now, create some another blank HTML file (index.html) and include this code in it:&#x20;

It uses base.html as its basis and allows us to input any simple or slightly HTML-marked text in-between `<div data-gb-custom-block data-tag="extends" data-0='base.html'></div> and </div>`.

***
