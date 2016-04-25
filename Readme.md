Heroku buildpack: Python, Numpy, and Scipy (Python 2.7 only)
=======
Caution
=======

XICA specific work around is added on this version.


Heroku buildpack: Python, Numpy, and Scipy
====================================================

This is a custom [Heroku buildpack](http://devcenter.heroku.com/articles/buildpacks)
for Python apps that use NumPy and/or SciPy, powered by [pip](http://www.pip-installer.org/).

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
  * 1.9.1
  * 1.9.2

SciPy:
  * 0.13.3 (compiled against NumPy 1.9.0)
  * 0.14.0 (compiled against NumPy 1.8.1)
  * 0.15.1 (compiled against NumPy 1.9.2)

Note: SciPy should be compiled against the right minor version of NumPy, but
the patch version doesn't matter, e.g., SciPy 0.15.1 can be compiled against
1.9.0 or 1.9.1, but probably not 1.8. I checked every single case though --
you should run tests (`numpy.test()` or `scipy.test()`) if you aren't sure
that things will work.

This package will also install compiled runtime libraries for BLAS, LAPACK,
ATLAS, and Fortran, which are needed by NumPy and SciPy at runtime.

### Known Issues and Todos

  1. Scikit-learn can be installed, but may not pass all tests. For example,
     scikit-learn 0.14.1 installed with NumPy 1.9.0 and SciPy 0.13.3 did not
     pass all tests. You can see the failed tests in [this issue][issue9].
     Another user [reported][issue11] that scikit-learn 0.15.2 installed fine, although
     he did not post any test results.
  2. This buildpack may not work well with Multipack apps (e.g., see [this
     issue][issue15]).
  3. I was getting some minor test failures for NumPy 1.9.2 that I wasn't able
     to resolve. See more information [here][issue19]. Please contact me if
     you have a problem related to this.
  4. This buildpack currently only works for Python 2.7. Support for Python 3.4
     will come whenever I have some free time to work on it (or if there is a
     pull request).

[issue9]: https://github.com/thenovices/heroku-buildpack-scipy/issues/9#issuecomment-61660727
[issue11]: https://github.com/thenovices/heroku-buildpack-scipy/issues/11#issuecomment-85143132
[issue15]: https://github.com/thenovices/heroku-buildpack-scipy/issues/15
[issue19]: https://github.com/thenovices/heroku-buildpack-scipy/issues/19

If any of these issues are immediately impacting you, please open a Github
issue so that I know that they are higher priority items.

Usage
-----
For a new app:

    heroku create --buildpack https://github.com/thenovices/heroku-buildpack-scipy

For an existing app:

    heroku buildpacks:set https://github.com/thenovices/heroku-buildpack-scipy

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
    $ echo -e "numpy==1.9.2\nscipy==0.15.1" > requirements.txt
    $ git add requirements.txt
    $ git commit -m 'Added requirements'
    $ git push heroku master


Acknowledgments
---------------

This fork is taken from @dbrgn -- I owe thanks to him, @wyn, and others for
setting up a lot of the code here.
