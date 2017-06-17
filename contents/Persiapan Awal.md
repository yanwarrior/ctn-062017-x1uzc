# Persiapan Awal

**Membuat dan Mengaktifkan Virtual Environment**

Jalankan perintah berikut ini untuk membuat virtual environment dengan nama `myenv`:

```
python -m venv myenv
```

Aktifkan `myenv` dengan perintah:

```
myenv\Scripts\activate
```

**Instalasi Django**

Pastikan virtual environment sudah aktif. 

Jalankan perintah berikut ini untuk menginstal `Django` di versi `1.11.2`:

```
pip install Django==1.11.2
```

**Membuat Workspace**

Buat folder workspace bernama `bookmarks`:

```
mkdir bookmarks
```

Masuk ke direktori `bookmarks`:

```
cd bookmarks
```

**Membuat Project dan Aplikasi**

Pastikan kita sudah ada di dalam direktori `bookmarks`.

Ketik perintah berikut untuk membuat project Django bernama `bookmarks`:

```
django-admin startproject bookmarks .
```

Ketik perintah berikut untuk membuat aplikasi Django bernama `account`:

```
python manage.py startapp account
```

**Aktifasi Aplikasi account**

Buka file `bookmarks/settings.py` dan tambahkan `account` di dalam pengaturan `INSTALLED_APPS` di paling pertama:

```python
INSTALLED_APPS = (
    'account',
    # ...
)
```

Lakukan migrasi pertama:

```
python manage.py migrate
```

[Kembali](./README.md)

