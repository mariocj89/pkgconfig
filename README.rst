pkgconfig
=========

.. image:: https://travis-ci.org/matze/pkgconfig.png?branch=master
    :target: https://travis-ci.org/matze/pkgconfig

``pkgconfig`` is a Python module to interface with the ``pkg-config``
command line tool for Python 3.3+.

It can be used to

-  find all pkg-config packages ::

       >>> packages = pkgconfig.list_all()

-  check if a package exists ::

       >>> pkgconfig.exists('glib-2.0')
       True

-  check if a package meets certain version requirements ::

       >>> pkgconfig.installed('glib-2.0', '< 2.26')
       False

-  return the version ::

       >>> pkgconfig.modversion('glib-2.0')
       '2.56.3'

-  query CFLAGS and LDFLAGS ::

       >>> pkgconfig.cflags('glib-2.0')
       '-I/usr/include/glib-2.0 -I/usr/lib/glib-2.0/include'

       >>> pkgconfig.libs('glib-2.0')
       '-lglib-2.0'

-  get all variables defined for a package::

        >>> pkgconfig.variables('glib-2.0')
        {u'exec_prefix': u'/usr'}

-  parse the output to build extensions with setup.py ::

       >>> d = pkgconfig.parse('glib-2.0 gtk+-2.0')
       >>> d['libraries']
       [u'gtk+-2.0', u'glib-2.0']

   or ::

       >>> ext = Extension('foo', ['foo.c'])
       >>> # sets extension attributes as needed
       >>> pkgconfig.configure_extension(ext, 'glib-2.0 gtk+-2.0')

   The ``pkgconfig.parse`` function returns a dictonary of lists.
   The lists returned are accurate representations of the equivalent
   ``pkg-config`` call's result, both in content and order.

If ``pkg-config`` is not on the path, raises ``EnvironmentError``.

The ``pkgconfig`` module is licensed under the MIT license.


Changelog
---------

Version 1.5.3
~~~~~~~~~~~~~

- Add ``configure_extension`` API

Version 1.5.2
~~~~~~~~~~~~~

- Update poetry dep
- Improve CI

Version 1.5.0
~~~~~~~~~~~~~

- Use poetry instead of setuptools directly
- Fix #42: raise exception if package is missing
- Fix version parsing for openssl-like version numbers, fixes #32
- Fix #31: expose --modversion
- Fix #30: strip whitespace from variable names

Version 1.4.0
~~~~~~~~~~~~~

- Add boolean ``static`` keyword to output private libraries as well
- Raise original ``OSError`` as well

Version 1.3.1
~~~~~~~~~~~~~

- Fix compatibility problems with Python 2.6

Version 1.3.0
~~~~~~~~~~~~~

- Add variables() API to query defined variables
- Disable Python 3.2 and enable Python 3.5 and 3.6 tests
- Fix #16: handle spaces of values in .pc files correctly

Version 1.2.1 and 1.2.2
~~~~~~~~~~~~~~~~~~~~~~~

Bug fix releases released on December 1st and 2nd 2016.

- Include the ``data`` folder in the distribution in order to run tests
- Improve the tests


Version 1.2.0
~~~~~~~~~~~~~

Released on November 30th 2016.

- Potential break: switch from result set to list
- Expose --list-all query
- Added support for PKG_CONFIG environment variable


Version 1.1.0
~~~~~~~~~~~~~

Released on November 6th 2013.

- Multiple packages can now be parsed with a single call to ``.parse``.


Version 1.0.0
~~~~~~~~~~~~~

First release on September 8th 2013.
