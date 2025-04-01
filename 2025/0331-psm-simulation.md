# 0331-PSM simulation

### Simulation

* **Frequency scope:** Only for frequencies ranging from about 3 GHz to about 3 THz, i.e., wavelengths ranging between 100 µm and 10 cm. At lower frequencies, Faraday rotation is important and our polarised maps are not representative of the sky emission, as this effect is presently neglected. Intensity maps, however, should be reasonably accurate down to about 500 MHz. At frequencies higher than 3 THz, the complexity of the dust emission is not properly taken into account by the present model, for which the representation of dust emission is based on spectral fits valid below 3 THz.
* **Object:** Emission from compact objects (external galaxies, clusters of galaxies, and Galactic compact sources).
* **Detailed components:**  the CMB dipole, CMB anisotropies, synchrotron, free-free, thermal dust, spinning dust, CO molecular lines, thermal SZ effect, kinetic SZ effect, radio sources, infrared sources, far infrared background, and ultracompact H II regions. Solar-system emission from the planets, their satellites, a large number of small objects (asteroids), and dust particles and grains in the ecliptic plane (which generate zodiacal light) are not modelled in the current version.
* **Power law vary in the  sky**? : Some components are modelled with a fixed emission law which does not depend on the sky location. In the current implementation, this is the case for the CMB, the non-relativistic SZ effects (thermal and kinetic), free-free, and spinning dust emission. Synchrotron and thermal dust are modelled with emission laws which vary over the sky. Each point source is also given its own emission law.

### Diffuse Galactic emission

* **ISM:** Diffuse Galactic emission originates from the ISM of the Milky Way. The ISM is made up of cold atomic and molecular clouds, a warm inter-cloud medium that is partly ionised, and a hot ionised medium. The ISM also comprises magnetic fields and cosmic rays. Galactic emission from the ISM is usually separated into distinct components according to the physical emission process: synchrotron radiation from relativistic free electrons spiralling in the Galactic magnetic field; free-free emission from the warm ionised medium, due to the interaction of free electrons with positively charged nuclei; thermal (vibrational) emission from interstellar dust grains heated by radiation from stars; spinning dust emission from the dipole moment of rotating dust grains; line emission from atoms and molecules. As the interstellar matter is concentrated in the Galactic plane, the intensity of these diffuse emissions decreases with Galactic latitude approximately according to a cosecant law (the optical depth of the emitting material scales proportionally to 1/sin |b|).
* **Synchrotron:** Galactic synchrotron emission arises from relativistic cosmic rays accelerated by the Galactic magnetic field (e.g., Rybicki & Lightman, 1979). It is the dominant contaminant of the polarised CMB signal at low frequencies (below about 80 GHz). The intensity of the synchrotron emission depends on the cosmic ray density _nₑ_ and on the strength of the magnetic field perpendicular to the line of sight. The spectral signature of the synchrotron emission is determined by the energy distribution of cosmic rays.

### Point sources

* **Galactic or Extragalactic?:** Numerous Galactic and extragalactic compact sources emit radiation in the frequency range modelled in the PSM. Extragalactic emission arises from a large number of radio and far-infrared galaxies, as well as clusters of galaxies. Compact regions in our own Galaxy include molecular clouds, supernova remnants, compact H II regions, as well as Galactic radio sources.
* **SZ effects:** The thermal and kinetic SZ effects, due to the inverse Compton scattering of CMB photons off free electrons in ionised media, are of special interest for cosmology. These effects occur, in particular, towards clusters of galaxies, which are known to contain hot (few keV) electron gas. SZ emission is modelled here both on the basis of known existing clusters, observed in the optical and/or in X-rays, and on the basis of cluster number counts predicted in the framework of a particular cosmological model.







