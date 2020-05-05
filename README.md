Regression testing tool for JWST Pipeline
-----------------------------------------

Location of the last run /ins//jwst-0.7.8rc3_regression_test
It needs the latest regression test db in this case b7.1rc3_sic_dil.db 

Documentation https://outerspace.stsci.edu/display/JWSTPWG/Regression+Testing+of+the+Calibration+Pipeline

First clone the package from git (git clone url}

To install the package first

source the jwst environment you want to run

>conda install sqlalchemy

run in the command line : 

>python setup.py install

"regression_test" should replace "check_jwst-0.7.8rc3.py" in the documentation.


Matt Hill wrote a script which will attempt to run a version of the build 7/conda-dev pipeline on a collection of exposures and write the result and some useful information about the exposures to a file.

Installing the code first time
------------------------------

The source code is located in Git https://github.com/STScI-MESA/regression-testing-tool. Clone this repository in your machine.::

   $ git clone https://github.com/STScI-MESA/regression-testing-tool.git

Once you do that, install go to the regression_testing_tool/ directory and install it

   $ python setup.py install

You will need to access the database that has the information about the regression test data so you need to install sqlalchemy::

   $ conda install sqlalchemy

Install the latest version of the JWST Calibration pipeline
-----------------------------------------------------------

You need to be running python3 so you need to download and install astroconda3 or miniconda3. Here information for Miniconda3 for Lynux::

   $ wget https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh
   $ sh Miniconda3-latest-Linux-x86_64.sh

   $ export PATH="$HOME/miniconda3/bin:$PATH"

or::

   $ wget https://repo.continuum.io/archive/Anaconda3-5.1.0-Linux-x86_64.sh
   $ bash Anaconda3-5.1.0-Linux-x86_64.sh
   $ export PATH=$HOME/anaconda3/bin:$PATH

Now install the build release
+++++++++++++++++++++++++++++

To install the build release follow the instructions in ``https://github.com/spacetelescope/jwst``.

Activate your release::

   $ source activate <env_name>


Setup CRDS
----------

To set up CRDS you need to set the environment variables to point to the correct system::

   $ export CRDS_SERVER_URL=https://jwst-crds.stsci.edu
   $ export CRDS_PATH=$HOME/crds_cache

Setup the context to use::

   $ export CRDS_CONTEXT="jwst_0403.pmap"

Regression Test Database
------------------------

The regression test database include the path and name to the available data for testing. This allows you to be able to run the tool in any directory. The set used is maintained by DMS/SDP and updated everytime a new version of the SDP is released. This means that from time to time the name of the directory will change (usually to the version of the software). In this case, and to avoid having to update the database, a symbolic link from the current to the old name of the database needs to be made. For example, the latest version of the SDP run is in directory /grp/jwst/ins/mary/b7.1rc9_full/ while the DB has directory /grp/jwst/ins/maryb7.1rc3_sic_dil.  Making a symbolic ink in /grp/jwst/ins/mary/ will get things running::

   $ ln -s /grp/jwst/ins/maryb7.1rc3_sic_dil /grp/jwst/ins/mary/b7.1rc9_full

This symbolic link will exist until Mary wipes out that directory and creates a new one. Remember that this directory contains only the regression test. The results of the test run will be saved in your working directory.

Creating a new database
-----------------------

You can create a new database by downloading::

   $ source activate <astroconda>

<astroconda> can be miniconda3 or astroconda3::

   $ conda install sqlalchemy

   $ source activate <jwst_environment>

   $ conda install --channel stsci-mesa reftest

   $ create_reftest_db /your/directory/path/namedatabase.db

Run the regression test
-----------------------

Using nohup should keep the code running even after loging off::

   nohup regression_test /path_to_db/regression_test.db output.txt --params '{"INSTRUME": "NIRSPEC"}' --nproc 6 &


