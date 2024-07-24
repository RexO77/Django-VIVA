### Module 1: Django Basics and Architecture

1. **What is Django?**
   - Django is a high-level Python web framework that encourages rapid development and clean, pragmatic design.

2. **What is a web framework?**
   - A web framework is a software framework designed to support the development of web applications including web services, web resources, and web APIs.

3. **What is MVC architecture?**
   - MVC stands for Model-View-Controller. It is a design pattern that separates an application into three interconnected components: Model (data), View (UI), and Controller (logic).

4. **What is MVT architecture in Django?**
   - MVT stands for Model-View-Template. It is Django's implementation of the MVC pattern, where the template is used for the user interface.

5. **What are the features of Django framework?**
   - Django is known for its ORM, admin interface, scalability, security features, and extensive documentation.

6. **What is URLConf?**
   - URLConf (URL Configuration) is a mapping between URL patterns and view functions in Django.

7. **What is HttpResponse?**
   - HttpResponse is a class in Django that allows you to send an HTTP response back to the client.

8. **What is a stateless protocol?**
   - A stateless protocol does not retain any information about previous requests. HTTP is a stateless protocol.

9. **Give an example of `urls.py`.**
   ```python
   from django.urls import path
   from . import views

   urlpatterns = [
       path('', views.home, name='home'),
       path('about/', views.about, name='about'),
   ]
   ```

10. **What is the difference between 2-tier and 3-tier architecture?**
    - 2-tier architecture involves a client and a server, while 3-tier architecture includes a client, an application server, and a database server.

### Module 2: Django Views and Templates

1. **What is a template in Django?**
   - A template is a text file that defines the structure or layout of a file (such as an HTML page), allowing dynamic content to be inserted.

2. **Explain how to use for loop and if condition inside templates.**
   ```html
   {% for item in items %}
       {% if item.is_active %}
           {{ item.name }}
       {% endif %}
   {% endfor %}
   ```

3. **What is meant by context in Django?**
   - Context is a dictionary-like object that maps template variable names to Python objects.

4. **How to render a template with context in Django?**
   ```python
   from django.shortcuts import render
   def my_view(request):
       context = {'key': 'value'}
       return render(request, 'template.html', context)
   ```

5. **What is context variable lookup in templates?**
   - Context variable lookup is the process of retrieving the value of a variable passed to a template from the context.

6. **List basic template tags.**
   - `{% for %}`, `{% if %}`, `{% block %}`, `{% extends %}`, `{% include %}`

7. **Explain `{% if %}` and `{% endif %}` with an example.**
   ```html
   {% if user.is_authenticated %}
       Hello, {{ user.username }}
   {% endif %}
   ```

8. **What is template inheritance?**
   - Template inheritance allows you to build a base template and extend it in other templates, promoting code reuse.

9. **How to include one template into another?**
   ```html
   {% include 'nav.html' %}
   ```

10. **Explain `{% for %}` and `{% endfor %}`.**
    ```html
    {% for item in items %}
        {{ item.name }}
    {% endfor %}
    ```

### Module 3: Django Models and ORM

1. **What is a model in Django?**
   - A model is a Python class that represents a database table. It defines the structure of the database table, including field types and default values.

2. **Define a simple model class for a Book.**
   ```python
   from django.db import models

   class Book(models.Model):
       title = models.CharField(max_length=200)
       author = models.CharField(max_length=100)
       published_date = models.DateField()
   ```

3. **Explain the purpose of migrations in Django.**
   - Migrations are used to propagate changes made to the models (like adding a field) into the database schema.

4. **How to create and apply migrations?**
   ```bash
   python manage.py makemigrations
   python manage.py migrate
   ```

5. **How to query all objects of a model?**
   ```python
   books = Book.objects.all()
   ```

6. **How to filter objects in Django ORM?**
   ```python
   books = Book.objects.filter(author='John Doe')
   ```

7. **How to update an object in Django ORM?**
   ```python
   book = Book.objects.get(id=1)
   book.title = 'New Title'
   book.save()
   ```

