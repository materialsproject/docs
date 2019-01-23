# Battery Explorer Manual
## Introduction
## Using the Li-ion Battery Explorer
### Advanced options
## The Search Result Table
## Viewing Details of a battery compound
### Voltage curve
### O<sub>2</sub> evolution curve
### Overall materials properties
### Voltage pair properties
## Diffusion data
## Bond valence difffusion pathway information
## Classical bond valence method
## Bond valence site energy calculation
A natural way to combine the bond valence approach with penalty functions for repulsions between the mobile and immobile cation types is to use Coulomb repulsion, but then the bond valence mismatch term also has to be expressed in energy units. In reference[^4] we discuss in detail an effective way to translate the squared bond valence (sum) mismatches into approximate a Morse-type bond valence site energy for the mobile ion[^5]. The approach automatically includes bond asymmetry penalties (for details and a table of the employed parameters see reference Adams & Rao[^6]). In brief, the bond valence site energy E(Li) for a cation Li at a given position is calculated from the position of its N anion neighbours Xj (j = 1,…,N) and P immobile cations is calculated as:

$E(Li)=\sum_{j=1}^{N}\{{\frac{D_{Li-X_j}}{s^2_{min,Li-X_j}}(exp[\frac{R_{o,Li-X_j}-R_{Li-X_j}}{b_{Li-X_j}}]-s_{min,Li-X_j})^2-D_{Li-X_j}}\}+E_{Coulomb}$

where 
* $R_{Li-X_j} is the distance between the central Li+ cation and the neighbouring anion $X_j$
* $R_{0,Li-X_j} and $b_{Li-X_j} are the tabulated bond valence parameters for the interaction between a Li cation and anions of type $X_j$
*$s_{min,Li-X_j}$ is the bond valence for the equilibrium bond distance $R_{min,Li-X_j}$ which itself is estimated from the bond valence parameters, the tabulated preferred coordination number NC and the absolute softnesses σ of the respective ions using the empirical formula:
$R_{min,Li-X_j}=R_{0,Li-X_j}*[0.9185+0.2285*|\sigma{}_{Li}-\sigma{}_{X}|]-b_{0,Li-X_j}$
* The bond dissociation energy $D_{Li-X_j}$ is estimated from
$D_{Li-X_j}=14.4\frac{eV}{\AA}*\frac{1*V_{id}(X_j)}{R_{min,Li-X_j}\sqrt{n_{Li}n_{X_j}}}*\frac{b^2_{Li-X_j}}{2}$


## Limitations of the approach
The bond valence site energy model essentially attempts to predict the energetic environment of mobile ions from a static structure model. Thus the approach, especially when applied to ab initio generated structure models cannot be expected to yield activation energies with high precision, but should still yield useful semi-quantitative information.

The static nature of the approach inherently leads to an overestimation of migration barriers, as the approach essentially calculates the energy that would be required (in the frame of the assumed force-field) to move the mobile ion without taking into account relaxations of the environment. To mitigate this overestimation the resulting energies are scaled by a factor of 0.8 that should work reasonable well for a wide range of network structures, but will significantly under¬estimate the effect of relaxations in structures held together by weak forces only such as layered structures. In the current version we refrained from using different scaling factors for different structures, knowing that this will tend to overestimate energy barriers for layered structures (roughly by a factor of two).

Another factor limiting the precision is the inherent tendency of the ab initio approaches to yield structure models with too large unit cell volumes. As the bond valence parameters are derived from fits to experimental reference crystal structure, they tend to yield somewhat lower than ideal bond valence sums when applied to ab initio models. A way to quantify this source of error is the Global Instability Index specified for each structure.

## Global instability index (GII)
The "global instability index" GII as defined by Salinas-Sanchez et al. is commonly used to quantify the plausibility of structure models. Essentially it represents a root mean square average deviation of the observed bond valence sums V(i) for all unique atoms i from the expectation values Vid(i) (i.e. the absolute value of the oxidation state) in a crystal structure:

$GII=\sqrt{\frac{\sum_{i=1}^{N}[(V(i)-V_{id}(i))^2]}{N}}$

The "global instability index" GII as defined by Salinas-Sanchez et al. is commonly used to quantify the plausibility of structure models. Essentially it represents a root mean square average deviation of the observed bond valence sums V(i) for all unique atoms i from the expectation values Vid(i) (i.e. the absolute value of the oxidation state) in a crystal structure:
## References
[^1] S. P. Ong, L. Wang, B. Kang, G. Ceder., The Li-Fe-P-O2 Phase Diagram from First Principles Calculations, Chemistry of Materials, vol. 20, Mar. 2008, pp. 1798-1807. [10.1021/cm702327g](https://doi.org/10.1021/cm702327g)  
[^2] S.P. Ong, A. Jain, G. Hautier, B. Kang, and G. Ceder, Thermal stabilities of delithiated olivine MPO4 (M=Fe, Mn) cathodes investigated using first principles calculations, Electrochemistry Communications, vol. 12, 2010, pp. 427-430. [10.1016/j.elecom.2010.01.010](https://doi.org/10.1016/j.elecom.2010.01.010)  
[^3] S. Adams, Solid State Ionics 177, 1625 (2006).  
[^4] S. Adams, Acta Crystallogr. B, Struct. Sci. 57, 278 (2001).  
[^5] S. Adams and R. Prasada Rao, Phys. Chem. Chem. Phys. 11, 3210 (2009).  
[^6] S. Adams and R. P. Rao: High power Li ion battery materials by computational design; Phys. Status Solidi A 208, 1746–1753 (2011). [10.1002/pssa.201001116](https://doi.org/10.1002/pssa.201001116)  
## Authors
