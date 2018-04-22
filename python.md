Python
======

Installation
------------

Windows
```
setx PATH C:\Python27;C:\Python27\Scripts
```

PIP
---

Installing with get-pip.py
```
curl -O https://bootstrap.pypa.io/get-pip.py
python get-pip.py
```

Ubuntu
```
sudo apt install python-pip
```

Upgrading pip
```
pip install -U pip
```

Virtual Environment
-------------------

> python -m venv <venv_path>

```
python -m venv test

# 윈도우의 경우
tree /f test
```

Reference
---------

1. [https://pip.pypa.io](https://pip.pypa.io)
1. [Python 3.6.5 documentation](https://docs.python.org/3/)
