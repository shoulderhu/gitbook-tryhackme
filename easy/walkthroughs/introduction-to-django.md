# Introduction to Django

## :person\_running: Getting started

```bash
pip3 -m venv venv
source venv/bin/activate
```

```bash
pip3 install Django==2.2.12
django-admin startproject thm
cd thm/
python3 manage.py migrate
python3 manage.py runserver
python3 manage.py createsuperuser
```

### #1 **How would we create an app called Forms?**&#x20;

```bash
python3 manage.py startapp Forms
```

### #2 **How would we run our project to a local network?**

```
python3 manage.py runserver 0.0.0.0:8000
```

## :spider\_web: Creating a website

```
python3 manage.py startapp Articles

```

## Support Material

{% embed url="https://developer.mozilla.org/zh-TW/docs/Learn/Server-side/Django/skeleton_website" %}

