# 1011-power spectrum estimation for partial sky

There would be some bias between using partial sky data and full sky data even over many realizations.  I think this comes from partial sky cannot estimate l bigger than its area. for example l\<pi/\theta. **The way to remedy this is to use the same pipeline for parameter estimation!**&#x20;

So it was hard to compare results with full sky power spectrum.

The coupling between mask and beam will cause small scale extra contribution to power spectrum, so it is better to debeam the map first and then estimate the power spectrum.

## Why

* why partial sky estimation have bias? just like what I said?
* when do mask and beam coupling make a big difference?
* does TF have the same result as matched filter?

We can ignore this problem first and the important thing is what to do next. The goal is to find if our method can reduce point sources contribution. We need to do TF first, then do ILC, get a good result of CMB, limit r.

* select point souces that we want to reduce. how to get the threshold?