8. **How to delete an object in Django ORM?**
   ```python
   book = Book.objects.get(id=1)
   book.delete()
   ```

9. **Explain the use of `__str__` method in a Django model.**
   - The `__str__` method defines a human-readable representation of the model instance, which is useful for displaying in the Django admin or shell.

10. **How to order querysets in Django ORM?**
    ```python
    books = Book.objects.all().order_by('published_date')
    ```

### Module 4: Django Forms and Validation

1. **What is a form in Django?**
   - A form in Django is a class that describes a form and its fields, and handles validation.

2. **How to create a simple form class in Django?**
   ```python
   from django import forms

   class ContactForm(forms.Form):
       subject = forms.CharField(max_length=100)
       email = forms.EmailField()
       message = forms.CharField(widget=forms.Textarea)
   ```

3. **How to validate a form in a view?**
   ```python
   def contact_view(request):
       if request.method == 'POST':
           form = ContactForm(request.POST)
           if form.is_valid():
               # Process form data
               pass
   ```

4. **What are widgets in Django forms?**
   - Widgets are the HTML form elements used to render the fields of a form.

5. **How to add custom validation to a form field?**
   ```python
   class ContactForm(forms.Form):
       subject = forms.CharField(max_length=100)
       email = forms.EmailField()

       def clean_email(self):
           email = self.cleaned_data.get('email')
           if not "@" in email:
               raise forms.ValidationError("Invalid email")
           return email
   ```

6. **Explain `form.as_p()` and `form.as_table()`.**
   - `form.as_p()` renders form fields as `<p>` elements, while `form.as_table()` renders them as table rows `<tr>`.

7. **What is the purpose of `cleaned_data` in form validation?**
   - `cleaned_data` is a dictionary that holds the validated form data after the `is_valid()` method is called.

8. **How to render form errors in a template?**
   ```html
   {{ form.errors }}
   ```

9. **How to use Django formsets?**
   - Formsets are a layer of abstraction to work with multiple forms on the same page.

10. **How to tie forms into views and templates?**
    ```python
    def my_view(request):
        if request.method == 'POST':
            form = MyForm(request.POST)
            if form.is_valid():
                # Process data
                pass
        else:
            form = MyForm()
        return render(request, 'template.html', {'form': form})
    ```

### Module 5: Django Deployment and Advanced Topics

1. **What is WSGI?**
   - WSGI (Web Server Gateway Interface) is a specification that describes how a web server communicates with web applications. Django uses WSGI for deployment.

2. **What is Docker and how can it be used with Django?**
   - Docker is a platform that packages applications and their dependencies into containers. It ensures consistent environments for development, testing, and deployment.

3. **What is Celery and how is it used with Django?**
   - Celery is an asynchronous task queue/job queue that is used to handle long-running tasks in Django.

4. **What is Django Channels and its use cases?**
   - Django Channels extend Django to handle WebSockets, chat protocols, IoT protocols, and other asynchronous protocols, enabling real-time applications.

5. **How to set up SSL for a Django application?**
   - Use a certificate from a trusted Certificate Authority (CA) and configure your web server (e.g., Nginx or Apache) to use SSL/TLS.

6. **How to serve static files in Django?**
   - Use the `django.contrib.staticfiles` app and configure the `STATIC_URL` and `STATICFILES_DIRS` settings.

7. **How to configure a database in Django?**
   - Set up the database in `settings.py` using the `DATABASES` dictionary.

8. **How to create a custom Django management command?**
   ```python
   from django.core.management.base import BaseCommand

   class Command(BaseCommand):
       def

 handle(self, *args, **options):
           self.stdout.write('Hello, world!')
   ```

9. **What is middleware in Django?**
   - Middleware is a way to process requests globally before they reach the view or after the view has processed them.

10. **What are signals in Django?**
    - Signals are a way to allow decoupled applications to get notified when certain actions occur elsewhere in the framework, like `post_save` and `pre_delete`.
