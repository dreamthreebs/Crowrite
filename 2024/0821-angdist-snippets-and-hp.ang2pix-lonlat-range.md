# 0821-angdist snippets and hp.ang2pix lonlat range

### Healpy

```python
import numpy as np
import healpy as hp
import matplotlib.pyplot as plt

dir1 = (112.66,65.74)
dir2 = (119.94,67.56)

distance = np.rad2deg(hp.rotator.angdist(dir1=dir1, dir2=dir2, lonlat=True))
print(f'{distance=}')
```



in \`hp.ang2pix\`, the longitude have no limits where latitude should range from -90 to 90.
