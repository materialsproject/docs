# Target Solubility Tool

## Overview

Redox flow batteries (RFBs) provide a promising pathway towards low-cost grid-scale
energy storage devices. The economic viability of non-aqueous and aqueous redox flow 
batteries (NAqRFBs and AqRFBs respectively) is highly dependent on electroactive
materials, salt, and solvent choices.[^1] The interactive *RFB Dashboard* can be used to 
select redox active materials for use in nonaqueous and aqueous RFBs by displaying 
individual materials along with regions of economic viability defined by the target battery 
price and minimum redox active species concentration.[^2] In addition, the tool provides 
concentration targets for redox active materials achieving the target battery price. This 
tool can be used to analyze both experimentally demonstrated materials and simulated 
families of materials. Reference 2 describes the techno-economic model implemented in 
the present tool. The default values of all input parameters are assumed to be the median 
values presented in Ref. 1.

## Redox Active Material Design Space

Redox active materials are defined using three electrochemical properties: 
molecular weight (g/mol e-), redox potential (V vs. Li/Li+), and active material
concentration (mol actives/kg electrolyte). The molecular weight is defined as
the molecular weight of redox active material normalized by the number of 
electrons transferred. The redox potential is defined as the average potential 
of electron transfer events that the material undergoes.

The molecular weight and redox potential of a redox active molecule
can be measured or simulated in less time and with more accuracy than
active material solubility. Thus, the *RFB Dashboard* shows redox active
materials on a two-dimensional materials-selection map, with axes of
molecular weight and redox potential, while drawing concentration contours
that achieves the target battery price. In the model each material is 
assumed to pair with a hypothetical counter-electrode material having 
a different potential than the material of interest, but common concentration and molecular weight.

## Using the RFB Dashboard

### Importing Data for Analysis

#### Via CSV

Data can be imported into the tool via a Comma Separated Values (CSV) file. 
The CSV file should be formatted in such a way that there is a header for the 
first row of the data sheet and the order of the data columns does not matter. 
However, the header names for each column has to have 'formula' for molecular 
formula, 'ew' for equivalent weight, 'redpot' for reduction potential and 'oxpot' 
for oxidation potential. Once your CSV file is ready, it can be uploaded into the 
tool by clicking on the "via CSV" button on top of the tool to upload the file 
and the data will then be displayed on the tool.

*This should be updated with "ew" changed to "mw"* (TODO EDIT)

#### Via Molecular Explorer

Data can also be imported into the tool via Molecule Explorer. By clicking on the 
"via Molecule Explorer" button on top of the RFB Dashboard, the Molecule Explorer 
would appear and materials with desired structures can be selected. Once the molecules 
data set are selected, click on the "Explore Solubility" button to import them into 
the RFB Dashboard for further analysis. For a visual tutorial on how to import data 
via Molecule Explorer, a [short video](https://www.youtube.com/watch?v=w5NHcwujX30)
is available to demonstrate how the Molecule Explorer is used.

## Description of Input Parameters

### Target Battery Price

The maximum battery price for RFBs built using the redox active materials enclosed by 
the concentration contours. The battery price is a combination of reactor cost, electrolyte
cost, balance-of-plant and addition-to-price costs. Battery price neglects the cost of 
power-conditioning equipment that is included in system price defined in Ref. 1. As a 
result, when calculating battery price balance-of-plant costs are reduced by $100/kW 
compared to that in Ref. 1 used to calculate system price. ($/kWh)

### Target Molality

The minimum concentration achieving the target battery price for redox active materials 
enclosed by the concentration contours. The molality is defined as a ratio of moles of 
redox active species to kilograms of solvent in mol/kg.

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
* Discharge Voltage Efficiency: ratio of cell potential during cycling to 
the thermodynamically reversible open-circuit cell potential (-)
* Round-trip Coulombic Efficiency: ratio of charge released during discharging 
cycle to charge stored during charging cycle (-)
* Discharge System Efficiency: accounts for auxiliary equipment losses during discharge (-)

### Electrochemical Parameters

* Area-Specific Resistance: accounts for ohmic, kinetic, and transport losses in 
the separator, electrodes, and electrolyte ($\Ohm$-cm2)
* Stability Limits: solvent window of stability beyond which breakdown occurs (V vs. Li/Li+)
* Hypothetical Counter-Electrode Potential: Assumed hypothetical counter-electrode 
for full-cell analysis of single electrode materials. (V vs. Li/Li+)

## References

[^1] R. M. Darling, K. G. Gallagher, J. A. Kowalski, S. Ha, and F. R. Brushett, 
Energy Environ. Sci., 7, 3459-3477 (2014). [DOI:10.1039/C4EE02158D](https://doi.org/10.1039/C4EE02158D)

[^2] R. Dmello, J. D. Milshtein, F. R. Brushett, and K. C. Smith, In Review (2016). <https://doi.org/10.1016/j.jpowsour.2016.08.129>

## Authors

* MP Team
* Kyle Bystrom
