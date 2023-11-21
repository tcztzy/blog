# numba

Numba is a just-in-time compiler for Python that works best on code that uses NumPy arrays and functions, and loops. It is a Python compiler that translates Python code into optimized machine code at runtime using the industry-standard LLVM compiler library. Numba-compiled numerical algorithms in Python can approach the speeds of C or FORTRAN. Numba supports compilation of Python to run on either CPU or GPU hardware, and is designed to integrate with the Python scientific software stack.


Example:

```python
import numpy as np
from numba import jit
from numba import cuda

@jit
def sum(a, b):
    return a + b

@cuda.jit
def sum_kernel(a, b, c):
    i = cuda.grid(1)
    c[i] = a[i] + b[i]

a = np.arange(6).reshape(2,3).astype('f')
b = np.arange(3).astype('f')
c = sum(a, b)
print(c)

d_a = cuda.to_device(a)
d_b = cuda.to_device(b)
d_c = cuda.device_array_like(d_a)
threadsperblock = 32
blockspergrid = (a.size + (threadsperblock - 1)) // threadsperblock
sum_kernel[blockspergrid, threadsperblock](d_a, d_b, d_c)
print(d_c.copy_to_host())
```
