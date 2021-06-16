# Elasticity

## Introduction

The elastic constants from the Materials Project (MP) are calculated
from first principles Density Functional Theory (DFT). The process is
started by performing an accurate structural relaxation for each
structure, to a state of approximately zero stress. Subsequently,
perturbations are applied to the lattice vectors and the resulting
stress tensor is calculated from DFT, while allowing for relaxation of
the ionic degrees of freedom. Finally, constitutive relations from
linear elasticity, relating stress and strain, are employed to fit the
full 6x6 elastic tensor. From this, aggregate properties such as Voigt
and Reuss bounds on the bulk and shear moduli are derived. Multiple
consistency checks are performed on all the calculated data to ensure
its reliability and accuracy.

## Formalism

The relaxed lattice vectors
\\( \\{\mathbf{a}\_{1} , \mathbf{a}\_{2} , \mathbf{a}\_{3} \\}\\)
are taken and these are deformed according to each of the 6 deformation
gradients \\(\mathbf{F}\\) as shown in the equations below. These 6
deformation gradients are applied one-by-one to the relaxed structure so
that only one independent deformation is considered each time. For each
of the 6 deformation modes, 4 different default magnitudes of
deformation are applied:
\\(\delta\_{1} \in \left\\{-0.01, -0.005, +0.005, +0.01\right\\}\\)
(pertaining to non shear-modes) and
\\(\delta_2 \in \left\\{ -0.06, -0.03, +0.03, +0.06 \right\\}\\)
(pertaining to shear-modes). This leads to a total of 24 deformed
structures, for which the stress tensor, \\(\mathbf{S}\\), is
calculated, allowing for relaxation of the ionic degrees of freedom.
Note that in this work, conventional unit cells, obtained using
`pymatgen.symmetry.SpacegroupAnalyzer.get_conventional_standard_structure`
are employed for all elastic constant calculations. In our experience,
these cells typically yield more accurate and better converged elastic
constants than primitive cells, at the cost of more computational time.
We suspect this has to do with the fact that unit cells often exhibit
higher symmetries and simpler Brillouin zones than primitive cells (an
example is face centered cubic cells).

\\[\boldsymbol{F}=
\left[{\begin{matrix}
1 + \delta \_{1} & 0 & 0 \\\\
0 & 1 & 0 \\\\
0 & 0 & 1 \\\\
\end{matrix}}\right]\,\\]

\\[\boldsymbol{F}=
\left[{\begin{matrix}
1 & 0 & 0 \\\\
0 & 1 + \delta \_{1} & 0 \\\\
0 & 0 & 1 \\\\
\end{matrix}}\right]\,\\]

\\[\boldsymbol{F}=
\left[{\begin{matrix}
1 & 0 & 0 \\\\
0 & 1 & 0 \\\\
0 & 0 & 1 + \delta \_{1} \\\\
\end{matrix}}\right]\,\\]

\\[\boldsymbol{F}=
\left[{\begin{matrix}
1 & \delta \_{2} & 0 \\\\
0 & 1 & 0 \\\\
0 & 0 & 1 \\\\
\end{matrix}}\right]\,\\]

\\[\boldsymbol{F}=
\left[{\begin{matrix}
1 & 0 & \delta \_{2} \\\\
0 & 1 & 0 \\\\
0 & 0 & 1 \\\\
\end{matrix}}\right]\,\\]

\\[\boldsymbol{F}=
\left[{\begin{matrix}
1 & 0 & 0 \\\\
0 & 1 & \delta \_{2} \\\\
0 & 0 & 1 \\\\
\end{matrix}}\right]\,\\]

\\[\mathbf{E}=\frac{1}{2}(\mathbf{F^T} \mathbf{F} - \mathbf{I})\,\\]

