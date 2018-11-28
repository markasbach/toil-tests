Reproducible tests for toil
===========================

Author: Mark Asbach
Date: 2018-11-28

There is a lot of online documentation on how to contribute to toil. Unfortunately,
running the tests is not a simple task for an aspiring contributor who just wants
to fix a small issue and provide a pull request.

See https://toil.readthedocs.io/en/latest/contributing/contributing.html for an intro.

The goal of this little repository is to simplify running tests on a reproducable
virtual machine.


Prerequisites
-------------

- VirtualBox 5.x
- vagrant >= 2.x
- ansible >= 3.6
- enough resources to run a VM with 4 Gb RAM and 2 CPUs


Running the tests on a VM
-------------------------

    git clone https://github.com/DataBiosphere/toil.git # or choose your respective fork here
    vagrant up bionic

The latter will spin up a fresh VM with Ubuntu 18.04 installed, upgrade all packages,
install some dependencies, install toil itself from the cloned repository and run
the offline tests. You will find the test output in the current directory as `test_offline.log`.

On my machine, the last lines of the log file read:

    ============= 66 failed, 75 passed, 521 skipped in 436.04 seconds ==============
    Makefile:147: recipe for target 'test_offline' failed

So expect the actual test to run about for 7 to 8 minutes. You could also run the tests on an older
Ubuntu 16.04 (python 3.5) using `vagrant up xenial`.
