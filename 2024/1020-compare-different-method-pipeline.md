# 1020-compare different method pipeline

1. Extract diffuse foreground power spectrum from partial sky (compare it with other component)
2. Find out threshold in T maps
3. Generate point sources simulation from previous threshold
4. Do template fitting for pcfn simulations and n simulations
5. Check goodness of fit.
6. Produce template fitting after maps on QU
7. Do inpainting (generate input by recycling method first)
8. Power spectrum estimation&#x20;

### Diffuse fg configuration

* 215GHz numerical error occur at 3500; calc at 3000;  power spectrum estimation on 2500. finally use up to 2000.  flux density error on T is 30.7mJy
* 95GHz numerical error occur at 1600; calc at 1500; power spectrum estimation at 1000. finally use up to 720. flux density error on T is 154.2 mJy.
* 30GHz numerical error occur at ?; calc at 500; power spectrum estimation at 500. finally use up to 2000. flux density error on T is 145.6 mJy.