We employ the Green-Lagrange strain tensor, \\(\mathbf{E}\\), in this
work, defined above. The 6x6 elastic tensor is calculated from the
equation below, with \\(\mathbf{E}\\) again the Green-Lagrange strain
tensor and \\(\mathbf{S}\\) the calculated stress tensor. The components
are calculated from a linear least-squares-fit if stress versus strain.
We make use of the following Voigt-notation in this work:
\\(11 \mapsto 1\\), \\(22 \mapsto 2\\), \\(33 \mapsto 3\\),
\\(23 \mapsto 4\\), \\(13 \mapsto 5\\), \\(12 \mapsto 6\\).

\\(\left[
\begin{array}{c}
S\_{11} \\\\
S\_{22} \\\\
S\_{33} \\\\
S\_{23} \\\\
S\_{13} \\\\
S\_{12}
\end{array}
\right]
=
\left[
\begin{array}{cccccc}
C\_{11} & C\_{12} & C\_{13} & C\_{14} & C\_{15} & C\_{16} \\\\
C\_{12} & C\_{22} & C\_{23} & C\_{24} & C\_{25} & C\_{26} \\\\
C\_{13} & C\_{23} & C\_{33} & C\_{34} & C\_{35} & C\_{36} \\\\
C\_{14} & C\_{24} & C\_{34} & C\_{44} & C\_{45} & C\_{46} \\\\
C\_{15} & C\_{25} & C\_{35} & C\_{45} & C\_{55} & C\_{56} \\\\
C\_{16} & C\_{26} & C\_{36} & C\_{46} & C\_{56} & C\_{66} \\\\
\end{array}
\right]
\left[
\begin{array}{c}
E\_{11} \\\\
E\_{22} \\\\
E\_{33} \\\\
2 E\_{23} \\\\
2 E\_{13} \\\\
2 E\_{12}
\end{array}
\right]\\)

Different choices of lattice vectors with respect to a Cartesian
coordinate system may lead to elastic tensors that look different from
what might be expected. For example, for the hexagonal crystal system it
is commonly stated that \\(C\_{11} = C\_{22}\\). However, this is true
under the conditions that lattice vectors \\(\mathbf{a}\_{1}\\) and
\\(\mathbf{a}\_{2}\\) are both in the basal plane, whereas
\\(\mathbf{a}\_{3}\\) is orthogonal to the basal plane. Hence, the
elastic tensor can only be completely specified when the lattice vectors
are expressed in a given coordinate system. To avoid confusion, we
present the elastic tensor in 2 ways. First, the elastic tensor is
presented for the exact choice of lattice vectors as presented on the
Materials Project webpage. This is consistent with the cif-file of the
"conventional standard" structure, which can also be downloaded from the
Materials Project webpage. Elastic tensors can also be expressed in a
standard format according to the IEEE standard. The standardized
IEEE-format specifies the precise choice of lattice vectors in a
coordinate system and thereby unambiguously defines the components of
the elastic tensor [^1]. In most cases, the elastic tensors in the
POSCAR-format and the IEEE-format are identical. When the elastic tensor
in POSCAR-format and IEEE-format are not identical however, they are
related by a rotation. Note that IEEE tensors can be obtained using the
get_ieee_tensor method for any of the subclasses of
pymatgen.analysis.elasticity.tensors.TensorBase (which include
ElasticTensor and PiezoTensor).

## Derived elastic properties

From the elastic tensor defined above, a number of aggregate and derived
properties is calculated. These properties are all available on the
Materials Project webpage and are shown in the Table 1. As described
above, the elastic tensor is presented in POSCAR-format. From the
elastic tensor in POSCAR-format, the compliance tensor is calculated and
reported. Also reported are Voigt, Reuss and Voigt-Reuss-Hill [^2]
bounds on the bulk and shear moduli for polycrystalline materials.
Finally, the elastic anisotropy index [^3] and isotropic Poisson ratio
are reported.

