# Reaction Calculator
Welcome to the Reaction Calculator wiki!  
  
You will find in here all relevant information regarding the Reaction Calculator, including release notes, the manual, etc.
## Release Notes

Version 0.3 - May 13, 2011
  * Ability to select a particular crystal structure for the reaction via structureid

Version 0.2 - Mar 31, 2011 
  * Ability to select between three different energy adjustment strategies via a slider

Version 0.1 - Mar 6, 2011 
  * Initial release
  
## Manual
### Overview
The reaction calculator allows users to estimate tens of thousands solid-state reaction enthalpies from a database of density functional theory calculations. In addition, the reaction calculator reports known experimental enthalpies (at 298K and 1atm) where available.

The reaction calculator's energies are generally a good estimate of room temperature formation enthalpies, although all calculations are performed at 0 K and 0 atm. More information regarding methods to perform the calculations and their accuracy can be found in the Calculations Manual.

### Using the Reaction Calculator
To use the reaction calculator, the **reactants input** and **products input** fields must be completed. Other fields are optional. Multiple **advanced arguments** may be specified by comma-separating each argument.

#### Specifying Reactants and Products
Reactants and Products are specified via chemical formula in the free-form text fields. Chemical formulas must be "+"-separated. The coefficients of all compounds are automatically determined; there is no need for the user to balance the reaction.

For each chemical formula, our database automatically selects the lowest energy compound at the specified composition (handling of gaseous and liquid elements is explained in the Calculations Manual). The crystal structure used for a particular reaction calculation may be examined by clicking the blue links in the reaction output.

There are several ways of specifying the chemical formula (examples follow). In all cases, element names should have only the first letter capitalized.

  * **Reactants** - enter in this field a '+'-separated list of chemical formulas for the desired reactants.
    1. Usage example: $\ce{Li + O + P + Fe}$
    2. Usage example: $\ce{Li2O + Fe2O3 + P2O5 + O}$
    3. Usage example: $\ce{LiFePO4}$
  * **Products** - enter in this field a '+'-separated list of chemical formulas for the desired products (same format as 'Reactants')
  
The reaction energy will always be normalized for the reaction shown in the output.

#### Choosing a particular phase / crystal structure
This feature will be supported in a future release of the reaction calculator.

#### Reading the output
The reaction calculator balances the reaction and displays the balanced reaction as the first line in the output. The next line gives the computed reaction energy.

When a computational energy is available, the computed ΔH of reaction indicates the overall reaction energy of the reaction as written in the first line of the output. The ΔHf for each compound in the reaction lists formation energies from the elements. Clicking the compound displays its crystal structure.

When an experimental energy is available, the computed ΔH of reaction indicates the overall reaction enthalpy of the reaction as written in the first line of the output. The ΔHf for each compound in the reaction lists formation enthalpies from the elements. Sub-headings indicate the source(s) of experimental information.

When both computational and experimental data are available, a graphical chart displays the error for each compound in the calculation.

### Calculation Details / Estimating Errors
The Calculations Manual provides details on our calculation methodology and provides information on the magnitude of errors that may be expected.

### Citation
To cite the reaction calculator, please reference the following works:

  * A. Jain, G. Hautier, C. Moore, S.P. Ong, C.C. Fischer, T. Mueller, K.A. Persson, G. Ceder., A High-Throughput Infrastructure for Density Functional Theory Calculations, accepted for publication, Computational Materials Science. (2011).
  * A. Jain, G. Hautier, S.P. Ong, C. Moore, C.C. Fischer, K.A. Persson, G. Ceder, Accurate Formation Enthalpies by Mixing GGA and GGA+U calculations, (to be submitted).

### Authors
  1. Anubhav Jain
  2. Shyue Ping Ong
  3. Charles Moore
