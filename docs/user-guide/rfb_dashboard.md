# RFB Dashboard
## Overview
Redox flow batteries (RFBs) provide a promising pathway towards low-cost grid-scale energy storage devices. The economic viability of non-aqueous and aqueous redox flow batteries (NAqRFBs and AqRFBs respectively) is highly dependent on electroactive materials, salt, and solvent choices.[^1](#references) The interactive RFB Dashboard can be used to select redox active materials for use in nonaqueous and aqueous RFBs by displaying individual materials along with regions of economic viability defined by the target battery price and minimum redox active species concentration.[[2]](#references) In addition, the tool provides concentration targets for redox active materials achieving the target battery price. This tool can be used to analyze both experimentally demonstrated materials and simulated families of materials. Reference 2 describes the techno-economic model implemented in the present tool. The default values of all input parameters are assumed to be the median values presented in Ref. 1.

## Redox Active Material Design Space
Redox active materials are defined using three electrochemical properties: molecular weight (g/mol e-), redox potential (V vs. Li/Li+), and active material concentration (mol actives/kg solvent). The molecular weight is defined as the molecular weight of redox active material normalized by the number of electrons transferred. The redox potential is defined as the average potential of electron transfer events that the material undergoes.

The molecular weight and redox potential of a redox active molecule can be measured or simulated in less time and with more accuracy than active material solubility. Thus, the RFB Dashboard shows redox active materials on a two-dimensional materials-selection map, with axes of molecular weight and redox potential, while drawing concentration contours that achieves the target battery price. In the model each material is assumed to pair with a hypothetical counter-electrode material having a different potential than the material of interest, but common concentration and molecular weight.

## Using the RFB Dashboard
### Importing Data for Analysis
#### Via Molecule Explorer
Data can be imported into the tool via Molecule Explorer. By clicking on the "via Molecule Explorer" button on top of the RFB Dashboard, the Molecule Explorer would appear and materials with desired structures can be selected. Once a set of molecules is selected, click on the "Explore Solubility" button to import them into the RFB Dashboard for further analysis. For a visual tutorial on how to import data via Molecule Explorer, a [short video](https://www.youtube.com/watch?v=w5NHcwujX30) is available to demonstrate how the Molecule Explorer is used.

#### Via CSV
Data can be imported into the tool via a Comma Separated Values (CSV) file. The CSV file should be formatted in such a way that there is a header for the first row of the data sheet and the order of the data columns does not matter. However, the header names for each column has to have 'formula' for molecular formula, 'mw' for molecular weight, 'redpot' for reduction potential and 'oxpot' for oxidation potential. Once your CSV file is ready, it can be uploaded into the tool by clicking on the "via CSV" button on top of the tool to upload the file, and the data will then be displayed on the tool.

## Description of Input Parameters
### Target Battery Price
The Target Battery Price is the maximum battery price for RFBs built using the redox active materials enclosed by the concentration contours. The battery price is a combination of reactor cost, electrolyte cost, balance-of-plant and addition-to-price costs. Battery price neglects the cost of power-conditioning equipment that is included in system price defined in Ref. 1. As a result, when calculating battery price balance-of-plant costs are reduced by $100/kW compared to that in Ref. 1 used to calculate system price. ($/kWh)

### Target Molality
The Target Molality is the minimum concentration achieving the target battery price for redox active materials enclosed by the concentration contours. The molality is defined as a ratio of moles of redox active species to kilograms of solvent in mol/kg.

### Cost Parameters
* Reactor Cost Per Unit Area ($/m2)
* Salt Cost: cost per unit mass of supporting salt ($/kg)
* Solvent Cost: cost per unit mass of solvent ($/kg)
* Active Material Cost: cost per unit mass of active material ($/kg)
* Additional Contribution to Price: accounts for depreciation, labor, overhead, and margin ($/kW)
* Balance of Plant Cost: accounts for ancillary equipment costs ($/kW)

### Operating Conditions
* System Discharge Time: battery discharge time (hours)
* Depth of Discharge: allowable range of state-of-charge (-)
* Discharge Voltage Efficiency: ratio of cell potential during cycling to the thermodynamically reversible open-circuit cell potential (-)
* Round-trip Coulombic Efficiency: ratio of the charge released during the discharging step of a complete cycle relative to the charge stored during the charging step of a complete cycle. (-)
* Discharge System Efficiency: accounts for losses in energy during discharge due to auxiliary equipment. (-)

### Electrochemical Parameters
* Area-Specific Resistance: accounts for ohmic, kinetic, and mass-transfer resistance in the separator, electrodes, and electrolyte (Ω-cm2)
* Stability Limits (Nonaqueous only): solvent window of stability beyond which breakdown occurs (V vs. Li/Li+)
* Hypothetical Counter-Electrode Potential (Nonaqueous only): assumed hypothetical counter-electrode for full-cell analysis of single electrode materials. (V vs. Li/Li+)
* pH (Aqueous only): sets the pH of the aqueous solution. Aqueous stability limits are determined by the oxygen and hydrogen evolution potentials, which depend on the pH of the solution. The hypothetical counter-electrode potentials are selected in order to be within the stability limits within a margin of the "Voltage Offset" parameter. (-)
* Voltage Offset (Aqueous only): Hypothetical counter-electrodes, with which each molecule of interest is paired, are specified by an increment in voltage, called the Voltage Offset. For positive-electrode molecules of interest the potential of the counter-electrode exceeds the hydrogen evolution potential by the magnitude of the Voltage Offset, and for negative-electrode molecules of interest the potential of the counter-electrode is set below the oxygen evolution potential by the magnitude of the Voltage Offset. (V)

## References
 [^1]: 10.1039/c4ee02158d 
 [^2]: 10.1016/j.jpowsour.2016.08.129
