Caution
=======

XICA specific work around is added on this version.


Heroku buildpack: Python, Numpy, and Scipy
====================================================

This is a custom [Heroku buildpack](http://devcenter.heroku.com/articles/buildpacks)
for Python apps that use NumPy and/or SciPy, powered by [pip](http://www.pip-installer.org/).

Note: This buildpack currently only supports the 'classic' cedar stack. It
does not yet support the cedar-14 stack, but has plans to do so in the
future.

Please open a GitHub for any problems encountered or feature requests.
If are using this project and found it useful, please let me know! (Preferably
by email: brandon.k.liu@gmail.com). I maintain this project on my spare time,
and I am much more motivated to work on it if I know there are people who are
benefiting.

Details
-------

This buildpack currently supports:

NumPy:
  * 1.6.2
  * 1.7.2
  * 1.8.1
  * 1.8.2
  * 1.9.0

SciPy:
  * 0.13.3 (compiled against NumPy 1.9.0)
  * 0.14.0 (compiled against NumPy 1.8.1)

This package will also install compiled runtime libraries for BLAS, LAPACK,
ATLAS, and Fortran, which are needed by NumPy and SciPy at runtime.

### Known Issues and Todos

  1. Currently, SciPy will only work with the specific version of NumPy
     against which it was compiled (e.g., SciPy 0.14.0 with NumPy 1.8.1).
  2. Scikit-learn can be installed, but may not pass all tests. For example,
     scikit-learn 0.14.1 installed with NumPy 1.9.0 and SciPy 0.13.3 did not
     pass all tests. You can see the failed tests in [this issue][issue9].
  3. The cedar-14 stack is not supported.

[issue9]: https://github.com/thenovices/heroku-buildpack-scipy/issues/9#issuecomment-61660727

If any of these issues are immediately impacting you, please open a Github
issue so that I know that they are higher priority items.

Usage
-----
For a new app:

    heroku create --buildpack https://github.com/thenovices/heroku-buildpack-scipy

For an existing app:

    heroku config:set BUILDPACK_URL=https://github.com/thenovices/heroku-buildpack-scipy

You must specify your exact desired version in `requirements.txt` (e.g.,
`numpy==1.9.0`). If no version is specified, the latest version available will
be used. At this time, this buildpack does not support requirements of the
form `numpy>=1.8`.

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


Acknowledgments
---------------

This fork is taken from @dbrgn -- I owe thanks to him, @wyn, and others for
setting up a lot of the code here.
