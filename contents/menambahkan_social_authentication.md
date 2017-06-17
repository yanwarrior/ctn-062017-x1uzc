# Menambahkan Social Authentication

Pada command line, ketik perintah berikut untuk menginstal package `social-auth-app-django`:

```txt
pip install social-auth-app-django==1.1.0
```

Kemudian tambahkan `social_django` ke dalam `INSTALLED_APPS` di dalam file `bookmarks/settings.py`:

```python
INSTALLED_APPS = [
    # ...
    'social_django',
]
```

Pada bagian pengaturan `TEMPLATES`, tambahkan dua `context processor` di bagian `context_processors` seperti berikut ini:

```python
TEMPLATES = [
    {
        # ...
        'OPTIONS': {
            # ...
            'context_processors': [
                # ...
                'social_django.context_processors.backends',
                'social_django.context_processors.login_redirect',
                # ...
            ]
        }
    }
]
```

Sekarang jalankan perintah berikut untuk sinkroniasi model `social-auth-app-django` dengan database Anda:

```txt
python manage.py migrate
```

Anda harus melihat hasil migrasi untuk aplikasi default sebagai berikut:

```txt
Applying default.0001_initial... OK
Applying default.0002_add_related_name... OK
Applying default.0003_alter_email_max_length... OK
```

Buka file `bookmarks/urls.py` dan tambahkan pola URL berikut ini:

```python
urlpatterns = [
    # ...
    url(r'^social-auth/', 
        include('social_django.urls', 
                namespace='social')),
]
```

**Windows 10**

Buka file `C:\Windows\System32\drivers\etc\hosts` dan tambakan baris berikut ke dalamnya:

```txt
127.0.0.1 mysite.com
```

**Linux/Unix**

Buka file `/etc/hosts` dan tambakan baris berikut ke dalamnya:

```txt
127.0.0.1 mysite.com
```



