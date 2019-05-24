# Molecules Explorer

## Release Notes
### Recent changes
#### Version 0.1 - July 16, 2016
* Initial release of Molecules Explorer.

## Introduction
The primary goal of the molecular explorer is to report the atomic structure of molecules,
found using quantum chemistry computational methods. Further quantities of interest,
including the electron affinity (EA) and ionization energies (IE), are also reported.

## Manual
* [Molecular Glossary of Terms](/user-guide/molecular_terms)

## Calculations
Atomic structures and quantities of interest were calculated using the Materials Project infrastructure with the 
quantum chemistry software Q-Chem at the backend. For small molecules, Q-Chem calculations were performed using the 
6-31+G* Pople bases [^1] and the hybrid-functional B3LYP [^2]. For molecules with more than 50 atoms, a hybrid procedure
 [^3] was used in which the geometry is optimized at a low level of theory and quantities of interest are still 
 calculated at the B3LYP/6-31+G* level.
 
### Geometry Optimization
An atomic structure is stable if its vibrational frequency spectrum contains no imaginary frequencies. Thus, the atomic
structures were calculated using a dynamic workflow that performs successive calculations until a geometry with zero 
imaginary frequencies is obtained [^3]. 

### Properties
the electron affinity (EA) and ionization potential (IP) are given by
$$EA = -\delta G_red(sol)/nF$$
$$IP = -\delta G_ox(sol)/nF$$

![Free energy cycle](img/molecules-explorer/free_energy_cycle.png)
*Figure 2: Free energy cycle for computing the oxidation/reduction potential. R denotes the molecule of interest.*

According to the above thermodynamic cycle in Fig. 1,
$delta G_ox(sol)$ and $\delta G_red(sol)$ can be calculated from the Gibbs free
energy change of gas phase:

$$\delta G_ox(sol)=\delta G_ox(gas)+\delta G_solv(R^+)-\delta G_solv(R)$$
$$\delta G_red(sol)=\delta G_red(gas)+\delta G_solv(R^-)-\delta G_solv(R)$$

The reported IP/EA are the adiabatic IP/EA[^1], which optimizes the geometry at different charge states (cation, anion, neutral), which emphasizes high-fidelity results.



## Database
The database was generated from three sources:

1. Molecules computed via systematic substitution of the functional groups in a base molecule
2. Molecules from public databases such as SciFinder and Reaxys
3. Molecules submitted by collaborators

As of May, 2019 about 22,000 molecules have been added to the database.

## Using the Computational Molecular Explorer
In order to search the database for the molecule in question, four methods can be employed.

1. Elements : returns any entry that includes the queried elements
2. Formula : returns any entry that satisfies a permutation of the queried atoms (e.g.
   H2O1, H2O, HOH, OHH all return water)
3. InChi (The IUPAC International Chemical Identifier): uses “bond connectivity,
   tautomeric information, isotope information, stereochemistry, and electronic charge
   information.” (See [InChI
   Wikipedia](https://en.wikipedia.org/wiki/International_Chemical_Identifier)) This may
   be the most precise way of searching for a molecule but perhaps the most complicated.
4. Chem Doodle: allows drawing of the chemical structure to query for the database entry
   (currently not supported on Firefox)

## References
[^1]: Ditchfield, R., Hehre, W.J. & Pople, J.A. J. Chem. Phys. 54, 724 (1971)
[^2]: Becke, A.D. Phys. Rev. A. 38, 3098 (1988)
[^3]: https://doi.org/10.1016/j.commatsci.2015.02.050