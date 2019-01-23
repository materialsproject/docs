# Glossary of Terms

## Materials Explorer

## Formula
<b> Anonymous chemical formula The chemical formula </b> with the element names anonymized to the letters A, B, C, etc. The order of the anonymized elements is from least atomic fraction to greatest atomic fraction, thus the coefficients are non-decreasing. For example, both TiO<sub>2</sub> and Na<sub>2</sub>O have an anonymous formula of A<sub>1</sub>B<sub>2</sub>.

## Structure
<b> Crystal system </b> The crystal system is commonly referred to as 'lattice' for periodic crystals and describes the shape of the repeating cell. Examples include cubic, tetragonal, and monoclinic. Calculations that simulate non-periodic systems, for example molecules, will be assigned as 'noncrystalline'.

<b> Number of sites in unit cell</b> The number of atoms in the unit cell of the calculation. For supercell calculations, this quantity refers to the number of atoms in the full supercell.

<b> Cell volume </b>The volume, in cubic Angstroms, of the unit cell of the calculation. For supercell calculations, this quantity refers to the volume of the full supercell.

<b> Density </b>The calculated bulk crystalline density, in grams/cc.

<b> Material id:</b> This number is used to uniquely identify a material in the database.

## Chemistry
<b>Oxidation state:</b> The degree of oxidation of the element in the material for ionic compounds.

<b>Coordination number:</b> The number of atoms to which the element in the material is bound.

<b>Ordered only:</b> Refers to whether the initial crystal data was obtained explicitly from experimental data (true) or required converting fractional occupancies into integer occupancies though an ordering algorithm (false).

## Energetics
<b>Formation energy:</b> Computed formation energy at 0K, 0atm using a reference state of zero for the pure elements. This quantity is often a good approximation for formation <i>enthalpy</i> at ambient conditions.

<b>Energy above hull:</b> The energy of decomposition of this material into the set of most stable materials at this chemical composition, in eV/atom. Stability is tested against all potential chemical combinations that result in the material's composition. For example, a Co<sub>2</sub>O<sub>3</sub> structure would be tested for decomposition against other Co<sub>2</sub>O<sub>3</sub> structures, against Co and O<sub>2</sub> mixtures, and against CoO and O<sub>2</sub> mixtures.

A positive E above hull indicates that this material is unstable with respect to decomposition. A zero E above hull indicates that this is the most stable material at its composition.
