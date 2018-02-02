# regression-testing-tool
Regression testing tool for JWST Pipeline

Location of the last run /ins//jwst-0.7.8rc3_regression_test
It needs the latest regression test db in this case b7.1rc3_sic_dil.db 

Documentation https://confluence.stsci.edu/display/JWSTPWG/Regression+Testing+of+the+Calibration+Pipeline

First clone the package from git (git clone url}

To install the package first

source the jwst environment you want to run
>conda install sqlalchemy

run in the command line : 

>python setup.py install

"regression_test" should replace "check_jwst-0.7.8rc3.py" in the documentation.
