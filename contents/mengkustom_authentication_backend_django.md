# Mengkustom Authentication Backend Django

Buat file baru di dalam direktori aplikasi `accoun`t dengan nama `authentication.py`. Tambahkan kode berikut ke dalamnya:

```python
rom django.contrib.auth.models import User


class EmailAuthBackend(object):
    """
    Authenticate using e-mail account.
    """
    def authenticate(self, username=None, password=None):
        try:
            user = User.objects.get(email=username)
            if user.check_password(password):
                return user
            return None
        except User.DoesNotExist:
            return None
    
    def get_user(self, user_id):
        try:
            return User.objects.get(pk=user_id)
        except User.DoesNotExist:
            return None
```

Edit `bookmarks/settings.py` dan tambahkan pengaturan berikut ini:

```python
AUTHENTICATION_BACKENDS = (
    'django.contrib.auth.backends.ModelBackend',
    'account.authentication.EmailAuthBackend',
)
```

Sekarang buka `http://127.0.0.1:8000/account/login/` di browser Kamu. Lakukan login kembali menggunakan email dan password.