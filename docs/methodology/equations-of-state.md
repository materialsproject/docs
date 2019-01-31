# Equations of State

## Introduction

Thermodynamic equations of state (EOS) for crystalline solids describe
material behaviors under changes in pressure, volume, entropy and
temperature. Despite over a century of theoretical development and
experimental testing of energy-volume (E-V) EOS for solids, there is
still a lack of consensus with regard to which equation is indeed
optimal, as well as to what metric is most appropriate for making this
judgment.

The calculation of EOS is automated using self-documenting workflows
compiled in the atomate code base that couples pymatgen for materials
analysis, custodian for just-in-time debugging of DFT codes, and
Fireworks for workflow management. The EOS workflow begins with a
structure optimization and subsequently calculates the energy of
isotropic deformations including ionic relaxation with volumetric strain
ranging from from -15.7% to 15.7% (-5% to 5% linear strain) of the
optimized structure. Density-functional-theory (DFT) calculations were
performed as necessary using the projector augmented wave (PAW) method
as implemented in the Vienna Ab Initio Simulation Package (VASP) within
the Perdew-Burke-Enzerhof (PBE) Generalized Gradient Approximation (GGA)
formulation of the exchange-correlation functional. A cut-off for the
plane waves of 520 eV is used and a uniform k-point density of
approximately 1,000 per reciprocal atom is employed. In addition,
standard Materials Project Hubbard U corrections are used for a number
of transition metal oxides, as documented and implemented in the
pymatgen VASP input sets. We note that the computational and convergence
parameters were chosen consistently with the settings used in the
Materials Project to enable direct comparisons with the large set of
available MP data.

## Fitted Equation Forms

![](/methodology/img/EOS_eqtable.png)

## Authors

1.  Katherine Latimer
2.  Shyam Dwaraknath
3.  Donny Winston

