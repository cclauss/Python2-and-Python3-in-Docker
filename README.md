# Python2-and-Python3-in-Docker

## Creates a single Docker container lets you run both Python 2.7.13 and Python 3.7.1

TL;DR:`$ docker build -t python-2-and-3 .`

Starts with`python:3.7.1-alpine`and then installs most of`python:2.7.13-alpine`on top
to allow you to choose either Python version at runtime via: python2, python3, pip2, pip3

NOTE: *site-packages are separate* so`pip2 install pkgname`does **not** make`pkgname`available to Python 3.
This means that you would also need to`pip3 install pkgname`to make`pkgname`accessable from both versions of Python.

```sh
$ mkdir python-2-and-3
$ cd python-2-and-3

# <put `Dockerfile` into that directory...>
$ docker build -t python-2-and-3 .
$ docker images  # python-2-and-3 should be at the top of the list

# Do some optional interactive testing...
$ docker run -it python-2-and-3 /bin/sh
\# python  -V  # Python 2.7.13
\# python2 -V  # Python 2.7.13
\# python3 -V  # Python 3.6.0

\# pip  -V     # pip 9.0.1 from /usr/local/lib/python2.7/site-packages (python 2.7)
\# pip2 -V     # pip 9.0.1 from /usr/local/lib/python2.7/site-packages (python 2.7)
\# pip3 -V     # pip 9.0.1 from /usr/local/lib/python3.6/site-packages (python 3.6)

\# SCRIPT="import platform ; print(platform.python_version())"
\# python  -c "$SCRIPT"  # 2.7.13
\# python2 -c "$SCRIPT"  # 2.7.13
\# python3 -c "$SCRIPT"  # 3.6.0

\# exit
$
```
