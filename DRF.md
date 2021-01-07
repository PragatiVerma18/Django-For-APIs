# Django Rest Framework 

Django creates websites containing webpages, while Django REST Framework creates web APIs which are a collection of URL endpoints containing available HTTP verbs that return JSON.

> `wsgi.py` stands for web server gateway interface and helps Django serve the eventual web pages

There are three main steps to convert your database models into a RESTful API are:
- a `urls.py` file for the URL routes
- a `serializers.py` file to transform the data into JSON
- a `views.py` file to apply logic to each API endpoint

## Serializers
A serializer translates data into a format that is easy to consume over the internet, typically JSON, and is displayed at an API endpoint.

**NOTES:**

> - Always add a `__str__` method to provide a human-readable name for each future model instance.
> - Migration files are a fantastic way to debug applications and you should strive to create a migration file for each small change. If we had updated the models in two different apps and then run python manage.py makemigrations the resulting single migration file would contain data on both apps. That just makes debugging harder. Try to keep your migrations as small as possible.

## CORS - Cross-Origin Resource Sharing
Whenever a client interacts with an API hosted on a different domain (mysite.com vs yoursite.com) or port (localhost:3000 vs localhost:8000) there are 
potential security issues.

Specifically, CORS requires the server to include specific HTTP headers that allow for the client to determine if and when cross-domain requests should be allowed.

The easiest way to handle this–-and the one recommended by Django REST Framework–-is to use middleware that will automatically include the appropriate HTTP headers based on our settings.

We use `django-cors-headers`:
- add `corsheaders` to the `INSTALLED_APPS`
- **add `CorsMiddleware` above `CommonMiddleWare` in `MIDDLEWARE`**
- create a `CORS_ORIGIN_WHITELIST`

**NOTE:**
> It’s very important that `corsheaders.middleware.CorsMiddleware` appears in the proper location. That is above `django.middleware.common.CommonMiddleware` in the `MIDDLEWARE` setting since middlewares are loaded **top-to-bottom**.

## Permissions
Django REST Framework ships with several out-of-the-box permissions settings that we can use to secure our API. These can be applied at a **project-level**, a **view-level**, or at any **individual model level**.

> ## Add log in to the browsable API
> This is such a common occurrence that Django REST Framework has a one-line setting to add log in and log out directly to the browsable API itself.

> Within the project-level `urls.py` file, add a new URL route that includes `rest_framework.urls`. Somewhat confusingly, the actual route specified can be anything
we want; what matters is that `rest_framework.urls` is included somewhere.
 
**Code:**
```python
# blog_project/urls.py
from django.urls import include, path

urlpatterns = [
  ...
  path('api-auth/', include('rest_framework.urls')), # new
]
```

### Project-Level Permissions

Django REST Framework ships with a number of built-in project-level permissions settings we can use, including:

- **AllowAny** - any user, authenticated or not, has full access
- **IsAuthenticated** - only authenticated, registered users have access
- **IsAdminUser** - only admins/superusers have access
- **IsAuthenticatedOrReadOnly** - unauthorized users can view any page, but only authenticated users have write, edit, or delete privileges

Implementing any of these four settings requires updating the `DEFAULT_PERMISSION_CLASSES` setting:
```python
# blog_project/settings.py

REST_FRAMEWORK = {
  'DEFAULT_PERMISSION_CLASSES': [
      'rest_framework.permissions.IsAuthenticated', # new
  ]
}
```

## Note:
> - If a request contains HTTP verbs included in `SAFE_METHODS` – a tuple containing `GET`, `OPTIONS`, and `HEAD` –then it is a read-only request and permission is granted.
> - The generic views will only check the object-level permissions for views that retrieve a single model instance. If you require object-level filtering of list views–for a collection of instances–you’ll need to filter by overriding the initial queryset.

# Conclusion:

Setting proper permissions is a very important part of any API. As a general strategy, it is a good idea to set a strict project-level permissions policy such that only authenticated users can view the API. Then make view-level or custom permissions more accessible as needed on specific API endpoints.

---
