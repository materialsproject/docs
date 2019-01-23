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

One concern for cathode design is resistance to O2 release, as O2 release from the cathode can lead to thermal runaway. The O2 evolution diagram determines the equilibrium chemical potentials at which O2 release can be expected, and the amount of O2 released[1][2]. One way to read this chart is to look at the chemical potential at which O2 release begins (the first x-value for which the y-axis is greater than zero). Compounds for which O2 release begins at more negative muO2 are more stable with respect to O2 release. Note that the O2 release chart is specific to one lithiation level of the set of compounds forming the cathode system. There is a drop-down that allows you to choose the lithiation level (e.g. fully delithiated, fully lithiated). The muO2 needed for release can be referenced against common binary systems to get an idea of stability to O2 release: 

### Overall materials properties
### Voltage pair properties
## Diffusion data
## Bond valence difffusion pathway information
## Classical bond valence method
## Bond valence site energy calculation
## Limitations of the approach
## Global instability index (GII)
## References
## Authors
