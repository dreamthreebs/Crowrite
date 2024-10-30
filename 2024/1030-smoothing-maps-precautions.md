# 1030-smoothing maps precautions

1. Using hp.synfast's fwhm paramter is equals to using hp.synfast without fwhm parameter, then use hp.map2alm then almxfl bl(fwhm) to get the same beam map.

```python
def gen_sim():
    cl_cmb = np.load('/afs/ihep.ac.cn/users/w/wangyiming25/work/dc2/psilc/src/cmbsim/cmbdata/cmbcl_8k.npy').T[0]

    np.random.seed(seed=0)
    cmb_9arcmin = hp.synfast(cls=cl_cmb, nside=nside, fwhm=np.deg2rad(9)/60)


    np.random.seed(seed=0)
    cmb_0arcmin = hp.synfast(cls=cl_cmb, nside=nside)

    cmb_0to9arcmin = hp.alm2map(hp.almxfl(hp.map2alm(cmb_0arcmin), fl=hp.gauss_beam(fwhm=np.deg2rad(9)/60,lmax=3*nside-1)), nside=nside)

    np.save('./data/cmb_9arcmin.npy', cmb_9arcmin)
    np.save('./data/cmb_0to9arcmin.npy', cmb_0to9arcmin)

def check_sim():
    cmb_9arcmin = np.load('./data/cmb_9arcmin.npy')
    cmb_0to9arcmin = np.load('./data/cmb_0to9arcmin.npy')

    hp.mollview(cmb_9arcmin, title='9 arcmin')
    hp.mollview(cmb_0to9arcmin, title='0to9 arcmin')
    hp.mollview(cmb_0to9arcmin - cmb_9arcmin, title='residual')
    plt.show()
```



