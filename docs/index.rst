.. doctest-skip-all

Astroquery
==========

This is the documentation for the Astroquery affiliated package of astropy_.

Code and issue tracker are on `GitHub <https://github.com/astropy/astroquery>`_.

Introduction
------------

Astroquery is a set of tools for querying astronomical web forms and databases.

There are two other packages with complimentary functionality as Astroquery:
`astropy.vo <http://docs.astropy.org/en/latest/vo/index.html>`_ is in the Astropy core and
`pyvo <https://pyvo.readthedocs.org/en/latest/>`_ is an Astropy affiliated package.
They are more oriented to general `virtual observatory <http://www.virtualobservatory.org>`_
discovery and queries, whereas Astroquery has web service specific interfaces.

Check out the :doc:`gallery` for some nice examples.

Installation
------------
Astroquery must be installed from source:

.. code-block:: bash

    $ git clone git@github.com:astropy/astroquery.git
    $ cd astroquery
    $ python setup.py install

pip install also works:

.. code-block:: bash

    $ pip install git+http://github.com/astropy/astroquery.git#egg=astroquery

Requirements
````````````

The following packages are required for astroquery installation & use:

* `numpy <http://www.numpy.org>`_
* astropy_ (v>=0.3)
* `requests <http://docs.python-requests.org/en/latest/>`_
* `keyring <https://pypi.python.org/pypi/keyring>`_ (required only for the
  `~astroquery.eso` module)
* `lxml <http://lxml.de/>`_ (required only for the `~astroquery.eso` module)

Using astroquery
----------------

All astroquery modules are supposed to follow the same API.  In its simplest form, the API involves
queries based on coordinates or object names.  Some simple examples, using SIMBAD:

.. code-block:: python

    >>> from astroquery.simbad import Simbad
    >>> result_table = Simbad.query_object("m1")
    >>> result_table.pprint(show_unit=True)
    MAIN_ID      RA         DEC     RA_PREC ... COO_QUAL COO_WAVELENGTH     COO_BIBCODE
              "h:m:s"     "d:m:s"           ...
    ------- ----------- ----------- ------- ... -------- -------------- -------------------
      M   1 05 34 31.94 +22 00 52.2       6 ...        C              R 2011A&A...533A..10L



All query tools allow coordinate-based queries:

.. code-block:: python

    >>> import astropy.coordinates as coord
    >>> import astropy.units as u
    >>> # works only for ICRS coordinates:
    >>> c = coord.ICRS("05h35m17.3s -05h23m28s")
    >>> r = 5 * u.arcminute
    >>> result_table = Simbad.query_region(c, radius=r)
    >>> result_table.pprint(show_unit=True)
       MAIN_ID           RA           DEC      ... COO_QUAL COO_WAVELENGTH     COO_BIBCODE
                      "h:m:s"       "d:m:s"    ...
    -------------- ------------- ------------- ... -------- -------------- -------------------
         HD  38875 05 34 59.7297 -80 51 09.082 ...        A              O 2007A&A...474..653V
    TYC 9390-799-1 05 33 58.2222 -80 50 18.575 ...        B                1998A&A...335L..65H


For additional guidance and examples, read the documentation for the individual services below.

Available Services
------------------

If you're new to Astroquery, a good place to start is the :doc:`gallery`:

.. toctree::
  :maxdepth: 1

  gallery

The following modules have been completed using a common API:

.. toctree::
  :maxdepth: 1

  simbad/simbad.rst
  vizier/vizier.rst
  irsa/irsa_dust.rst
  ned/ned.rst
  splatalogue/splatalogue.rst
  irsa/irsa.rst
  ukidss/ukidss.rst
  magpis/magpis.rst
  nrao/nrao.rst
  besancon/besancon.rst
  nist/nist.rst
  nvas/nvas.rst
  gama/gama.rst
  eso/eso.rst

These others are functional, but do not follow a common & consistent API:

.. toctree::
  :maxdepth: 1

  fermi/fermi.rst
  sdss/sdss.rst
  alfalfa/alfalfa.rst
  sha/sha.rst
  lamda/lamda.rst
  ogle/ogle.rst


Developer documentation
-----------------------

The modules and their maintainers are listed on the
`Maintainers <https://github.com/astropy/astroquery/wiki/Maintainers>`_
wiki page.


The :doc:`api` is intended to be kept as consistent as possible, such
that any web service can be used with a minimal learning curve imposed on the
user.

.. toctree::
   :maxdepth: 1

   api.rst
   template.rst
   testing.rst

The following Astroquery modules are mostly meant for internal use of
services in Astroquery, you can use them for your scripts, but we don't guarantee API stability.

.. toctree::
  :maxdepth: 1

  utils.rst
  query.rst
