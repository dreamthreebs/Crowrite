# 0823-same name of some variable

```python
import numpy as np

def lonlat(a, b):
    return a + b

def hi(x, y, lonlat=True):
    if lonlat:
        print(f'{x=}')
    else:
        print(f'{y=}')

hi(3, 4)
```
