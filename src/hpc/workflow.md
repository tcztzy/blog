# Workflow

## What is a workflow?

A workflow is a set of rules that define how to organize the code and data in a way that is easy to understand and maintain. It is also a way to automate the process of running the code.

## Why do we need a workflow?

The workflow is a way to organize the code and data in a way that is easy to understand and maintain. It is also a way to automate the process of running the code.

## How to create a workflow?

We can simply create a workflow in Python by following these steps:

<!-- mdbook-xgettext:skip -->
```python
import multiprocessing as mp

def f(x):
    return x**2

if __name__ == '__main__':
    with mp.Pool(5) as p:
        print(p.map(f, [1, 2, 3]))
```

Or you can use [dask](https://examples.dask.org/applications/evolving-workflows.html):

```python
import dask

@dask.delayed
def f(x):
    return x**2


```
