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

Buatlah direktori baru bernama `registration` di dalam folder `account/templates/`. Di dalam direktori `registration` buatlah file bernama `login.html` dan tambahkan kode berikut ini ke dalamnya:

```html
{% extends "base.html" %}

{% block title %}Log-in{% endblock %}

{% block content %}
<h1>Log-in</h1>
{% if form.errors %}
<p>
    Your username and password didn't match.
    Please try again.
</p>
{% else %}
<p>Please, use the following form to log-in:</p>
{% endif %}

<div class="login-form">
    <form action="{% url 'login' %}" method="post">
        {{ form.as_p }}
        {% csrf_token %}
        <input type="hidden" name="next" value="{{ next }}" />
        <p><input type="submit" value="Log-in"></p>
    </form>
</div>
{% endblock %}
```

Sekarang buat lagi file template bernama `logged_out.html` dan simpan di dalam direktori `account/templates/registration/` dan buat file tersebut terlihat seperti ini:

```html
{% extends "base.html" %}

{% block title %}Logged out{% endblock %}

{% block content %}
<h1>Logged out</h1>
<p>
    You have been successfully logged out. 
    You can <a href="{% url 'login' %}">log-in again</a>.
</p>
{% endblock %}
```

Buka file `account/views.py` dan tambahkan kode berikut ini ke dalamnya:

```python
from django.contrib.auth.decorators import login_required


@login_required
def dashboard(request):
    return render(request, 
                  'account/dashboard.html',
                  {'section': 'dashboard'})
```

Sekarang buatlah file template `account/templates/account/dashboard.html` dan buatlah file tersebut terlihat seperti ini:

```html
{% extends "base.html" %}

{% block title %}Dashboard{% endblock %}

{% block content %}
<h1>Dashboard</h1>
<p>Welcome to your dashboard.</p>
{% endblock %}
```

Kemudian, tambahkan pola URL untuk view yang sudah kita buat di dalam file `account/urls.py`:

```python
urlpatterns = [
    # ...
    url(r'^$', views.dashboard, name='dashboard'),
]
```

Edit file `bookmarks/settings.py` dan tambahkan kode berikut ini ke dalam file tersebut:

```python
from django.core.urlresolvers import reverse_lazy

LOGIN_REDIRECT_URL = reverse_lazy('dashboard')
LOGIN_URL = reverse_lazy('login')
LOGOUT_URL = reverse_lazy('logout')
```

Edit file `account/templates/base.html` dan modifikasi element `<div>` yang memiliki ID `header` menjadi seperti ini:

```html
<div id="header">
    <span class="logo">Bookmarks</span>
    
    {% if request.user.is_authenticated %}
    <ul class="menu">
        <li {% if section == "dashboard" %}class="selected"{% endif %}>
            <a href="{% url "dashboard" %}">My dashboard</a>
        </li>
        <li {% if section == "images" %}class="selected"{% endif %}>
            <a href="#">Images</a>
        </li>
        <li {% if section == "people" %}class="selected"{% endif %}>
            <a href="#">People</a>
        </li>
    </ul>
    {% endif %}
    <span class="user">
        {% if request.user.is_authenticated %}
        Hello {{ request.user.first_name }},
        <a href="{% url "logout" %}">Logout</a>
        {% else %}
        <a href="{% url "login" %}">Log-in</a>
        {% endif %}
    </span>
</div>
```

Sekarang, akses URL `http://127.0.0.1:8000/account/login/` di browser kamu. Akan muncul halaman login. Lakukan login.

ketika login berhasil, kamu akan di bawa ke halaman dashboard seperti pada gambar di bawah ini:

![](../images/5.JPG)

Klik link **Logout** untuk keluar. Akan tampil halaman seperti gambar berikut ini:

![](../images/6.JPG)





