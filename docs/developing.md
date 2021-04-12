# Developing lagtraj

`lagtraj` is automatically checked with tests that reside in `tests/`.
These are run automatically on all pull-requests against the git
repository at https://github.com/EUREC4A-UK/lagtraj and can be run locally
with `pytest` from the root of the repository:

```bash
pip install pytest
pytest
```

If you are running the tests repeatedly it's a good idea to download the
testdata locally and point lagtraj to where it resides (otherwise lagtraj will
attempt to download the testdata every time the tests are run):

```bash
wget http://gws-access.ceda.ac.uk/public/eurec4auk/testdata/lagtraj.testdata.tar.gz
mkdir /tmp/lagtraj
tar zxvf lagtraj.testdata.tar.gz -C /tmp/lagtraj
export LAGTRAJ_TESTDATA_DIR=/tmp/lagtraj
```

If the computer you are running on has multiple CPUs it can be advantageous to
run the tests in parallel to speed up the testing process. To do this you will
first need to install `pytest-xdist` and run pytest with `-n` to indicate the
number of parallel workers:

```bash
pip install pytest-xdist
pytest -n <n_cpus>
```

You can also speed up testing by reducing the number of test being run (if
you're for example working on fixing just a single breaking test) by using the
`-k` flag which where you provide a regex pattern for the name of tests you
want to run, e.g.

```bash
pytest -k lagrangian
```

Finally, it is useful to have a `ipdb`-debugger open up inline on failing
tests. This can be achieved by first installing `ipdb` and setting the
`PYTEST_ADDOPPS` environment variable:

```bash
export PYTEST_ADDOPTS='--pdb --pdbcls=IPython.terminal.debugger:Pdb'
```