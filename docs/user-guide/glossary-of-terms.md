# Glossary of Terms

## Materials Explorer

## Formula

**Anonymous chemical formula:**
The chemical formula with the element names anonymized to the letters A, B, C, etc.
The order of the anonymized elements is from least atomic fraction to greatest atomic fraction, thus the coefficients are non-decreasing.
For example, both $\ce{TiO2}$ and $\ce{Na2O}$ have an anonymous formula of $\ce{A1B2}$.

## Structure

**Crystal system:**
The crystal system is commonly referred to as 'lattice' for periodic crystals and describes the shape of the repeating cell.
Examples include cubic, tetragonal, and monoclinic.
Calculations that simulate non-periodic systems, for example molecules, will be assigned as 'noncrystalline'.

**Number of sites in unit cell:**
The number of atoms in the unit cell of the calculation.
For supercell calculations, this quantity refers to the number of atoms in the full supercell.

**Cell volume:**
The volume, in cubic Angstroms, of the unit cell of the calculation.
For supercell calculations, this quantity refers to the volume of the full supercell.

**Density:**
The calculated bulk crystalline density, in grams/cc.

**Material id:**
This number is used to uniquely identify a material in the database.

## Chemistry

**Oxidation state:**
The degree of oxidation of the element in the material for ionic compounds.

**Coordination number:**
The number of atoms to which the element in the material is bound.

**Ordered only:**
Refers to whether the initial crystal data was obtained explicitly from experimental data (true) or required converting fractional occupancies into integer occupancies though an ordering algorithm (false).

## Energetics

**Formation energy:**
Computed formation energy at 0K, 0atm using a reference state of zero for the pure elements.
This quantity is often a good approximation for formation _enthalpy_ at ambient conditions.

**Energy above hull:**
The energy of decomposition of this material into the set of most stable materials at this chemical composition, in eV/atom.
Stability is tested against all potential chemical combinations that result in the material's composition.
For example, a $\ce{Co2O3}$ structure would be tested for decomposition against other $\ce{Co2O3}$ structures, against $\ce{Co}$ and $\ce{O2}$ mixtures, and against $\ce{CoO}$ and $\ce{O2}$ mixtures.

A positive E above hull indicates that this material is unstable with respect to decomposition.
A zero E above hull indicates that this is the most stable material at its composition.

## Mechanics

**Elastic Tensor:**
The elastic tensor $C$ describes the response of a crystalline material to mechanical stress.
Specifically, it relates the stress tensor $S$ to the strain tensor $E$.

**Bulk, Shear, and Young's Moduli:**
The bulk modulus $K$ describes the response of a material to compression.
The shear modulus $G$ describes the response of a material to shear stress.
Young's modulus $E$ relates uniaxial strain to stress in the same direction.
All three are scalars with units of pressure.

For isotropic materials, these three moduli fully describe the linear elastic reponse, and are related to each other by the Poisson ratio $\nu$: $2G(1+\nu)=E=3K(1-2\nu)$.
For anisotropic materials (most crystals), the full elastic tensor $C$ is required because the stress-strain ratio is dependent on the direction of the stress and strain.

**Poisson Ratio:**
The Poisson ratio $\nu$ is the negative of the ratio of tranvserse strain to axial strain under uniaxial stress.

**Voigt-Reuss-Hill Average Bulk and Shear Moduli:**
The Voigt-Reuss-Hill (VRH) moduli describe a polycrystalline material's approximate average responses to stress.
See the [Elasticity calculations](/methodology/elasticity) page for details on how these moduli are constructed.

## Data Science and Machine/Statistical Learning

**Cross validation**:
Cross validation is a method for testing the accuracy of a machine learning model by setting aside part of the available data as a validation set, training the model on the remaining data, and comparing the predicted values for the validation set to the known values.
[Cross Validation Wikipedia article](<https://en.wikipedia.org/wiki/Cross-validation_(statistics)>)

**Gradient Boosting**:
Gradient boosting is a machine learning method in which weak learner models are repeatedly fit to the residual (errors) of the existing model in order to improve it.
[Gradient Boosting Wikipedia article](https://en.wikipedia.org/wiki/Gradient_boosting)

**Local Polynomial Regression**:
In local polynomial regression, polynomial curves are fit to subsets of the data in proximity to specific points.
Predictions are made by combining these curves weighted by how close the test sample is to each local regression's center.
[Local Regression Wikipedia article](https://en.wikipedia.org/wiki/Local_regression)

## Authors

- Handong Ling
- Oxana Andriuc