| Property                                  | Unit           | Description                                                                                                          | Equation                                                                                                                                |
| ----------------------------------------- | -------------- | -------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| Elastic tensor, \\(C\_{ij}\\)             | GPa            | Tensor, describing elastic behavior, corresponding to IEEE orientation, symmetrized to crystal structure             | see main text                                                                                                                           |
| Elastic tensor (original), \\(C\_{ij}\\)  | GPa            | Tensor, describing elastic behavior, unsymmetrized, corresponding to POSCAR (conventional standard cell) orientation | see main text                                                                                                                           |
| Compliance tensor, \\(s\_{ij}\\)          | GPa\\(^{-1}\\) | Tensor, describing elastic behavior                                                                                  | \\(s\_{ij} = C\_{ij}^{-1}\\)                                                                                                            |
| Bulk modulus Voigt average, \\(K\_{V}\\)  | GPa            | Upper bound on \\(K\\) for polycrystalline material                                                                  | \\(9K\_{V}=\left(C\_{11}+C\_{22}+C\_{33}\right) + 2\left(C\_{12}+C\_{23}+C\_{31}\right)\\)                                              |
| Bulk modulus Reuss average, \\(K\_{R}\\)  | GPa            | Lower bound on \\(K\\) for polycrystalline material                                                                  | \\(1 / K\_{R} = \left(s\_{11}+s\_{22}+s\_{33}\right) + 2\left(s\_{12}+s\_{23}+s\_{31}\right)\\)                                         |
| Shear modulus Voigt average, \\(G\_{V}\\) | GPa            | Upper bound on \\(G\\) for polycrystalline material                                                                  | \\(15 G\_{V} = \left(C\_{11}+C\_{22}+C\_{33}\right)-\left(C\_{12}+C\_{23}+C\_{31}\right) + 3\left(C\_{44}+C\_{55}+C\_{66}\right)\\)     |
| Shear modulus Reuss average, \\(G\_{R}\\) | GPa            | Lower bound on \\(G\\) for polycrystalline material                                                                  | \\(15 / G\_{R} = 4\left(s\_{11}+s\_{22}+s\_{33}\right)-4\left(s\_{12}+s\_{23}+s\_{31}\right) + 3\left(s\_{44}+s\_{55}+s\_{66}\right)\\) |
| Bulk modulus VRH average, \\(K\_{VRH}\\)  | GPa            | Average of \\(K\_{R}\\) and \\(K\_{V}\\)                                                                             | \\(2 K\_{VRH} = \left(K\_{V} + K\_{R} \right)\\)                                                                                        |
| Shear modulus VRH average, \\(G\_{VRH}\\) | GPa            | Average of \\(G\_{R}\\) and \\(G\_{V}\\)                                                                             | \\(2 G\_{VRH} = \left(G\_{V} + G\_{R} \right)\\)                                                                                        |
| Universal elastic anisotropy, \\(A^{U}\\) | -              | Description of elastic anisotropy                                                                                    | \\(A^{U} = 5 \left(G\_{V}/G\_{R}\right) + \left(K\_{V}/K\_{R}\right) -6 \geq 0\\)                                                       |
| Isotropic Poisson ratio, \\(\mu\\)        | -              | Number, describing lateral response to loading                                                                       | \\(\mu = \left(3K\_{VRH} - 2G\_{VRH}\right)\\) / \\(\left(6K\_{VRH} + 2G\_{VRH}\right)\\)                                               |

## DFT parameters

To obtain accurate elastic constants from DFT, a well-converged stress
tensor is required. This typically means that more precise
DFT-parameters have to be employed, compared to for example a simple
total energy-calculation. Careful convergence testing and comparison to
experimental results has led to a set of DFT-parameters that yield
elastic constants, converged to within approximately 5 % for over 95 %
of the systems. In choosing DFT-parameters for the calculations, we
distinguish between metals and metallic compounds (metallics) on one
hand and semiconductors and insulators (non-metallics) on the other
hand. The most relevant DFT-parameters used in our HT-calculations are
shown in Table 2. K-point density is expressed in per-reciprocal-atom
(pra). The first-principles results presented in this work are performed
using the projector augmented wave (PAW) method [^3][^4] as implemented
in the Vienna Ab Initio Simulation Package (VASP) [^5][^6][^7]. In all
calculations, we employ the Perdew, Becke and Ernzerhof (PBE) [^8]
Generalized Gradient Approximation (GGA) for the exchange-correlation
functional.
As described in the literature, several filters are used to detect cases
where the elastic tensor might not have been converged properly. For
those cases, the calculation is repeated but now with more stringent
DFT-convergence parameters. Hence, the numerical values in Table 2 are
representative for our calculations, but in some cases more strict
parameters have been used. The calculation details for each compound can
be found on the Materials Project webpage.

