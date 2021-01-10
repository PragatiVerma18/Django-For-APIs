## Default Authentication in DRF

- **DEFAULT_PERMISSION_CLASSES:** AllowAny
- **DEFAULT_AUTHENTICATION_CLASSES:** SessionAuthentication and BasicAuthentication. 

```python
REST_FRAMEWORK = {
    'DEFAULT_PERMISSION_CLASSES': [
        'rest_framework.permissions.IsAuthenticated',
    ],
    'DEFAULT_AUTHENTICATION_CLASSES': [  # new
        'rest_framework.authentication.SessionAuthentication',
        'rest_framework.authentication.BasicAuthentication'
    ],
}
```

#### Why use both methods?
- Sessions are used to power the Browsable API and the ability to log in and log out of it.
- BasicAuthentication is used to pass the session ID in the HTTP headers for the API itself.

## Implementing token authentication

The first step is to update our `DEFAULT_AUTHENTICATION_CLASSES` setting to use `TokenAuthentication` as follows:

```python
REST_FRAMEWORK = {
    'DEFAULT_PERMISSION_CLASSES': [
        'rest_framework.permissions.IsAuthenticated',
    ],
    'DEFAULT_AUTHENTICATION_CLASSES': [
        'rest_framework.authentication.SessionAuthentication',
        'rest_framework.authentication.TokenAuthentication',  # new
    ],
}

```

- We keep SessionAuthentication since we still need it for our Browsable API, but now use tokens to pass authentication credentials back and forth in our HTTP headers.
- We also need to add the `authtoken` app which generates the tokens on the server. It comes included with Django REST Framework but must be added to our `INSTALLED_-
APPS` setting.

```python
'rest_framework.authtoken',
```

## Django-Rest-Auth
To create API endpoints so user can log in, log out, and reset password.

- Install the `django-rest-auth` package
```python
pip install django-rest-auth
```
- Add the new app to the `INSTALLED_APPS` config in settings.py
```python
'rest_auth',
```
- Set the routes in urls.py
```python
path('api/v1/rest-auth/', include('rest_auth.urls')), 
```

#### User Registration
Traditional Django does not ship with built-in views or URLs for user registration and neither does Django REST Framework. 

A popular approach is to use the third-party package **django-allauth** which comes with user registration as well as a number of additional features to the Django auth system such as social authentication via Facebook, Google, Twitter, etc.

- Install the `django-allauth` package
```python
pip install django-allauth
```

- Update the `INSTALLED_APPS` settings
```python
'django.contrib.sites',
'allauth',
'allauth.account',
'allauth.socialaccount',
'rest_auth.registration',
```
- Make sure to also include `EMAIL_BACKEND` and `SITE_ID`. 

> **Note:** Technically it does not matter where in the settings.py file they are placed, but it’s common to add additional configs like that at the bottom.

```python
EMAIL_BACKEND = 'django.core.mail.backends.console.EmailBackend' # new
SITE_ID = 1 # new
```

> **Note:**
> - The email back-end config is needed since by default an email will be sent when a new user is registered, asking them to confirm their account. Rather than also set up an email server, we will output the emails to the console with the console.EmailBackend
setting.

> - `SITE_ID` is part of the built-in Django “**sites**” framework which is a way to host multiple websites from the same Django project. We obviously only have one site we are working on here but django-allauth uses the sites framework, so we must specify
a default setting.

- Add URL route for registration
```python
path('api/v1/rest-auth/registration/', include('rest_auth.registration.urls')),
```
---
