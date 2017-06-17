# Membuat View untuk Login dan Logout

Edit file `account/urls.py` dan buatlah menjadi seperti ini:

```python
from django.conf.urls import url
from django.contrib import auth
from . import views

urlpatterns = [
    # previous login view
    # url(r'^login/$', views.user_login, name='login'),
    
    # login / logout urls
    url(r'^login/$',
        auth.views.login,
        name='login'),
    url(r'^logout/$',
        auth.views.logout,
        name='logout'),
    url(r'^logout-then-login/$',
        auth.views.logout_then_login,
        name='logout_then_login'),
]
```

