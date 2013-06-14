Heroku buildpack: Python, Numpy, Scipy, Scikit-learn
====================================================

This is a [Heroku buildpack](http://devcenter.heroku.com/articles/buildpacks)
for Python apps, powered by [pip](http://www.pip-installer.org/).

Additionally, it adds support for Numpy, Scipy and Scikit-learn.

[![Build Status](https://secure.travis-ci.org/dbrgn/heroku-buildpack-python-sklearn.png?branch=master)](http://travis-ci.org/dbrgn/heroku-buildpack-python-sklearn)

Differences to other forks
--------------------------

This buildpack is strongly inspired by @wyn and @ToonTimbermont. In fact, I
copied a lot of code from them. It also uses binaries provided by @wyn. Thanks
a lot.

In contrast to their forks, this buildpack does not require a `setup.py`, it
works with a normal `requirements.txt` file. Additionally, it is based on the
current version of the heroku-buildpack-python. This means that it uses a
current version of pip, which gets rid of some stack traces in the deploy log.

Setup, Usage
------------

Specify the buildpack as usual. For a new app:

    heroku create --buildpack https://github.com/dbrgn/heroku-buildpack-python-sklearn/

For an existing app:

    heroku config:set BUILDPACK_URL=https://github.com/dbrgn/heroku-buildpack-python-sklearn/
