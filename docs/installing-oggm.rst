Installing OGGM
===============

OGGM itself is a pure python package, but it has several dependencies wich
are not always trivial to install. The instructions below are
self-explanatory and should work on any platform. However,
complete beginners should get familiar with Python and its packaging
ecosystem before trying to install and run OGGM.

OGGM is tested with Python versions `2.7 and 3.4`_.

For most users we recommend to use the conda_ package manager  to install
the dependencies `With conda (all platforms)`_. Linux users and people
with experience with `pip`_ can follow the specific instructions
`With virtualenv (linux/debian)`_.

.. _2.7 and 3.4: https://wiki.python.org/moin/Python2orPython3
.. _conda: http://conda.pydata.org/docs/using/index.html
.. _pip: https://docs.python.org/3/installing/


Dependencies
------------

Standard SciPy track:
    - numpy
    - scipy
    - scikit-image
    - pillow
    - matplotlib
    - pandas
    - joblib

Python 2 support:
    - six

Configuration file parsing tool:
    - configobj

I/O:
    - netcdf4

GIS and geometrical tools:
    - gdal
    - shapely
    - pyproj
    - geopandas

Testing:
    - nose

Other libraries:
    - `salem <https://github.com/fmaussion/salem>`_
    - `cleo <https://github.com/fmaussion/cleo>`_
    - `motionless (py3) <https://github.com/fmaussion/motionless>`_


With conda (all platforms)
--------------------------

Prerequisites
~~~~~~~~~~~~~

You should have a recent version of `git`_ and of `conda`_ (either by
installing `miniconda`_ or `anaconda`_).


**Linux** users should install a couple of packages (not all of them are
required but just to be sure)::

    $ sudo apt-get install build-essential liblapack-dev gfortran libproj-dev gdal-bin libgdal-dev netcdf-bin ncview python-netcdf

.. _git: https://git-scm.com/book/en/v2/Getting-Started-Installing-Git
.. _miniconda: http://conda.pydata.org/miniconda.html
.. _anaconda: http://docs.continuum.io/anaconda/install


Conda environment
~~~~~~~~~~~~~~~~~

We recommend to create a specific `environment`_ for OGGM. In a terminal
window, type::

    conda create --name oggm python=3.4

You can of course use any other name for your environment. Don't forget to
activate it::

    source activate oggm

(on windows: `activate oggm`)

.. _environment: http://conda.pydata.org/docs/using/envs.html


Packages
~~~~~~~~

Install the packages from the ioos channel::

    conda install -c ioos geopandas matplotlib Pillow joblib netCDF4 scikit-image configobj nose pyproj numpy

After success, install the following packages from Fabien's github::

    pip install git+https://github.com/fmaussion/motionless.git
    pip install git+https://github.com/fmaussion/salem.git
    pip install git+https://github.com/fmaussion/cleo.git

OGGM
~~~~

We recommend to clone the git repository (or a fork if you want
to participate to the development)::

   git clone git@github.com:OGGM/oggm.git

Then go to the project root directory::

    cd oggm

And install OGGM in development mode::

    pip install -e .


Testing
~~~~~~~

From the oggm root directory, type::

    nosetests .


With virtualenv (linux/debian)
------------------------------

For Debian / Ubuntu / Mint users only!

Linux packages
~~~~~~~~~~~~~~

For building stuffs::

    $ sudo apt-get install build-essential python-pip liblapack-dev gfortran libproj-dev

For matplolib to work on **Python 2**::

    $ sudo apt-get install python-gtk2-dev

And on **Python 3**::

    $ sudo apt-get install tk-dev python3-tk python3-dev

For GDAL::

    $ sudo apt-get install gdal-bin libgdal-dev python-gdal

For NETCDF::

    $ sudo apt-get install netcdf-bin ncview python-netcdf


Virtual environment
~~~~~~~~~~~~~~~~~~~

Install::

    $ sudo pip install virtualenvwrapper

Create the directory where the virtual environments will be created::

    $ mkdir ~/.pyvirtualenvs

Add these three lines to the files: ~/.profile and ~/.bashrc::

    # Virtual environment options
    export WORKON_HOME=$HOME/.pyvirtualenvs
    source /usr/local/bin/virtualenvwrapper_lazy.sh

Reset your profile::

    $ . ~/.profile

Make a new environment with **Python 2**::

    $ mkvirtualenv oggm_env -p /usr/bin/python

Or **Python 3**::

    $ mkvirtualenv oggm_env -p /usr/bin/python3

(Details: http://simononsoftware.com/virtualenv-tutorial-part-2/ )


Python Packages
~~~~~~~~~~~~~~~

Be sure to be on the working environment::

    $ workon oggm_env

Install one by one the easy stuff::

   $ pip install numpy scipy pandas shapely

For Matplotlib and **Python 2** we need to link the libs in the virtual env::

    $ ln -sf /usr/lib/python2.7/dist-packages/{glib,gobject,cairo,gtk-2.0,pygtk.py,pygtk.pth} $VIRTUAL_ENV/lib/python2.7/site-packages
    $ pip install matplotlib

(Details: http://www.stevenmaude.co.uk/2013/09/installing-matplotlib-in-virtualenv.html )

For Matplotlib and **Python 3** it doesn't seem to be necessary::

    $ pip install matplotlib

Check if plotting works by running these three lines in python::

    >>> import matplotlib.pyplot as plt
    >>> plt.plot([1,2,3])
    >>> plt.show()

If nothing shows-up, something got wrong.

For **GDAL**, it's also not straight forward. First, check which version of
GDAL is installed::

    $ dpkg -s libgdal-dev

The version (10, 11, ...) should match that of the python package. Install
using the system binaries::

    $ pip install gdal==1.10.0 --install-option="build_ext" --install-option="--include-dirs=/usr/include/gdal"
    $ pip install fiona --install-option="build_ext" --install-option="--include-dirs=/usr/include/gdal"

(Details: http://tylerickson.blogspot.co.at/2011/09/installing-gdal-in-python-virtual.html )

Install further stuffs::

    $ pip install pyproj rasterio Pillow geopandas netcdf4 scikit-image configobj joblib

And the external libraries::

    $ pip install git+https://github.com/fmaussion/motionless.git
    $ pip install git+https://github.com/fmaussion/salem.git
    $ pip install git+https://github.com/fmaussion/cleo.git

OGGM and tests
~~~~~~~~~~~~~~

Refer to `OGGM`_ above.