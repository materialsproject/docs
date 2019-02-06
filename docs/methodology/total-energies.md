# Total Energy Calculations

Calculation Details
-------------------

We use density functional theory as implemented in the Vienna Ab Initio
Simulation Package (VASP) software[^1] to evaluate the total energy of
compounds. For the exchange-correlational functional, we employ a mix of
Generalized Gradient Approximation (GGA) and GGA+<em>U</em>, as
described [later in this manual](#ggau_tag).
We use the Projector Augmented Wave (PAW) method for modeling core
electrons with an energy cutoff of 520 eV. This cutoff corresponds to
1.3 times the highest cutoff recommended among all the pseudopotentials
we use (more details can be found in the [Pseudopotentials
Choice](/methodology/pseudopotentials) manual). All calculations
are performed at 0K and 0atm. All computations are performed with spin
polarization on and with magnetic ions in a high-spin ferromagnetic
initialization (the system can of course relax to a low spin state
during the DFT relaxation). We used a k-point mesh of 1000/(number of
atoms in the cell) for all computations, the Monkhorst-Pack method for
the k-point choices (but \\(\Gamma\\)-centered for hexagonal cells) and
the tetrahedron method to perform the k-point integration. Pymatgen
could change those default parameters if they are not adequate for the
computation (e.g., switch to another k-point integration scheme). Some
details of our calculation method can be found in ref [^2]; however, the
Materials Project has updated many parameters as documented throughout
the Methodology sections.

### Crystal structures

We use input structures from the Inorganic Crystal Structure Database
(ICSD),[^3] and relax all cell and atomic positions in our calculation
two times in consecutive runs. When multiple crystal structures are
present for a single chemical composition, we attempt to evaluate all
unique structures as determined by an affine mapping technique.[^4]

### Total energy convergence

We currently employ a k-point mesh of 1000 per reciprocal atom (pra). We performed
a convergence test of total energy with respect to k-point
density and convergence energy difference for a subset of chemically
diverse compounds for a previous parameter set, which employed a smaller
k-point mesh of 500 pra. Using a 500 pra k-point mesh, the numerical
convergence for most compounds tested was within 5 meV/atom, and 96% of
compounds tested were converged to within 15 meV/atom. Results for the
new parameter set will be better due to the denser k-point mesh
employed. Convergence will depend on chemical system; for example,
oxides were generally converged to less than 1 meV/atom.[^5]

### Structure convergence

The energy difference for ionic convergence is set to 0.0005 \* natoms
in the cell. Data on expected accuracy on cell volumes can be found in a
previous paper.[^2] We have found these parameters to yield
well-converged structures in most instances; however, if the structures
are to be used for further calculations that require strictly converged
atomic positions and cell parameters (e.g. elastic constants, phonon
modes, etc.), we recommend that users re-optimize the structures with
tighter cutoffs or in force convergence mode.

Total Energy Adjustments
------------------------

To better model energies across diverse chemical spaces, we apply
several adjustments to the total energy. These adjustments are described
below.

### Default corrections

#### Gases, liquids, and elements

Our total energy calculations are for periodic solids at 0K. For
elements that are gaseous in their standard state, our raw calculations
do not represent the same phase as standard experimental data. In
addition, there may be GGA errors associated with reducing gas phases in
gas-to-solid reactions. Rather than calculating the liquid/gas energies
directly, we adjust the energies of several elements that are liquid or
gaseous at room temperature using Wang's method.[^5] The best-tested fit
is for oxygen gas reacting to form to oxides. We have adjusted energies
of the following compounds:

-   $\ce{O2}$, $\ce{N2}$, $\ce{Cl2}$, $\ce{F2}$, $\ce{H2}$

The adjusted energies outside of $\ce{O2}$ are not as well-tested, and
calculations involving these elements should be taken with greater
caution. For example, it is assumed in our elemental gas adjustments
that reactions to the solid will involve reduction of the gas.

<a name="ggau_tag"></a>
#### GGA+<em>U</em> calculations and adjustments to match GGA energies

Some compounds are better modeled with a <em>U</em> correction term to
the density functional theory Hamiltonian while others are better
modeled without (i.e., straight GGA). Energies from calculations with
the +<em>U</em> correction are not directly comparable to those without.
To obtain better accuracy across chemical systems, we use GGA when
appropriate, GGA+<em>U</em> otherwise, and mix energies from the two
calculation methodologies by adding an energy correction term to the
GGA+<em>U</em> calculations to make them comparable to the GGA
calculations. The idea behind this approach is to split reactions into
sub-reactions that are well-modeled by GGA, well-modeled by
GGA+<em>U</em>, or a binary formation reaction that can be estimated
from known experimental data. More details on this method can be found
in ref [^6].

Accuracy of Total Energies
--------------------------

To estimate the accuracy of our total energy calculations, we compute
reaction data and compare against experimental data. Note that this data
set was compiled using a lower k-point mesh and pseudopotentials with
fewer electrons than the current Materials Project parameter set.

### Estimating errors in calculated reaction energies

The accuracy of calculated reaction energies depends on the chemical
system investigated. In general, GGA calculations have similar errors
among chemically similar systems. Hence, reaction energies between
chemically similar systems (e.g., a reaction where the reactants and
products are all oxides, such as $\ce{MgO + Al2O3 -> MgAl2O4}$) tend
to have smaller errors than reactions between chemically dissimilar
systems (e.g., between metals and insulators).

![formen errors](/methodology/img/calculations-manual/FormE_errors.png)
*Figure 1: Errors in Calculated Formation Energies for
413 binaries in the Kubaschewski Tables. Energies are normalized to per
mol atom.*

To provide a quantitative indicator of the error we may expect from the
reaction calculator, we have computed the reaction energies of
[413 binaries](/methodology/static/KtablesBinaries.txt) in the Kubaschewski
Tables formed with Group V, VI and VII anions. Figure 1 shows the errors
in the calculated formation energies (compared to the experimental
values) for these compounds. The mean absolute error (MAE) is around 14
kJ mol$^{-1}$. 75% of the calculated formation energies are within 20 kJ
mol$^{-1}$. We also found that compounds of certain elements tend to have
larger errors. For example, Bi, Co, Pb, Eu, U, Tl and W compounds often
have errors larger than 20 kJ mol$^{-1}$.

It should be noted that while an MAE of 14 kJ mol$^{-1}$ is significantly
higher than the desired chemical accuracy of 4 kJ mol$^{-1}$, it compares
fairly well with the performance of most quantum chemistry
calculations[^7]. Other than the most computationally expensive model
chemistries such as G1-G3 and CBS, the reaction energy errors of most
computational chemistry model chemistries are well above 10 kJ mol$^{-1}$.

For oxidation of the elements into binary compounds, an average error of
~4% or 33 kJ/mol-$\ce{O2}$ is typical.[^8] For conventional ternary oxide
formation from the elements, we have found a mean relative absolute
error of about 2%.[^6]

### Sources of error

The largest contribution to the error comes from the inability of the
GGA to fully describe electronic exchange and correlation effects. In
addition, there is some error associated with neglecting zero-point
effects and with comparing 0K, 0atm computations with room-temperature
enthalpy experiments. The latter effect was estimated to contribute less
than 0.03 eV/atom by Lany.[^9] The stability of antiferromagnetic
compounds may be underestimated, as the majority of our calculations are
performed ferromagnetically only. The effect of magnetism may be small
(under 10 meV/atom) or large (100 meV/atom or greater), depending on the
compound. For compounds with heavy elements, relativistic effects may
lead to greater-than-expected errors.

### GGA errors on reaction energies between chemically similar compounds

We recently conducted a more in-depth study comparing GGA (+U) reaction
energies of ternary oxides from binary oxides on 135 compounds. [^10]

The main conclusions are:

-   The error in reaction energies for the binary oxide to ternary
    oxides reaction energies are an order of magnitude lower than for
    the more often reported formation energies from the element. An
    error intrinsic to GGA (+U) is estimated to follow a normal
    distribution centered in zero (no systematic underestimation
    or overestimation) and with a standard deviation around 24 meV/at.
-   When looking at phase stability (and for instance assessing if a
    phase is stable or not), the relevant reaction energies are most of
    the time not the formation energies from the elements but reaction
    energies from chemically similar compounds (e.g., two oxides forming
    a third oxide). Large cancelation of errors explain
    this observation.
-   The +U is necessary for accurate description of the energetics evene
    when reactions do not involve change in formal oxidation states

Accuracy of Calculated Volumes
------------------------------

A discussion of errors in calculated volumes can be found in the [Volume
Change Error manual](/methodology/volume-change-error).

Citation
--------

To cite the calculation methodology, please reference the following
works:

1.  A. Jain, G. Hautier, C. Moore, S.P. Ong, C.C. Fischer, T.
    Mueller, K.A. Persson, G. Ceder., A High-Throughput Infrastructure
    for Density Functional Theory Calculations, Computational Materials
    Science, vol. 50, 2011, pp. 2295-2310.
    [DOI:10.1016/j.commatsci.2011.02.023](https://dx.doi.org/10.1016/j.commatsci.2011.02.023)
2.  A. Jain, G. Hautier, S.P. Ong, C. Moore, C.C. Fischer, K.A.
    Persson, G. Ceder, Accurate Formation Enthalpies by Mixing GGA and
    GGA+U calculations, Physical Review B, vol. 84, 2011, p. 045115.
    [DOI:10.1103/PhysRevB.84.045115](https://doi.org/10.1103/PhysRevB.84.045115)

Authors
-------

1. Anubhav Jain
2. Shyue Ping Ong
3. Geoffroy Hautier
4. Charles Moore

References
----------

[^1]: Kresse, G. & Furthmuller, J., 1996. Efficient iterative schemes
    for ab initio total-energy calculations using a plane-wave basis
    set. Physical Review B, 54, pp.11169-11186.

[^2]: A. Jain, G. Hautier, C. Moore, S.P. Ong, C.C. Fischer, T. Mueller,
    K.A. Persson, G. Ceder., A High-Throughput Infrastructure for
    Density Functional Theory Calculations, Computational Materials
    Science. vol. 50 (2011) 2295-2310.

[^3]: G. Bergerhoff, The inorganic crystal-structure data-base, Journal
    Of Chemical Information and Computer Sciences. 23 (1983) 66-69.

[^4]: R. Hundt, J.C. Schön, M. Jansen, CMPZ - an algorithm for the
    efficient comparison of periodic structures, Journal Of Applied
    Crystallography. 39 (2006) 6-16.

[^5]: L. Wang, T. Maxisch, G. Ceder, Oxidation energies of transition
    metal oxides within the GGA+U framework, Physical Review B. 73
    (2006) 1-6. 

[^6]: A. Jain, G. Hautier, S.P. Ong, C. Moore, C.C. Fischer, K.A.
    Persson, G. Ceder, Formation Enthalpies by Mixing GGA and GGA+U
    calculations, Physical Review B, vol. 84 (2011), 045115.

[^7]: J.B. Foresman, A.E. Frisch, Exploring Chemistry With Electronic
    Structure Methods: A Guide to Using Gaussian, Gaussian. (1996).

[^8]: A. Jain, S.-a Seyed-Reihani, C.C. Fischer, D.J. Couling, G.
    Ceder, W.H. Green, Ab initio screening of metal sorbents for
    elemental mercury capture in syngas streams, Chemical Engineering
    Science. 65 (2010) 3025-3033.

[^9]: S. Lany, Semiconductor thermochemistry in density functional
    calculations, Physical Review B. 78 (2008) 1-8.

[^10]: G. Hautier, S.P. Ong, A. Jain, C. J. Moore, G. Ceder, Accuracy of
    density functional theory in predicting formation energies of
    ternary oxides from binary oxides and its implication on phase
    stability, Physical Review B, 85 (2012), 155208
