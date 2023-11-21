# cupy

Cupy is a GPU array library that mimics numpy. It is a drop-in replacement for numpy, but it runs on GPU. It is a good choice for GPU programming beginners.

## Installation

```bash
pip install cupy
```

Example:

```python
import cupy as cp
import numpy as np

a = cp.arange(6).reshape(2,3).astype('f')
b = cp.arange(3).astype('f')
c = cp.dot(a, b)
print(c)
```
