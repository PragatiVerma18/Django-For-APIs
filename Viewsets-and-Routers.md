# Viewsets and Routers

**Viewsets** and **routers** are tools within Django REST Framework that can speed-up API development. They are an additional layer of abstraction on top of views and URLs.

The primary benefit is that a single viewset can replace multiple related views. And a router can automatically generate URLs for the developer.

> **Note:** By using `get_user_model` we ensure that we are referring to the correct user model, whether it is the default User or a custom user model as is often defined in new Django projects.

## Viewsets
A **viewset** is a way to combine the logic for multiple related views into a single class. In other words, one viewset can replace multiple views.

The tradeoff is that there is a loss in readability for fellow developers who are not intimately familiar with viewsets. So it’s a trade-off.

```python
from django.contrib.auth import get_user_model
from rest_framework import viewsets 

from .serializers import UserSerializer

class UserViewSet(viewsets.ModelViewSet):  # new
    queryset = get_user_model().objects.all()
    serializer_class = UserSerializer

```

## Routers
Routers work directly with viewsets to automatically generate URL patterns for us.

Django REST Framework has two default routers: **SimpleRouter** and **DefaultRouter**.

```python
# posts/urls.py
from django.urls import path
from rest_framework.routers import SimpleRouter

from .views import UserViewSet

router = SimpleRouter()
router.register('users', UserViewSet, base_name='users')

urlpatterns = router.urls

```

## Conclusion
A good rule of thumb is to start with views and URLs. As your API grows in complexity if you find yourself repeating the same endpoint patterns over and over again, then look to viewsets and routers. Until then, keep things simple.

---

