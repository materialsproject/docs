# Nanoporous Materials Explorer

## Introduction
Nanoporous materials are defined as materials having pore less than 100 nm in size which are often comparable to the size of individual molecules. This gives rise to a series of unique properties, making nanoporous materials useful for industrially important applications such as gas storage, separations, catalysis, et cetera. A vast number of unique nanoporous materials can be synthesized, varying in chemical composition and pore topology. Thousands such materials have already been synthesized and hundreds of thousand hypothetical materials have been computationally predicted. In addition, a considerable number of computational screening studies have appeared in the literature that examine the potential of nanoporous materials for a series of applications. This has generated a substantial amount of data that cannot be presented efficiently by traditional publications. To address this, the Nanoporous Explorer App provides a platform for the aggregation and presentation of data related to nanoporous materials and their properties in an interactive way. The app aims to ease the access to the available information in a way that was not previously possible and enable the identification of promising materials based on their performance and properties. The data for the Nanoporous Explorer App are predicted, measured, and/or maintained by the [Nanoporous Materials Genome Center](http://www1.chem.umn.edu/nmgc/) (NMGC).

This manual covers the description of the classes of materials and type of properties currently available.

## Using the Nanoporous Explorer App

The search interface of the Nanoporous Explorer App is built around an interactive 2-dimensional scatter plot. In order to initiate a search and generate a scatter plot, you need to select one or more of the available material and adsorbate classes from the drop down menu at the top of the screen and hit the “Explore Nanoporous Materials” button. The default selection includes all the available material classes and no adsorbates. 

### Interfacing with the data
Once a scatter plot has been generated, for a set of material and adsorbate classes, you can click and drag the mouse cursor on the plot to zoom in on a specific area. When zoomed in, a “reset zoom” button will appear to go back to the default plot size. The sliders on the right of the screen can adjust the pressure and temperature range of the data. You can click on a point in the scatter plot to access a list of materials in the vicinity of the chosen point. The materials close to the chosen point will appear as a table below the scatter plot, and you can obtain detailed information about the material by clicking on each material in the table. The details page for each material provides all the properties available for this specific material. Such details include pore characteristics and material properties for all the materials as well as adsorption properties (Henry’s constants, adsorption isotherms and the heats of adsorption) for a subset of the materials.

## Material Classes

### CoRE MOFs
Computation-Ready, Experimental MOF database was constructed by a collaboration within the Nanoporous Materials Genome Center. The database is derived from the Cambridge Structural Database (CSD), which contains a large number of small organic and inorganic molecules as well as periodic structures. After the construction of the database, a large-scale GCMC simulation was carried out on all the structures in the database for methane storage and working capacity [^1].

#### Key Assumptions in Creating the CoRE MOF Database
1. Stoichiometry information provided by the CSD is correct. Crystal structures were categorized and processed based on the stoichiometry text information provided by the CSD.
    1. If the stoichiometry string for a given structure did not contain commas, we assumed that the structure does not contain additional species (solvents or ions) apart from the MOF framework.
    2. If the stoichiometry string did not contain "+" or "-" signs, we assumed that the structure does not contain ionic species.
2. The disorder information provided by the CSD gives complete information about the presence of disorder in the crystal structure.
    We assume that the structures without such text do not contain any disorder and represent the pristine crystal structure as reported in the literature.

#### Database Construction Procedure
Four steps were taken to extract the crystal structures from the CSD and make them computation-ready:
1. Removal of free solvents and coordinated solvents.
2. Judicious retention of charge-balancing ions in the framework atoms to make the crystal charge neutral.
3. Text Mining to recover structures with no framework disorder.
4. Manual editing of any disordered structures.

#### Graph-based representation of Molecular Structures
Solvent removal and ion retention procedures rely on the construction of molecular graph representation of a MOF crystal. To construct the periodic adjacency matrix for each structure the Atomic Simulation Environment NeighborList module is used. Two atoms are considered bonded if the distance between them is less than the sum of their CSD covalent radii plus a skin distance of 0.3 Å. The skin distance is chosen to be slightly smaller than the CSD definition (0.4 Å) such that the terminal atom connected to the metal atom does not form another bond with other nearby atoms. The adjacency matrix is passed to the SciPy connected components module to identify the bonded components in each structure.

#### Removal of Free Solvents and Coordinated Solvents
All bonded components in the molecular graph of each structure other than the MOF framework and charge-balancing ions were removed. The MOF framework was defined as the highest molecular weight bonded component of the graph. Interpenetrated MOF frameworks were retained by identifying the number of atoms, N, in the largest bonded component in the structure and retaining all additional components having at least 0.5N atoms. The bonded component corresponding to the MOF framework often includes undesirable solvent bound to unsaturated metal centers. To remove these coordinated solvent molecules, we performed a trial “cut” on all bonds between metal centers oxygen atoms. If the number of bonded clusters detected by the connected component algorithm remained constant, the bond was restored. If the number of bonded components increased, the entire new component was considered a solvent molecule and removed. An exception was built into the algorithm to retain hydroxyl groups bonded to metal centers.

#### Retention of Charge-Balancing Ions
Many MOF structures with associated charge-balancing ions also contain undesirable neutral solvent molecules. To discriminate between ionic species and neutral solvent molecules, the elemental compositions of the bonded components in a molecular graph of each structure were compared to the chemical formulas reported by the CSD using an in-house python script. The bonded components are the independent “molecules” within each structure; these include the MOF framework, the ionic species, and any neutral solvent molecules. The bonded components with elemental compositions matching the composition of the ions reported by the CSD were exempted from deletion in the solvent removal step.

### Hypothetical MOFs
Wilmer and co-workers at Northwestern University have created a database of 137,953 hypothetical Metal-organic frameworks [^2]. Current analysis of this database includes Grand Canonical Monte Carlo (GCMC) simulations to estimate the methane storage and working capacity of MOFs using Universal Force Field parameters (UFF). Among the top 300 hypothetical MOFs, Wilmer and co-workers identified target materials for synthesis and measured gas adsorption characteristics and found that excellent agreement between simulation and experiment. The hypothetical MOF database has also been used to define the structure-property relationship for $\ce{CO2}$ and $\ce{N2} separation[^3], Xe/Kr separation[^4], and hydrogen storage applications[^5].

#### Building Blocks
A novel, bottom-up algorithm was developed to speed up structure enumeration. One hundred and two building blocks with varying degree of geometry and number of acids sites (e.g., COOH- sites) were used. The building blocks are divided into three main groups: metal nodes, organic linkers, and functional groups. Table 1 and Figure 1 summarizes the building blocks used in structure generation algorithm for Ref. [^1].

To make the hypothetical MOF database relevant for hydrogen storage, only magnesium atoms were incorporated into the linker as a functional group, and new types of linkers were used as building blocks. The two hydrogen atoms on the phenyl ring group were substituted with two oxygen atoms and one magnesium atom. For each MOF structure, 0%, 50% and 100% magnesium functionalization was used. The list of building blocks and functionalization scheme is shown in Figure 2.

#### Generation Algorithms
The generation procedure creates hypothetical MOFs by recombining building blocks derived from crystallographic data of already synthesized MOFs. Atoms are grouped into building blocks based on reagents used in reported synthesis procedures as shown in Table 1. A building block can be combined with any other building block provided that the local geometry and chemical composition are the same as in crystallographically determined structure. Building blocks are combined in a piece-wise manner. When atomic overlap occurs at a particular step, a different building block or connection site is chosen until all possibilities are exhausted. Note that there is no force field (or quantum mechanical) energy minimizations involved; the pieces are connected according to geometric rules that govern how the building blocks are connected in already synthesized MOFs.  Figure 2 summarizes the generation step discussed above.

### Hypothetical Zeolites

Zeolites are crystalline nanoporous material made from tetrahedrally coordinated silicon or alumnimum atoms connected by oxygen atoms. Zeolites are naturally occuring, but are usually produced synthetically for industrial applications in adsorption and catalysis. The International Zeolite Association database lists 218 silaceous zeolite structures that have been synthesized in the laboratory 6. Synthesis of new zeolite structures is an active area of research.
Deem et al. generated a large database of hypothetical silica zeolite structures that could serve as targets for experimental  synthesis [^7],[^8]. First, graphs of possible framework were enumerated by placing tetrahedral nodes (“T-atoms”) in all 230 symmetry groups over a wide range of lattice constants. These candidate structure were then annealed with the Sander-Leslie-Catlow interatomic potential to yield over 300,000 structures within 30 kJ mol-1 of quartz.  

### Other Hypothetical Materials
In addition to MOFs and Zeolites currently a set of 10,000 computational predicted porous polymeric networks (PPNs) are available [^9].

## Properties

### Henry's Constants
The Henry's constant (KH), expressed in mol/kg/bar for gas phase system, defines the slope on the adsorption isotherm at the low-pressure limit. Computational calculation of Henry's constant can be efficiently carried out using Widom’s ghost particle insertion [^10] method over the simulation cell volume and calculating the energy difference of the system with the sorbate molecule in the nanoporous material (adsorbed phase) and with the sorbate molecule in the surrounding fluid phase. The Henry's constant is related to the energy difference for the molecule in the simulation cell [^11],[^12] by,

$$K_H={M\over8{\pi}V{\rho}RT}{\int}e^{-{\beta}U}dr={1\over{RT}}{\sum_{i=1}^{N_{points}}{\exp(-{\beta}U_{i}^{ads})}\over{N_{points}}}$$ Eq. 1

The obtained Henry’s constant can be used to calculate the free energy of adsorption in the infinite-dilution limit of the sorbate molecule via the following thermodynamic relationship  (Equation 2):

$$A_{ads}=-RT\text{ln}(RT{\rho}_sK_H)$$ Eq.2

#### Application to Large-scale screening
Recently, the ratio of Henry’s constant has been used to rapidly assess the materials selectivity of one molecule over another (e.g., $\ce{CO2}$ over $\ce{H2}$). Examples of such studies in literature include work by Haldoupis, et. al ($\ce{CO2}$/$\ce{H2}$)[^13] and Watanabe, et. al. ($\ce{CO2}/$\ce{N2}$)[^14].

### Absorption Isotherms
In porous materials, such as zeolites, metal-organic frameworks (MOFs), and porous polymer networks (PPNs), adsorption is the physical adsorption of molecules from a gas or liquid phase onto the solid surface, such as pore wall. An adsorption isotherm is the loading of adsorbate as a function of pressure and/or composition at a given temperature in thermodynamic equilibrium. Adsorption isotherms are sometimes normalized by the mass or volume of the adsorbent to allow comparison of the adsorption capacity of different materials.  Adsorption isotherms are fundamental in characterizing the suitability of nanoporous materials for gas storage and separation applications. Experimentally measured nitrogen and argon isotherms are used to determine the surface area and pore size distribution of nanoporous materials [^15].
The adsorption isotherms can be predicted computationally using Grand Canonical Monte Carlo (GCMC) or Gibbs Ensemble Monte Carlo (GEMC) techniques. This is useful for efficiently screening large databases of experimentally synthesized and hypothetical constructed nanoporous materials for desirable adsorption properties [^1]. The accuracy of the simulations depends on choice of the force fields that describe fluid-fluid and fluid-solid interactions. Nanoporous Materials Explorer includes GCMC simulation results for methane uptake in each material at a temperature of 298 K and pressures of 5.8, 35, and 65 bar.

### Heat of Adsorption
In two phase gas-liquid systems, the Clausius-Clapeyron equation states that the latent heat of vaporization of a pure component is approximately proportional to the slope of a plot of $\text{ln}(P_{sat})$ vs. $1/T$ [^16]. The analogous expression for two phase systems consists of gas and porous materials defines the isosteric heat of adsorption qst [^17]:

$$q_{st}={RT^2}\left ({{\partial{\text{ln}P}}\over{\partial{T}}}\right )_N$$ Eq.3

Therefore, the isosteric heat of adsorption may be obtained by plotting ln P vs T relations from several isotherms at a constant adsorbate loading of N. The heat of adsorption is positive by definition, and the negative heat of adsorption is also known as the differential enthalpy of adsorption. The negative sign reflects the exothermic nature of adsorption.
The heat adsorption is a quantitative measure of whether a species is strongly adsorbing or weakly adsorbing, with values typically ranging from 10 to 40 kJ/mol. Heats of adsorption can be determined experimentally by differential calorimetry. 
In molecular simulations, the isosteric heat of adsorption can be calculated from a fluctuation method [^1]:

$$q_{st}={RT}-{{\langle{VN}\rangle-\langle{V}\rangle\langle{N}\rangle}\over{\langle{N^2}\rangle-\langle{N}\rangle^2}}$$ Eq.4

Here, V is the potential energy per adsorbate molecule. The angled brackets indicate an ensemble average taken over a grand-canonical Monte Carlo (GCMC) simulation at low loading to minimize the influence of adsorbate-adsorbate interactions.  In the limit of low loading, the heat of adsorption is related to the Henry’s constant by [^18]:


$$q_{st}={{\partial{\text{ln}K_H}}\over{\partial{\beta}}}$$ Eq.5

Here, β is $1/(k_BT)$ where $k_B$ is the Boltzmann constant.

### DDEC Point Charges
Partial point charges are provided for a majority of the structures in the CoRE MOF database. These charges were calculated using the Density Derived Electrostatic and Chemical (DDEC) method that involves atomic population analysis on the electron and spin density distributions generated by quantum chemistry methods [^19].
DDEC charges reproduce atomic chemical states and the electrostatic potential surrounding a material.  Such charges are well suited for constructing force fields used in atomistic simulations such as classical molecular dynamics or Monte Carlo simulations.

#### Calculation Details
Charges were assignment using the January 2014 version of the DDEC program provided by Manz et.al [^20]. The electron and spin density distributions used as input for the DDEC code were generated in the Vienna Ab Initio Simulation Package (VASP) software [^21]. Single point plane wave density functional theory calculations with the PBE functional were performed. 
While the DDEC method provides an individual charge for each atom in the system, it is computationally more convenient to distinguish between atom types within a structure. Therefore, point charges are provided for each atom type in a structure. Atom types are assigned based on the atom’s neighboring environment and charges for each atom type are averaged to obtain a net neutral system.

### Pore Descriptors
A series of pore descriptors have been proposed in the literature as way of quantifying the unique pore topology present in each material. We have currently collected four such descriptors:

* Pore Limiting Diameter (PLD): Is defined as the smallest opening along the pore that a molecule needs to cross in order to diffuse through this material. This quantity is also know as the largest free sphere. Reported in units of Å. 
* Largest Cavity Diameter (LCD): Is defined as the largest opening along the pore. This quantity is also known as the largest included sphere. Reported in units of Å.
* Void Fraction: Is defined as the fraction of the unit cell volume that is accessible to specific molecule. All the values have been so far computed for a $\ce{CH4}$ molecule using a sphere of radius 1.645 Å.
* Accessible Surface Area: Is defined as the surface area that a sorbate molecule can access inside the pores of a material. It is computed using the method by Düren et al. [^22]. All the values have been so far computed for a $\ce{CH4} molecule using a sphere of radius 1.645 Å. Reported in units of $m^2/\text{cm}^3$

All the pore descriptors have been calculated using the open source software Zeo++ (http://www.maciejharanczyk.info/Zeopp/about.html)

### P-XRD Patterns
Simulated powder X-ray diffraction (PXRD) patterns derived from crystallographic data are provided for nanoporous materials. PXRD is a widely used technique for characterizing solid materials. The scattering of X-rays from atoms produces a diffraction pattern, which contains information about the atomic arrangement within the crystal. Therefore, the PXRD pattern can serve as the fingerprint to identify the phase and structure of a solid materials [^23].
PXRD pattern of a solid material is commonly recorded using a diffractometer. The results can be used to determine phase composition, unit cell lattice parameters, crystal structure, Texture/Orientation and crystalline size.

## References
[^1]: 
[^2]:
[^3]:
[^4]:
[^5]:
[^6]:
[^7]:
[^8]:
[^9]:
[^10]:
[^11]:
[^12]:
[^13]:
[^14]:
[^15]:
[^16]:
[^17]:
[^18]:
[^19]:
[^20]:
[^21]:
[^22]:
[^23]:

## Authors
* Jeffrey Camp
* Greg Chung
* Emmanuel Haldoupis
* Dalar Nazarian
* Tess Smidt

##TODO
* Add table
* Add figures
* Add reference doi's
