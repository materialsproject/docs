# Calculations Manual

## Overview

This manual explains our calculation methods, adjustments made to our calculated energies,
and errors in our calculations.

## Total Energy Calculations Details

We use density functional theory as implemented in the Vienna Ab Initio Simulation Package (VASP)
software[^1] to evaluate the total energy of compounds. For the exchange-correlational functional,
we employ a mix of Generalized Gradient Approximation (GGA) and GGA+*U*, as described
[later in this manual] (TODO link to later).
We use the Projector Augmented Wave (PAW) method for modeling core electrons with an energy
cutoff of 520 eV. This cutoff corresponds to 1.3 times the highest cutoff recommended among all 
the pseudopotentials we use (more details can be found in the
[Pseudopotentials Choice](pseudopotentials-choice.md) manual).
All calculations are performed at 0K and 0atm. All computations are performed with spin polarization
on and with magnetic ions in a high-spin ferromagnetic initialization (the system can of course
relax to a low spin state during the DFT relaxation). We used a k-point mesh of 1000/(number of
atoms in the cell) for all computations, the Monkhorst-Pack method for the k-point choices (but
$\Gamma$-centered for hexagonal cells) and the tetrahedron method to perform the k-point integration.
Pymatgen could change those default parameters if they are not adequate for the computation 
(e.g., switch to another k-point integration scheme). Some details of our calculation method
can be found in ref [^2]; however, the Materials Project has updated many parameters as 
documented throughout the [Calculations Wiki](calculations-wiki.md).

### Crystal structures

We use input structures from the Inorganic Crystal Structure Database (ICSD),[^3]
and relax all cell and atomic positions in our calculation two times in consecutive runs.
When multiple crystal structures are present for a single chemical composition, we
attempt to evaluate all unique structures as determined by an affine mapping technique.[^4]

### Total energy convergence

We currently employ a k-point mesh of 1000/number of atoms. We performed a convergence test
of total energy with respect to k-point density and convergence energy difference for a subset
of chemically diverse compounds for a previous parameter set, which employed a smaller k-point
mesh of 500/atom. Using 500/atom k-point mesh, the numerical convergence for most compounds 
tested was within 5 meV/atom, and 96% of compounds tested were converged to within 15 meV/atom.
Results for the new parameter set will be better due to the higher k-point mesh employed. 
Convergence will depend on chemical system; for example, oxides were generally converged 
to less than 1 meV/atom.[^2]

### Structure convergence

The energy difference for ionic convergence is set to 0.0005 * natoms in the cell. 
Data on expected accuracy on cell volumes can be found in a previous paper.[^2] We 
have found these parameters to yield well-converged structures in most instances; 
however if the structures are to be used for further calculations that require strictly
converged atomic positions and cell parameters (e.g. elastic constants, phonon modes, etc.)
we recommend that users re-optimize the structures with tighter cutoffs or in force convergence mode.

## Total Energy Adjustments

To better model energies across diverse chemical spaces, we apply several adjustments
to the total energy. These adjustments are described below.

### Default corrections

#### Gases, liquids, and elements

Our total energy calculations are for periodic solids at 0K. For elements that are gaseous 
in their standard state, our raw calculations do not represent the same phase as standard
experimental data. In addition, there may be GGA errors associated with reducing gas phases 
in gas-to-solid reactions. Rather than calculating the liquid/gas energies directly, we 
adjust the energies of several elements that are liquid or gaseous at room temperature 
using Wang's method.[^5] The best-tested fit is for oxygen gas reacting to form to oxides.
We have adjusted energies of the following compounds:

* $

#### GGA+*U* calculations and adjustments to match GGA energies

## Band Structure and DOS computations details

## Accuracy of Total Energies

### Estimating errors in calculated reaction energies

### Sources of error

### GGA errors on reaction energies between chemically similar compounds

## Accuracy of Calculated Volumes

## Accuracy of Band Structures

### Band gaps

#### Origin of band gap error and improving accuracy

## Citation

## References

## Authors

* Anubhav Jain
* Shyue Ping Ong
* Geoffroy Hautier
* Charles Moore
