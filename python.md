Python
======

Python Install
--------------

### 설치
```
$ curl -O https://bootstrap.pypa.io/get-pip.py
$ setx PATH C:\Python27;C:\Python27\Scripts
$ python get-pip.py
$ pip install Django
```

### 설치확인
```
$ python 
>>> import django
>>> print django.get_version()
1.7
```