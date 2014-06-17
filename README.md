Heroku buildpack: Python, Numpy, Scipy, Scikit-learn
====================================================

This is a [Heroku buildpack](http://devcenter.heroku.com/articles/buildpacks)
for Python apps, powered by [pip](http://www.pip-installer.org/).

This custom buildpack supports NumPy 1.8.1 and SciPy 0.14.0 installations.

Differences to other forks
--------------------------

This fork is taken from @dbrgn -- I owe thanks to him, @wyn, and others for
setting up a lot of the code here.

In contrast to other forks, this buildpack does not require a `setup.py`, it
works with a normal `requirements.txt` file. Additionally, it is based on the
current version of the heroku-buildpack-python. This means that it uses a
current version of pip, which gets rid of some stack traces in the deploy log.

Setup, Usage
------------

NOTE: This buildpack only supports:

- NumPy 1.8.1
- SciPy 0.14.0

This buildpack is currently very simple in that it will install *only* these
versions, even if you specify a different version in requirements.txt. This
can be improved in the future if there is enough interest.

If you desire older NumPy or SciPy packages, please take a look at
https://github.com/dbrgn/heroku-buildpack-python-sklearn

Then specify the buildpack as usual. For a new app:

    heroku create --buildpack https://github.com/thenovices/heroku-buildpack-scipy

For an existing app:

    heroku config:set BUILDPACK_URL=https://github.com/thenovices/heroku-buildpack-scipy

Demo
----

    $ mkdir testheroku
    $ cd testheroku
    $ git init
    $ heroku create --buildpack https://github.com/thenovices/heroku-buildpack-scipy
    $ echo -e "numpy==1.8.1\nscipy==0.14.0" > requirements.txt
    $ git add requirements.txt
    $ git commit -m 'Added requirements'
    $ git push heroku master
