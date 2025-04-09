# 1002-apodization

'Apodization' refers to the process of applying a mathematical function after the Fast Fourier Transform (FFT) to remove side peaks in the spectrum, which can distort signals and hinder their interpretation in Earth and Planetary Sciences.

## BRAINSTORM

* try different lmax to see if the mode-mixing effect ameliorated.
* try different mask apodization.
* simulation by fg first.
* see if lmax limited adding will cause some problem.

## BRAINSTORM testing

* if different lmax are applied the results will not change much expect for the last bin.
* different mask apodization won't change the results a lot.
