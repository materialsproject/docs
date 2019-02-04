# GGA+U Calculations

It is well-known that first principles calculations within the local
density approximation (LDA) or generalized gradient approximation (GGA)
lead to considerable error in calculated redox reaction energies of many
transition metal compounds. This error arises from the self-interaction
error in LDA and GGA, which is not canceled out in redox reactions where
an electron is transferred between significantly different environments,
such as between a metal and a transition metal or between a transition
metal and oxygen. Extensive discussion of this issue can be found in the
following works.[^1][^2][^3][^4]

In the Materials Project, we have calibrated U values for many
transition metals of interest using the approach outlined in Wang et
al.'s work[^5]. At the present moment, U values have been calibrated for
transition metal oxide systems only. The choice of systems to which we
apply U was largely determined by our experience and by systematic
benchmarking. It is very likely that we will expand calibration of U
values to more chemical systems in the future.

Calibration of U values
-----------------------

The U values were obtained by fitting to experimental binary formation
enthalpies as described in Wang et al.'s work, which is simple and
accurately reproduces phase stabilities. A least squares method of
obtaining the correct U value was used, as follows:

1.  For each non-overlapping formation energy reaction considered, we
    find the region where the formation energy error passes zero. For
    the V-O system, this includes the following:
    *  $\ce{2 V2O3 + O2 -> 4 VO2}$
    *  $\ce{4 VO2 + O2 -> 2 V2O5}$
2.  For each formation energy region identified, we fit the linear
    equation $\\begin{align} \\mbox{Error/redox} & = m U + c \\end{align}$ to
    the final U range. In the case of V, we will have two sets of (m,c).
2.  We find the U value that minimizes the sum of square Error / Redox.
4.  In the case of V, we get a U value of 3.25.

U values
--------

The full list of U values used is described in the table below. For
oxides containing any of the elements, both GGA and GGA+U calculations
were performed.

| Element | System | Fitting Reaction                  | Redox Couple         | Calibrated U (eV) | Comments                                                                       |
|:--------|--------|-----------------------------------|----------------------|-------------------|--------------------------------------------------------------------------------------------------------------------|
| Co      | Oxides | $\ce{6 CoO + O2 -> 2 Co3O4}$      | $\ce{Co^{2+} -> Co^{2.67+}}$ | 3.32          |                                                                                |
| Cr      | Oxides | $\ce{2/3 Cr2O3 + O2 -> 4/3 CrO3}$ | $\ce{Cr^{3+} -> Cr^{6+}}$      | 3.7               |                                                                                |
| Fe      | Oxides | $\ce{6 FeO + O2 -> 2 Fe3O4}$ <br> $\ce{4 Fe3O4 + O2 -> 6 Fe2O3}$   | $\ce{Fe^{2+} -> Fe^{2.67+}}$ <br> $\ce{Fe^{2.67+} -> Fe^{3+}}$    | 5.3               |                                                                                |
| Mn      | Oxides | $\ce{6 MnO + O2 -> 2 Mn3O4}$  <br>  $\ce{Mn3O4 + O2 -> 3 MnO2}$  | $\ce{Mn^{2+} -> Mn^{2.67+}}$ <br> $\ce{Mn^{2.67+} -> Mn^{4+}}$    | 3.9               | $\ce{Mn2O3}$ was explicitly excluded from calibration set due to the large number of atoms in its unit cell.                              |
| Mo      | Oxides | $\ce{2 MoO2 + O2 -> 2 MoO3}$    | $\ce{Mo^{4+} -> Mo^{6+}}$ | 4.38              |                                                                                |
| Ni      | Oxides | $\ce{Li2O + NiO + O2 -> LiNiO2}$    | $\ce{Ni^{2+} -> Ni^{3+}}$ | 6.2               | Binary formation energies are not readily available for Ni. The Ni U calibration was performed using a ternary oxide formation energy.[^5]  |
| V       | Oxides | $\ce{2 V2O3 + O2 -> 4 VO2}$ <br> $\ce{4 VO2 + O2 -> 2 V2O5}$ | $\ce{V^{3+} -> V^{4+}}$ <br> $\ce{V^{4+} -> V^{5+}}$  | 3.25              | $\ce{VO}$ was explicitly excluded from calibration due to its known metallic nature.                                               |
| W       | Oxides | $\ce{2 WO2 + O2 -> 2 WO3}$  | $\ce{W^{4+} -> W^{6+}}$        | 6.2               |                                                                                |

Caveats
-------

The U values are calibrated for phase stability analyses, and should be
used with care if applied to obtain other properties such as band
structures. Also, the U values depend on the pseudopotential used. A
discussion of the pseudopotentials used in the Materials Project can be
found [here](/methodology/pseudopotentials).

Authors
-------

1.  Shyue Ping Ong

References
----------

[^1]: F. Zhou, M. Cococcioni, C. A. Marianetti, D. Morgan and G. Ceder.
    First-principles prediction of redox potentials in transition-metal
    compounds with LDA+U. Physical Review B, 2004, 70, 235121.
    <doi:10.1103/PhysRevB.70.235121>

[^2]: M. Cococcioni, S. de Gironcoli, Linear response approach to the
    calculation of the effective interaction parameters in the LDA+U
    method. Physical Review B, 2005, 71, 035105.
    <doi:10.1103/PhysRevB.71.035105>

[^3]: L. Wang, T. Maxisch, & G. Ceder. Oxidation energies of transition
    metal oxides within the GGA+U framework. Physical Review B. 2006,
    73, 195107, <doi:10.1103/PhysRevB.73.195107>

[^4]: A. Jain, G. Hautier, S. P. Ong, C. Moore, C. Fischer, K. A.
    Persson, & G. Ceder. Formation enthalpies by mixing GGA and GGA + U
    calculations. Physical Review B, 2011, 84(4), 045115.
    <doi:10.1103/PhysRevB.84.045115>

[^5]: M. Wang, A. Navrotsky Enthalpy of formation of LiNiO2, LiCoO2 and
    their solid solution, LiNi1-xCoxO2, Solid State Ionics, vol. 166,
    no. 1-2, pp. 167-173, Jan. 2004.