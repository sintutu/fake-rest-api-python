# Getting started

This document follows https://docs.pytest.org/en/stable/getting-started.html#get-started.

To install, run

```bash
pip install -U pytest
```

This is equivalent to 

```bash
pip install --upgrade pytest
```

This is what the -U option does:
> Upgrade all specified packages to the newest available version. The handling of dependencies depends on the upgrade-strategy used.

The remainder of this document is running through all the examples from the getting started guide.

A few lessons from this session:

## Upgrading `pip` is hard. 

I encountered 

```log
ERROR: Could not install packages due to an OSError: [WinError 5] Access is denied: 'c:\\python312\\lib\\site-packages\\pip-24.0.dist-info\\AUTHORS.txt'
```

It's a quick fix. 

```bash
python.exe -m pip install --upgrade pip
```
sorts out the problem. Seemingly for all users as python is installed on the workstation for all users at c:\\python312.

Another fix would be do do things specific for the user with 

```bash
python -m pip install --upgrade pip --user
```
which does thing specific for the user.

I don't know which is better at this time.

## Test methods are prepended with `test_`

A method is defined with the `def` keyword then the method name.

A test method is a method prepended with `test_` e.g.
```python
def test_two(self):
        assert self.value == 1
```
## Test Classes
A class is defined with the `class` keyword and the class name follows Pascal case.

It can contain multiple methods, member variables and test methods, all following the above rules.

## Tests for exceptions

To use exceptions, `pytest` uses the `with` keyword and the method `raises({ExceptionType})` where `{ExceptionType}` takes in the exception that is raised.

```python
def test_mytest():
    with pytest.raises(SystemExit):
        f()
```
after which the `assert` method is called to assert that the expected assertion type is indeed what is returned.

You can use the `not` keyword to assert that a certain exception type is not raised e.g. 

```python
def f():
    raise ExceptionGroup(
        "Group message",
        [
            RuntimeError(),
        ],
    )


def test_exception_in_group():
    with pytest.raises(ExceptionGroup) as excinfo:
        f()
    assert excinfo.group_contains(RuntimeError)
    assert not excinfo.group_contains(TypeError)
```

That's all for now.