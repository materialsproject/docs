# Battery Explorer Manual

## Introduction

The Battery Explorer is a customized tool to search the Materials Project database for battery materials satisfying various critical criteria such as voltage, capacity, stability and energy density.

Currently, this app contains more than 4,000 intercalation compounds and 16,000 conversion compounds with different types of working ions (such as Li, Mg, Zn, Al and more). These numbers will increase as new compounds are continuously added to the database, including many new structural predictions.

## Searching Using the Battery Explorer

The battery explorer is designed to help battery scientists find electrode materials of interest. There are a number of search fields that can be used to filter all the battery material entries to customize the results returned. Every battery material entry compiles multiple material entries that represent a given battery electrode at different states of charge and the corresponding data analysis to predict useful battery properties such as voltage or change in volume.

The search bar above the periodic table in the battery explorer app can be used to search for battery material entries based on the composition (either by typying into the search bar or clicking on the periodic table to specify elements), by Material ID, or by Battery ID. In the toolbar to the right of the periodic table, there are a number of additional criteria that can be used to filter the results:

* Number of Elements (including the working ion)
* Excluded Elements
* Toggle select between Intercalation Compounds or Conversion Compounds
* Type of Working Ion 
* Average Voltage in V with respect to the voltage of the pure metal for the corresponding working ion
* Volumetric Capacity in Ah/L
* Gravimetric Capacity (also known as Specific Capacity) in (mAh/g)

At the bottom of the toolbar to the right of the periodic table, a number of advanced search options can be expanded:
* Max. Voltage Step in V
* Max. Volume Change in fractional units (for example 1 corresponds to 100% volume change)
* Max. Instability in eV/atom determined from the energy above hull metric (see glossary for more information)

## The Search Result Table
The search result table presents the resulting battery material entries from your search. You can add or hide fields from the result table by clicking the "Show/ hide columns" button and filter the results based on these fields by clicking the arrow in the column of interest. There are also buttons to print or export the Search Result Table to save your results for future reference.

## Viewing Details of a Battery Compound

To investigate an individual battery material entry, click on one of the rows in the Search Results Table. This will open a new page containing a detailed summary for that entry including links and additional information for each material entry associated with a given battery material entry and data analysis such as the predicted voltage profile, oxidative stability, volume change, etc.

Within a single battery material entry, each associated material entry is dedicated to one structural framework (e.g. $\ce{Mn2O4}$ spinel, $\ce{Li0.5Mn2O4}$ spinel, or $\ce{LiMn2O4}$ spinel) that represents a different state of charge or working ion intercalation level. These material entries have been grouped together into a single battery material entry using structural analysis of the structures with the working ion(s) removed.

The details view has many components including interactive plots:

### Voltage Curve

The voltage curve graph displays the calculated equilibrium voltage versus state of charge. If voltage criteria were specified in the query, the line might be segmented into different colors. The green portion of the curve matches the query, whereas the the blue portion of the curve does not.

Try hovering over points on the voltage curve plot with your mouse for more information on that data point.

### O<sub>2</sub> Evolution Curve

One concern for battery electrode design is resistance to $\ce{O_2}$ release, as $\ce{O_2}$ release from an electrode can lead to thermal runaway which is a safety hazard. The $\ce{O_2}$ evolution diagram determines the equilibrium chemical potentials at which $\ce{O_2}$ release can be expected, and the amount of $\ce{O_2}$ released[^1][^2]. 

One way to read this chart is to look at the chemical potential at which $\ce{O_2}$ release begins (the first x-value for which the y-axis is greater than zero). Compounds for which O2 release begins at more negative muO2 are more stable with respect to $\ce{O_2}$ release. The $\mu_\ce{O_2}$ needed for release can be referenced against established battery compounds to get an idea of stability to $\ce{O_2}$ release. This plot is interactive so you can hover over a data point with your mouse for more detailed information.

### Structure Viewer

For viewing convenience, there is a drop down list below the structure viewer window where you can select the structure of each material entries associated with a battery material entry.

### Overall Battery Material properties

The overall battery materials properties display aggregate or average properties derived from all states of charge (e.g. intercalation levels) for a given structural framework. Note that some intercalation levels presented in this section may be outside the desired range of voltage, stability, or safety. More details are given in the 'Voltage pair properties' section.

### Voltage Pair Properties

This table displays calculated data for each voltage step along the voltage profile. In each row, the two material entries associated with a single voltage step and the corresponding properties (volume change, capacity, voltage, etc.) are displayed. Click on the composition of one of the materials listed to be directed to that material entry.

## Authors
1. Shyue Ping Ong
2. Anubhav Jain
3. Stefan Adams (diffusion data)
4. Eric Sivonxay
5. Jimmy Shen
6. Ann Rutt

## References
[^1]: S. P. Ong, L. Wang, B. Kang, G. Ceder., The Li-Fe-P-O2 Phase Diagram from First Principles Calculations, Chemistry of Materials, vol. 20, Mar. 2008, pp. 1798-1807. [doi:10.1021/cm702327g](https://doi.org/10.1021/cm702327g)  
[^2]: S.P. Ong, A. Jain, G. Hautier, B. Kang, and G. Ceder, Thermal stabilities of delithiated olivine MPO4 (M=Fe, Mn) cathodes investigated using first principles calculations, Electrochemistry Communications, vol. 12, 2010, pp. 427-430. [doi:10.1016/j.elecom.2010.01.010](https://doi.org/10.1016/j.elecom.2010.01.010)  
[^3]: S. Adams, Solid State Ionics 177, 1625 (2006).  
[^4]: S. Adams, Acta Crystallogr. B, Struct. Sci. 57, 278 (2001).  
[^5]: S. Adams and R. Prasada Rao, Phys. Chem. Chem. Phys. 11, 3210 (2009).  
[^6]: S. Adams and R. P. Rao: High power Li ion battery materials by computational design; Phys. Status Solidi A 208, 1746–1753 (2011). [doi:10.1002/pssa.201001116](https://doi.org/10.1002/pssa.201001116)  
