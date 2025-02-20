# GreenplumPython development

## Requirements

### [tox](https://tox.wiki)

Install with `pip`:

```
pip install tox
```

Install with `brew` on macOS:

```
brew install tox
```

`NodeJs` need to have version 12.X, otherwise `Pyright` can't be executed correctly. Possible scenarios:
 - Error : Cannot find module 'worker_threads'
 - Nothing happens when run `Pyright`

## Build & Test

### Lint

```
tox -e lint
```

### Test

The tests will create connection to the Greenplum cluster. So the `PGPORT` needs to be set if it is not the default `5432`:

```
export PGPORT=6000
```

Test with the default python version:

```
tox -e test
```

Test with specified officially supported version:

```
tox -e test_py39
```

Run a specified test case(s):

```
tox -e test -- -k <EXPRESSION>
# e.g.
tox -e test -- -k table
```

### VirtualEnv

The `tox` is based on VirtualEnv. If you need to enter a special VirtualEnv, just source the `activate` file in the corresponding sub directory of `.tox`. Like:

```
source .tox/test/bin/activate
```

#### Upload to PyPI

```shell
# change the version in setup.py
pip3 install twine
python3 setup.py sdist
twine upload dist/*
```
