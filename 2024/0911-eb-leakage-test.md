# 0911-EB leakage test

### DATA

nside = 512

* CMB (lmax=3\*nside-1)
* NOISE all scale
* diffuse foreground lmax=600

### RESULT

#### CMB only&#x20;

* lmax=600 2.0609977627964478
* lmax=3nside-1 2.0605068073823825
* zzr lmax=600 2.1137298869562455
* zzr lmax=3nside-1 2.1309597391592563

#### CMB +NOISE

* lmax=600  2.0411961242764383
* lmax=3nside-1 2.035552067741892

#### DIFFUSE FOREGROUND only

* lmax=600 2.096625211600084
* lmax=3nside-1 2.092762185743223

#### CFN

* lmax=600 2.442499166185035
* lmax=3nside-1 2.4417910289591216
* zzr lmax=600 2.249160721811816
* zzr lmax=3nside-1 2.2513067125353503

