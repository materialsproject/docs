# Glossary of Terms

## Materials Explorer

## Formula
**Anonymous chemical formula:**
The chemical formula with the element names anonymized to the letters A, B, C, etc. The order of the anonymized elements is from least atomic fraction to greatest atomic fraction, thus the coefficients are non-decreasing. For example, both $\ce{TiO2}$ and $\ce{Na2O}$ have an anonymous formula of $\ce{A1B2}$.

## Structure
**Crystal system:**
The crystal system is commonly referred to as 'lattice' for periodic crystals and describes the shape of the repeating cell. Examples include cubic, tetragonal, and monoclinic. Calculations that simulate non-periodic systems, for example molecules, will be assigned as 'noncrystalline'.

**Number of sites in unit cell:**
The number of atoms in the unit cell of the calculation. For supercell calculations, this quantity refers to the number of atoms in the full supercell.

**Cell volume:**
The volume, in cubic Angstroms, of the unit cell of the calculation. For supercell calculations, this quantity refers to the volume of the full supercell.

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
Computed formation energy at 0K, 0atm using a reference state of zero for the pure elements. This quantity is often a good approximation for formation *enthalpy* at ambient conditions.

**Energy above hull:**
The energy of decomposition of this material into the set of most stable materials at this chemical composition, in eV/atom. Stability is tested against all potential chemical combinations that result in the material's composition. For example, a $\ce{Co2O3}$ structure would be tested for decomposition against other $\ce{Co2O3}$ structures, against $\ce{Co}$ and $\ce{O2}$ mixtures, and against $\ce{CoO}$ and $\ce{O2}$ mixtures.

A positive E above hull indicates that this material is unstable with respect to decomposition. A zero E above hull indicates that this is the most stable material at its composition.

## Authors
* Handong Ling
* Oxana Andriuc
