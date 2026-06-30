# Integrated Methane Inversion (IMI) Workflow
## Overview:

This directory contains the source code for setting up and running the
[Integrated Methane Inversion](https://carboninversion.com/) with GEOS-Chem. This fork has been created specifically to accomodate the needs of scientists at SRON who use the IMI on the Dutch National Supercomputer Snellius.


## Documentation:

For official IMI documentation, please see the [IMI readthedocs site](https://imi.readthedocs.io).

## SRON installation steps

1. Step one: clone the SRON-specific fork of the IMI:
```shell
git clone https://github.com/Clayton-Roberts/integrated_methane_inversion.git
```

2. Move into the IMI directory you've created and clone GCClassic. Use the -recursive flag to download links from previous commits: 
```shell
cd integrated_methane_inversion
git clone https://github.com/geoschem/GCClassic.git
cd GCClassic
git submodule update --init –-recursive
```

 (to download links from previous commits)

## New header

## References:

* Estrada, L.A., D.J. Varon, M. Sulprizio, H. Nesser, Z. Chen, N. Balasus, S.E. Hancock, M. He, J.D. East, T.A. Mooring, A. Oort Alonso, J.D. Maasakkers, I. Aben, S. Baray, K.W. Bowman, J.R. Worden, F.J. Cardoso-Saldaña, E. Reidy, and D.J. Jacob, Integrated Methane Inversion (IMI) 2.0: an improved research and stakeholder tool for monitoring total methane emissions with high resolution worldwide using TROPOMI satellite observations, Geoscientific Model Development, 18, 3311–3330, [https://doi.org/10.5194/gmd-18-3311-2025](https://doi.org/10.5194/gmd-18-3311-2025), 2025.
* Varon, D. J., Jacob, D. J., Sulprizio, M., Estrada, L. A., Downs, W. B., Shen, L., Hancock, S. E., Nesser, H., Qu, Z., Penn, E., Chen, Z., Lu, X., Lorente, A., Tewari, A., and Randles, C. A.: Integrated Methane Inversion (IMI 1.0): a user-friendly, cloud-based facility for inferring high-resolution methane emissions from TROPOMI satellite observations, Geosci. Model Dev., 15, 5787–5805, [https://doi.org/10.5194/gmd-15-5787-2022](https://doi.org/10.5194/gmd-15-5787-2022), 2022.