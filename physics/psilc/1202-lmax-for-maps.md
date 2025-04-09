# 1202-lmax for maps

```python
lmax=5000
bl_floor = 1e-4
bl = hp.gauss_beam(fwhm=np.deg2rad(beam)/60, lmax=lmax)
lmax_alm = np.argmax(bl < bl_floor) if np.any(bl < bl_floor) else lmax

// or without lmax
bl_floor = 1e-4
bl = hp.gauss_beam(fwhm=np.deg2rad(beam)/60, lmax=8000)
lmax_alm = np.argmax(bl < bl_floor)
```