|                                | Metallics | Non-metallics |
| ------------------------------ | --------- | ------------- |
| Plane wave energy cut-off (eV) | 700       | 700           |
| Density of k-points (pra)      | 7,000     | 1,000         |
| Pseudo potential               | GGA-PBE   | GGA-PBE       |

![elastic property database](/methodology/img/elasticity/Data_figure_11_22.png)
*Figure 1: Visualization of the current
elastic-property database, consisting of over 1,100 metals and inorganic
compounds. This map shows the shear and bulk moduli, together with
isotropic Poisson ratio and volume-per-atom. See the paper [*Charting
the complete elastic properties of inorganic crystalline
compounds*](http://www.nature.com/articles/sdata20159) for
details.*

## Symmetrization

Tensor symmetrization and IEEE conversion procedures are implemented in
[pymatgen](http://pymatgen.org/_modules/pymatgen/core/tensors.html).
Symmetrization occurs by finding all of the symmetry operations that
correspond to a particular crystal symmetry, and taking the average over
all transformed tensors with respect to these operations. If there are
\\(y\\) symmetry operations are denoted \\(Q\_{ij}^{(x)}\\) then:

\\(C\_{mnop}^{(sym)} = \sum\_{x=1}^y Q\_{im}^{(x)} Q\_{jn}^{(x)} Q\_{ko}^{(x)} Q\_{lp}^{(x)} C\_{ijkl}\\)

## Citation

To cite the elastic constants within the Materials Project, please
reference the following work:

- de Jong M, Chen W, Angsten T, Jain A, Notestine R, Gamst A, Sluiter M,
  Ande CK, van der Zwaag S, Plata JJ, Toher C, Curtarolo S, Ceder G,
  Persson KA, Asta M (2015) Charting the complete elastic properties of
  inorganic crystalline compounds. [Scientific Data 2: 150009](http://www.nature.com/articles/sdata20159)

The paper presents the results of our elastic constant-calculations for
the first batch of 1,181 metals and compounds. Our DFT-parameters, the
workflow and comparison to experiments are described in detail. Also,
the filters in the workflow used for detecting anomalies in the
calculations are described in the paper.

## Authors

1.  Maarten de Jong

## References

[^1]:
    IEEE standard on piezoelectricity. ANSI/IEEE Std 176-1987 0-1
    (1988).

[^2]:
    Hill, R. The elastic behaviour of a crystalline aggregate.
    Proceedings of the Physical Society. Section A 65, 349 (1952).

[^3]:
    Ranganathan, S. I. & Ostoja-Starzewski, M. Universal elastic
    anisotropy index. Physical Review Letters 101, 055504 (2008).

[^4]:
    Blochl, P. E. Projector augmented-wave method. Phys. Rev. B 50,
    17953{17979 (1994).

[^5]:
    Kresse, G. & Joubert, D. From ultrasoft pseudopotentials to the
    projector augmented-wave method. Phys. Rev. B59, 1758{1775 (1999).

[^6]:
    Kresse, G. & Hafner, J. Ab initio molecular dynamics for liquid
    metals. Phys. Rev. B 47, 558{561 (1993).

[^7]:
    Kresse, G. & Furthmuller, J. Efficffient iterative schemes for ab
    initio total-energy calculations using a plane-wave basis set. Phys.
    Rev. B 54, 11169{11186 (1996).

[^8]:
    Perdew, J. P., Burke, K. & Ernzerhof, M. Generalized gradient
    approximation made simple. Physical Review Letters 77, 3865 (1996).
