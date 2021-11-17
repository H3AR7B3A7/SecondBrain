# Django
_Django_ is a high-level [[Python]] web framework that encourages rapid development and clean, pragmatic design.

### Setup
[Python](https://docs.python.org/3.7/) 3.7.9 | [Django](https://docs.djangoproject.com/en/3.1/) 3.1.3

See [here](https://www.youtube.com/watch?v=KcM5ont7jy4) how to start a project using PyCharm.
All we have to do is migrate the database by running 'manage.py migrate' in the console and press 'Run...'  
However, migrating the database isn't that important yet because we are not using it yet.

## Creating a Project with CLI 
- **python -m venv "C:\...\projectname"**
- **.\Scripts\activate**
- **pip install django**
- **mkdir src**
- **cd src**
- **django-admin startproject projectname .**
- **python manage.py migrate**
- **python manage.py runserver**

(Specify python and django versions if not using system defaults!)
- **Ctrl + C**, to shut down server
- **deactivate**, to leave virtual environment

## Creating Super User
**manage.py createsuperuser**
Username: admin
Password: pass

To delete using the shell:
> python manage.py shell
> from django.contrib.auth.models import User
> User.objects.get(username="joebloggs", is_superuser=True).delete()

In our development db this password isn't important, but when we add a db for production we will use a stronger password.

## Creating a Basic App
**manage.py startapp name**

- Create model in models.py
- **manage.py makemigrations**
- **manage.py migrate**
- Add *'products'* to installed apps in *settings.py*

In *'admin.py'*:

    from .models import Product
    admin.site.register(Product)

We can now add products on: http://127.0.0.1:8000/admin/products/product/

### In the shell
> python manage.py shell
> from products.models import Product
> Products.objects.create(title="Product Name",price="10")
> Product.objects.all()

## HttpResponse
For a simple response we can import HttpResponse and add a function to *'views.py'* in the project folder:

    from django.http import HttpResponse

    def home_view(*args, **kwargs):
        return "<h1>Hello World</h1>"

Then we need to add to *'urls.py'*:

    from DjangoCourse import views

    urlpatterns = [
        path('', views.index, name='index'),
        path('admin/', admin.site.urls),
    ]

## Templating
To respond with templates we use the *render* import:

    from django.shortcuts import render

    def index(request, *args, **kwargs):
        return render(request, "index.html")

And we can create our templates in the *'templates'* folder. If we aren't using PyCharm we might have to configure 
the templates folder in *settings.py*, like this:

    'DIRS': [BASE_DIR / 'templates']

or with an *'os'* import:

    'DIRS': [os.path.join(BASE_DIR, "templates")]

## Template Inheritance
We can create a *'base'-template* to inherit from when creating pages. 
To indicate where our content will go, we use the following tags within this base template:

    {% block content %}{% endblock %}

Likewise we will wrap our content pages with these tags and extend the *'base'-template* at the top of the page:

    {% extends 'base.html' %}

## Partials
We can also include partials in other pages with:

    {% include 'navbar.html' %}

## Static resources
At the top of the template where you want to import the static folder:

    {% load static %}

We then reference to the stylesheet like this (presuming the path = static/css/style.css):

    href="{% static 'css/style.css' %}"

Configure STATICFILES_DIRS in *'settings.py'* depending on where you want your static folder to be.  
In templates folder:

    STATICFILES_DIRS = [BASE_DIR / 'templates/static']

In project directory:

    STATICFILES_DIRS = [BASE_DIR / 'static']

Or similarly with an os import:

    STATICFILES_DIRS = [os.path.join(BASE_DIR, 'templates/static')]

[Official documentation](https://docs.djangoproject.com/en/3.1/howto/static-files/)

## Template Context
We can add context to our template in views.py:

    def index(request, *args, **kwargs):
        my_context = { "my_text": "Some text ...",
                       "my_list": [5, 6, 7, 8]}
        return render(request, "index.html", my_context)

Now we can output this context in *index.html* using the key in between handlebars:

    {{ my_text }}

    {% for item in my_list %}
        <li>{{ item }}</li>
    {% endfor %}

To add database entries of an app to our context:

    "list": Product.objects.all()

## Parameters
We can direct users to the details of just one object by fetching a parameter in the url:

    "object": Product.objects.get(id=request.GET['id'])

The link to this would be: *'/product/?id=1'*, 
which we could offer the user with something like this on the *'products'-page*:

    {% for item in list %}
    <li><a href="/product/?id={{ item.id }}">{{ item.title }}</a></li>
    {% endfor %}

## Filters
We can add simple 'filters' by adding them after a | *'pipe'*:

    {{ item.price|add:10 }}

[Built-in Tags / Filters](https://docs.djangoproject.com/en/3.1/ref/templates/builtins/)  
[Custom Tags / Filters](https://docs.djangoproject.com/en/3.1/howto/custom-template-tags/)

## Model Forms
We create a file *'forms.py'* in our app and write out a model:

    from django import forms
    from .models import Product

    class ProductForm(forms.ModelForm):
    class Meta:
        model = Product
        fields = [
            'title',
            'description',
            'price'
        ]

We import ProductForm from .forms in *'views.py'* and we add a function for our form:

    def product_form(request, *args, **kwargs):
        form = ProductForm(request.POST or None)
        if form.is_valid():
            form.save()
    
        context = {
            "form": form
        }
        return render(request, "product/form.html", context)

And then we create a template to go with that form:

    <form method="post"> {% csrf_token %}
        {{ form.as_p }}
        <input type="submit" value="Save">
    </form>

We can have more control over our forms by using *'Form'* instead of *'ModelForm'*. 
An example of this was included inside the project. 
Both forms are fully styled and exactly the same, for a good comparison.

## Redirect
To redirect *from django.shortcuts import redirect* and:

    return redirect('/products')

## Form Validation
There are default validations using Django. We can make our own validations too though:

    def clean_title(self, *args, **kwargs):
        title = self.cleaned_data.get('title')
        if "CFE" not in title:
            raise forms.ValidationError("This is not a valid title")
        else:
            return title

## Update Form
We can make a form to update our products using the same form template by tweaking the form function a little:

    def update_form(request):
        obj = Product.objects.get(id=request.GET['id'])
        initial_data = {
            'title': obj.title,
            'description': obj.description,
            'price': obj.price
        }
        form = ProductForm(request.POST or None, initial=initial_data, instance=obj)
        if form.is_valid():
            form.save()
            return redirect('/products')
        context = {
            "form": form
        }
        return render(request, "product/form.html", context)

And we just give this function to a new url in *'urls.py'*

## Parameters
Instead of using default params getting them from the request that are passed like this:  
*'/product/?id=1'*  
We can create our url in *'urls.py'* a little different:

    path('update/<int:product_id>', update_form, name='updateform'),

When we do it this way, we can make our urls look a little cleaner:  
*'/product/1'*  
And we simply get our object like this:

    obj = Product.objects.get(id=product_id)

## 404: Page Not Found
When we enter an invalid product id as parameter we get a user unfriendly exception. 
To solve this we import get_object_or_404 from django.shortcuts and get our object like this instead:

    obj = get_object_or_404(Product, id=product_id)

Now we will get the 404 response we all know and love.  
Another way to achieve this would be to import *'Http404'* from django.http and fetch the object in a *'try'-block*:

    try:
        obj = Product.objects.get(id=product_id)
    except Product.DoesNotExist:
        raise Http404

## Delete Form / Button
Our link to delete looks similar to the one to update:

    path('delete/<int:product_id>', delete_product, name='delete_product'),

our function is rather simple but we want ot to be a post with CSRF-token:

    def delete_product(request, product_id):
        obj = get_object_or_404(Product, id=product_id)
        if request.method == "POST":
            obj.delete()
        return redirect('/products')

And finally our form will look something like this:

    <form id="del-form" action="/delete/{{ item.id }}" method="post">
        {% csrf_token %}
        <input type="submit" value="Delete">
    </form>

It will basically just be a button in a form with POST as method.

## Absolute path
To make our apps reusable we have some cleanup/work to do. 
One of the things we will want to make use of is absolute paths. 
For this we import reverse from django.urls and create following function in *'model.py'*:

    def get_absolute_url(self):
        return reverse("products-detail", kwargs={"product_id": self.id})

Now we can simply refer to our object urls with: 

    {{ product.get_absolute_url }}

Inside the project we can see we moved the products-app related urls inside its own *'urls.py'* 
and named the app so we can use a namespace:

    def get_absolute_url(self):
        return reverse("products:products-detail", kwargs={"product_id": self.id})

## Error handling - Custom error page
- Create a 404.html view
- In *'urls.py'*:

    handler404 = 'DjangoCourse.views.error_404_view'

- In *'views.py'*:

    def error_404_view(request, exception):
        return render(request, "404.html")

### 500 error when debug is off
We will need to set DEBUG = False in *'settings.py'* to see the effect of our changes.
For this to work we will need to disable django compression and run collectstatic.

- Run the following in console:
>python manage.py collectstatic 
- Add the following line to *'settings.py'*:

    COMPRESS_ENABLED = os.environ.get('COMPRESS_ENABLED', False)

## Settings Profiles
To have settings for different environments we can make a copy of *'settings.py'* and name it 
*'test_settings.py'*. We can then specify the file we want to use with the following environment variable:

    DJANGO_SETTINGS_MODULE=djangoProject.test_settings
    
In PyCharm we can simply change the environment variable in *'Edit configurations...'*. 
If we want to change the default name, we can do this in wsgi.py. 
We can also import a base settings file to avoid duplicate code.

## Heroku Deployment
In terminal:
>pip install gunicorn  
>pip install django-heroku  
>pip freeze > requirements.txt

Add file to root named:
Procfile
    
    web: gunicorn mysite-project.wsgi:application --log-file - --log-level debug
    python manage.py collectstatic --noinput
    manage.py migrate

*Edit 'settings.py'*:

    import django_heroku
    import dj_database_url
    ...
    ALLOWED_HOSTS = ['*']
    ...
    # DATABASES = {
    #     'default': {
    #         'ENGINE': 'django.db.backends.sqlite3',
    #         'NAME': BASE_DIR / 'db.sqlite3',
    #     }
    # }
    
    DATABASES = {
        'default': dj_database_url.config()
    }
    ...
    django_heroku.settings(locals())

- Install Heroku toolbelt
- Login to Heroku:
    
    heroku login

- Create an application on Heroku:

    heroku create heroku rename name

- Add SSL protection to the project:

    heroku keys:add

- Add remote

    git remote add projectname ~git url from heroku~.git

- Push the application to heroku:

    git push projectname master
    
- Create db on heroku

    heroku addons:create --app projectname heroku-postgresql:hobby-dev

- Migrate

    heroku run manage.py migrate
    
To get logs from Heroku:
>heroku logs --app projectname --tail



---
#Python 