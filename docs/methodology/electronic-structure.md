# Electronic Structure Calculations

Band Structure and DOS computations details
-------------------------------------------

We used the relaxed structure from the total energy run to perform using
the same GGA functional (and U if any) a DOS and band structure run.
This data is available for many entries in
the materials explorer. We ran first a static run with a uniform
(Monkhorst Pack or $\Gamma$-centered for hexagonal systems) k-point grid.
From this run the DOS and the charge density were extracted. The charge
density was then used to perform a band structure computation for
k-points along the symmetry lines of the Brillouin zone. The symmetry
lines have been determined following the methodology from Curtarolo et
al.[^7] using the aconvasp software.

The band structure data is displayed with full lines for up spin and
dashed lines for down spin. For insulators, the band gap is computed
according to the band structure. The nature of the gap (direct or
undirect) as well as the k-points involved in the band gap transition
are displayed. The VBM and CBMs are displayed for insulators as well by
red and white dots. The web site does not display the 10% highest bands
as those higher energies bands tend to converge more slowly.

The DOS indicates the full DOS by default but projections along atoms or
orbitals are also available through a scroll down menu. Please note that
the DOS data and band structure can be slightly different as the k-point
grid is not the same. For instance, the k-point grid for the DOS might
not include Gamma while the band structure does.

Accuracy of Band Structures
---------------------------

**Note**: *the term 'band gap' in this section generally refers to the
fundamental gap, not the optical gap. The difference between these
quantities is reported to be small in semiconductors but significant in
insulators.* [^12]

![band gaps](/methodology/img/calculations-manual/Gaps.png)
*Figure 1: Experimental versus computed band gaps for
237 compounds in an internal test. The computed gaps are underestimated
by an average factor of 1.6, and the residual error even after
accounting for this shift is significant (MAE of 0.6 eV). We thank M.
Chan for her assistance in compiling this data.*

Density functional theory is formulated to calculate ground state
properties. Although the band structure involves excitations of
electrons to unoccupied states, the Kohn-Sham energies used in solving
the DFT equations are often interpreted to correspond to electron energy
levels in the solid.

The correspondence between the Kohm-Sham eigenvalues computed by DFT and
true electron energies is theoretically valid only for the highest
occupied electron state. The Kohn-Sham energy of this state matches the
first ionization energy of the material, given an exact
exchange-correlation functional. However, for other energies, there is
no guarantee that Kohn-Sham eigenvalues will correspond to physical
observables.

Despite the lack of a rigorous theoretical basis, the DFT band structure
does provide useful information. In general, band dispersions predicted
by DFT are reported to match experimental observations; one small test
of band dispersion accuracy found that errors ranged from 0.1 to about
0.4 eV.[^13] However, predicted band gaps are usually severely
underestimated. Therefore, a common way to interpret DFT band structures
is to apply a 'scissor' operation whereby the conduction bands are
shifted in energy by a constant amount so that the band gap matches
known experimental observations.

### Band gaps

In general, band gaps computed with common exchange-correlation
functionals such as the LDA and GGA are severely underestimated.
Typically the disagreement is reported to be around 50% in the
literature. Some internal testing by the Materials Project supports
these statements; typically, we find that band gaps are underestimated
by about 40% (Figure 1). We additionally find that several known
insulators are predicted to be metallic.

#### Origin of band gap error and improving accuracy

The errors in DFT band gaps obtained from calculations can be attributed
to two sources: 1. Approximations employed to the exchange correlation
functional 2. A derivative discontinuity term, originating from the true
density functional being discontinuous with the total number of
electrons in the system.

Of these contributions, (2) is generally regarded to be the larger and
more important contribution to the error. It can be partly addressed by
a variety of techniques such as the GW approximation but typically at
high computational cost.

Strategies to improve band gap prediction at moderate to low
computational cost now been developed by several groups, including Chan
and Ceder (delta-sol),[^14] Heyd et al. (hybrid functionals) [^15], and
Setyawan et al. (empirical fits) [^16]. (These references also contain
additional data regarding the accuracy of DFT band gaps.) The Materials
Project may employ such methods in the future in order to more
quantitatively predict band gaps. For the moment, computed band gaps
should be interpreted with caution.

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

-   Anubhav Jain
-   Shyue Ping Ong
-   Geoffroy Hautier
-   Charles Moore

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

[^7]: Setyawan, W.; Curtarolo, S. Computational Materials Science 2010,
    49, 299-312.

[^8]: J.B. Foresman, A.E. Frisch, Exploring Chemistry With Electronic
    Structure Methods: A Guide to Using Gaussian, Gaussian. (1996).

[^9]: A. Jain, S.-a Seyed-Reihani, C.C. Fischer, D.J. Couling, G.
    Ceder, W.H. Green, Ab initio screening of metal sorbents for
    elemental mercury capture in syngas streams, Chemical Engineering
    Science. 65 (2010) 3025-3033.

[^10]: S. Lany, Semiconductor thermochemistry in density functional
    calculations, Physical Review B. 78 (2008) 1-8.

[^11]: G. Hautier, S.P. Ong, A. Jain, C. J. Moore, G. Ceder, Accuracy of
    density functional theory in predicting formation energies of
    ternary oxides from binary oxides and its implication on phase
    stability, Physical Review B, 85 (2012), 155208

[^12]: E.N. Brothers, A.F. Izmaylov, J.O. Normand, V. Barone, G.E.
    Scuseria, Accurate solid-state band gaps via screened hybrid
    electronic structure calculations., The Journal of Chemical Physics.
    129 (2008)

[^13]: R. Godby, M. Schluter, L.J. Sham, Self-energy operators and
    exchange-correlation potentials in semiconductors, Physical Review
    B. 37 (1988).

[^14]: M. Chan, G. Ceder, Efficient Band Gap Predictions for Solids,
    Physical Review Letters 19 (2010)

[^15]: J. Heyd, J.E. Peralta, G.E. Scuseria, R.L. Martin, Energy band
    gaps and lattice parameters evaluated with the
    Heyd-Scuseria-Ernzerhof screened hybrid functional, Journal of
    Chemical Physics 123 (2005)

[^16]: W. Setyawan, R.M. Gaume, S. Lam, R. Feigelson, S. Curtarolo,
    High-throughput combinatorial database of electronic band structures
    for inorganic scintillator materials., ACS Combinatorial Science.
    (2011).