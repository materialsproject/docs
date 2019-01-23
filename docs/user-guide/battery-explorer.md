# Battery Explorer Manual

## Introduction

The Battery Explorer is a customized tool to search the Materials Project database for Li-ion battery materials satisfying various critical criteria such as voltage, capacity, stability and energy density.

Currently, this app contains approximately ~3,600 lithium intercalation compounds and ~16,000 conversion compounds. However, new compounds are being continuously added to the database, including many new structural predictions.

## Using the Li-ion Battery Explorer

The Li-ion battery explorer is highly customized to make it easy for battery scientists to find the materials that they are interested in quickly. Useful defaults have been set for the voltage range, minimum gravimetric and minimum volumetric capacity. In fact, simply clicking Search in the Battery Explorer without changing any of the fields already brings up many interesting battery compounds. However, if you have a particular chemistry in mind, judicious use of the form fields will help you find the material you want efficiently. Here's a summary of the various fields and how they can be used:

1. Elements - Use this field (alternatively, you can click the mini-periodic table to specify the elements) to limit the search for compounds containing only those elements present in the battery materials. F
2. No. of Elements (inc Li) - Use this field to limit the search to battery compounds containing a total number of elements.
3. Formula - The formula field should be used as an alternative to specifying the elements and number of elements. In fact, typing in the formula field will automatically fill up the element and no. of elements fields with appropriate parameters. The formula field can be used to restrict the search to compounds satisfying a particular chemical formula.
4. Voltage Range - Use this slider to set the voltage range you want to search in.
5. Min. Grav. Capacity - Use this slider to set the minimum gravimetric capacity for the search.
6. Min. Vol. Capacity - Use this slider to set the minimum volumetric capacity for the search.

### Advanced options
1. Excluded elements - Use this field to exclude certain elements from the search. For example, if you want to exclude certain expensive or toxic elements.
2. Materials Id - Use this field to search for a battery material containing a material with a particular Materials Id within the delithiation range.
3. Battery Id - Use this field to search for a battery material with the corresponding battery id.
4. Max. Volt. Step - Use this slider to limit the search to battery materials having a voltage step less than the specified number.
5. Max. Vol. Change - Use this slider to limit the search to battery materials having a volume change upon lithiation/delithiation smaller than the specified percentage.
6. Max. energy above hull - Use this slider to limit how unstable the lithiated or delithiated battery material can be.

## The Search Result Table
The search result table presents the results from your search. You can add or hide fields from the result table by clicking the Show/Hide Button.

We have provided additional tools to aid you in analyzing the results. For example, you can select a few battery compounds by clicking the checkbox on the rightmost column of the table, and then click the "voltage profile" button to show all the voltage profiles in one easy plot for comparison. You can also compare any two materials for structural similarity. Finally, you can click on the BattId of any material to go to the Battery Material page, which provides detailed information about a battery material, including an assessment of oxidative stability, a Jmol view of the molecule, etc.

## Viewing Details of a battery compound

You can click the blue links in any of the search results to see a detailed summary of that battery compound. Each details page is dedicated to one structural framework, e.g. Mn2O4 spinel, and provides information on *all* lithiation levels into this structural framework.

The details view has many components:

### Voltage curve

The voltage curve graph displays the calculated equilibrium voltage versus state of charge. If voltage criteria were specified in the query, the line might be segmented into different colors. The green portion of the curve matches the query, whereas the the blue portion of the curve does not.

### O<sub>2</sub> evolution curve

One concern for cathode design is resistance to O2 release, as O2 release from the cathode can lead to thermal runaway. The O2 evolution diagram determines the equilibrium chemical potentials at which O2 release can be expected, and the amount of O2 released[^1][^2]. One way to read this chart is to look at the chemical potential at which O2 release begins (the first x-value for which the y-axis is greater than zero). Compounds for which O2 release begins at more negative muO2 are more stable with respect to O2 release. Note that the O2 release chart is specific to one lithiation level of the set of compounds forming the cathode system. There is a drop-down that allows you to choose the lithiation level (e.g. fully delithiated, fully lithiated). The muO2 needed for release can be referenced against common binary systems to get an idea of stability to O2 release:

![](https://github.com/sivonxay/mp_wiki_docs/blob/battery/docs/user-guide/img/battery/battery_Muoscale.gif)

### Overall materials properties

The overall materials properties display aggregate or average properties over all lithiation levels of a given structural framework. Note that some lithiation levels presented in this section may be outside the desired range of voltage, stability, or safety. More details are given in the 'Voltage pair properties' section.

### Voltage pair properties

This table displays calculated data for each voltage step along the voltage profile. 

## Diffusion data
The battery diffusion data shown in the Materials Project differs from other data in that it is computed with classical approaches rather than first-principles approaches. In particular, the accuracy of these methods are lower than Density Functional Theory calculations, and in general they are used to make qualitative rather than quantitative predictions. We review the important concepts for understanding the diffusion data in this section.
## Bond valence difffusion pathway information
The bond valence site energy pathways are based on isosurfaces of constant bond valence site energy E(Li) calculated for a grid covering the entire crystal structure. Note that this energy scaled approach builds on, but is slightly different from the conventional bond valence approach yielding information in on a “valence units” scale.

The title line indicates the name of the (delithiated) compound for with the Li migration pathways have been modeled using the empirical bond valence potentials. The subtitle contains information about the plausibility of the underlying structure model in terms of the Global Instability Index GII and translates the GII value into qualitative statement on the reliability of the structure model high (GII < 0.15), average (GII < 0.30), low (GII > 0.30).

The two *pathway graphs* show two different projections of one symmetry-adapted unit cell (which is often a supercell of the primitive P1 cell used for the ab initio calculations) with the Li pathways visualized as three superimposed isosurfaces of constant E(Li). The innermost, darkest isosurface typically represents the regions of lowest bond valence site energy (e.g. equilibrium sites for Li), while the lightest isosurface visualizes a long-rage transport path, if such a path exists for activation energies up to 2.4 eV.

The *main table* then lists the observed *continuous pathways* and classifies them according to the dimensionality of the path and the minimum activation energy that mobile Li have to overcome along this path.

The sites table lists all identified local minima of E(Li) in the structure and qualifies them according to their site energy values into equilibrium sites Li# (or lowest energy sites for compounds not containing Li) and interstitials i#. Symmetry-equivalent sites are listed only once. For some compounds with complex pathways this table also includes information on saddle-points s# along the path to help distinguish otherwise ambiguous connections between Li sites in the structure.

The paths table lists the connections between site pairs, their activation energy. It also includes information regarding the contribution to the long range pathways listed above.
## Classical bond valence method
Empirical relationships between bond length RA-X and the so-called bond valence sA-X= exp[(R0-RA-X)/b] are widely used in crystal chemistry to identify plausible equilibrium sites for an atom in a structure as sites, where the bond valence sum V(A) of A from interactions with all its surrounding counterions X matches its oxidation state.[^3]

A few years ago, we introduced a systematic adjustment of the bond valence parameter b to bond softness.[^4] Together with the inclusion of the weak interactions beyond the first coordination shell, this makes it possible to extend the application range of the bond valence method to assess also non-equilibrium sites more adequately and therefrom to predict pathways for mobile ions in models of local structures as regions in a structure model where the bond valence sum V(A) deviates only marginally from the ideal valence Vid(A) (i.e., its oxidation state). To enhance chemical plausibility of such bond valence mismatch landscapes |ΔV(A)| penalty functions have been introduced that (i) discriminate against sites, where a matching V(A) is achieved by strongly asymmetric coordinations and (ii) exclude sites close to other immobile cation types.

The determination of the empirical bond valence parameters R0 and b is based on fits to large sets of experimental reference structures. Thus it may be expected that their application to ab initio structure models (with typically slightly larger unit cell volumes) causes a somewhat reduced accuracy of the approach.
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

with $nLi$, $nXj$ representing the principal quantum numbers of $Li^+$ and the anion $X_j$; $V_{id}(X_j)$ the absolute value off the nominal charge of anion $X_j$ ($V_{id}(X_j)=1$). Note that a slightly different formula for calculation the dissociation energy applies to transition metal cations.  
*the screened Coulomb repulsion between Li and an the P surrounding immobile cations Mi (i=1,…,P) is
$E_{Coulomb}=\frac{1}{4\pi\epsilon{}_0}\sum_{i=1}^{P}[\frac{q_{Li}q_{M_i}}{R_{Li-M_i}}erfc(\frac{R_{Li-M_i}}{\rho{}_{Li-M_i}}]$
using fractional charges, where the systematic assignment of context sensitive fractional charges again involves the inverse square root of the principal quantum number as a scaling factor (for details see[^4]). The screening factor ρLi-Mi is assumed to equal the sum of the covalent radii of the two ions involved times a scaling factor f that depends on the average absolute cation electronegativity and the average cation charge in the compound. Typical values of f in ternary and quaternary lithium oxides fall into the range 0.74±0.04 and thereby ρ is of the order of 2 Å.

These calculations are repeated for a dense grid of points covering the unit cell (grid size ca. 0.1 Å) and pathways of low activation are identified as regions in the structure for which E(Li) assumes low values. It should be noted that the inclusion of weak interactions to counter-ions beyond the first coordination shell is indispensable for such a modeling ion transport to avoid artifacts when an ion moves across the border of its coordination shell. To limit computation-nal effort the well-converging E(Li) calculation can be cut off at a distance of 5 – 8 Å depending on the atom size and bond softness.

As the parameters vary with the oxidation state of all atoms involved and atomic positions are slightly different, it is expected that transport pathways and especially the activation energies will differ between lithiated and delithiated forms of the cathode material. In the initial release only data for the delithiated phase of the redox couple are shown.

## Limitations of the approach
The bond valence site energy model essentially attempts to predict the energetic environment of mobile ions from a static structure model. Thus the approach, especially when applied to ab initio generated structure models cannot be expected to yield activation energies with high precision, but should still yield useful semi-quantitative information.

The static nature of the approach inherently leads to an overestimation of migration barriers, as the approach essentially calculates the energy that would be required (in the frame of the assumed force-field) to move the mobile ion without taking into account relaxations of the environment. To mitigate this overestimation the resulting energies are scaled by a factor of 0.8 that should work reasonable well for a wide range of network structures, but will significantly under¬estimate the effect of relaxations in structures held together by weak forces only such as layered structures. In the current version we refrained from using different scaling factors for different structures, knowing that this will tend to overestimate energy barriers for layered structures (roughly by a factor of two).

Another factor limiting the precision is the inherent tendency of the ab initio approaches to yield structure models with too large unit cell volumes. As the bond valence parameters are derived from fits to experimental reference crystal structure, they tend to yield somewhat lower than ideal bond valence sums when applied to ab initio models. A way to quantify this source of error is the Global Instability Index specified for each structure.

## Global instability index (GII)
The "global instability index" GII as defined by Salinas-Sanchez et al. is commonly used to quantify the plausibility of structure models. Essentially it represents a root mean square average deviation of the observed bond valence sums V(i) for all unique atoms i from the expectation values Vid(i) (i.e. the absolute value of the oxidation state) in a crystal structure:

$GII=\sqrt{\frac{\sum_{i=1}^{N}[(V(i)-V_{id}(i))^2]}{N}}$

The "global instability index" GII as defined by Salinas-Sanchez et al. is commonly used to quantify the plausibility of structure models. Essentially it represents a root mean square average deviation of the observed bond valence sums V(i) for all unique atoms i from the expectation values Vid(i) (i.e. the absolute value of the oxidation state) in a crystal structure:
## References
[^1]: S. P. Ong, L. Wang, B. Kang, G. Ceder., The Li-Fe-P-O2 Phase Diagram from First Principles Calculations, Chemistry of Materials, vol. 20, Mar. 2008, pp. 1798-1807. [doi:10.1021/cm702327g](https://doi.org/10.1021/cm702327g)  
[^2]: S.P. Ong, A. Jain, G. Hautier, B. Kang, and G. Ceder, Thermal stabilities of delithiated olivine MPO4 (M=Fe, Mn) cathodes investigated using first principles calculations, Electrochemistry Communications, vol. 12, 2010, pp. 427-430. [doi:10.1016/j.elecom.2010.01.010](https://doi.org/10.1016/j.elecom.2010.01.010)  
[^3]: S. Adams, Solid State Ionics 177, 1625 (2006).  
[^4]: S. Adams, Acta Crystallogr. B, Struct. Sci. 57, 278 (2001).  
[^5]: S. Adams and R. Prasada Rao, Phys. Chem. Chem. Phys. 11, 3210 (2009).  
[^6]: S. Adams and R. P. Rao: High power Li ion battery materials by computational design; Phys. Status Solidi A 208, 1746–1753 (2011). [doi:10.1002/pssa.201001116](https://doi.org/10.1002/pssa.201001116)  
## Authors
1. Shyue Ping Ong
2. Anubhav Jain
3. Stefan Adams (diffusion data)
4. Eric Sivonxay
5. Jimmy Shen
