# Structure Predictor App

Welcome to the Structure Predictor App wiki!

You will find in here all relevant information regarding the Structure Predictor App, including release notes, the manual, etc.

## Release Notes

### Recent changes

## Manual

### Background on Data Mined Crystal Structure and Compound Prediction

Crystal structure and compound prediction is an essential step of computational materials
design. Indeed, while many materials properties can be computed nowadays with *ab initio*
computations. Those computed properties are only relevant if they are evaluated on a compound (i.e., a
stoichiometry and crystal structure) stable enough to be formed. Crystal structure prediction can be quite useful
for experimentalists too. For instance, when only powder XRD experiments are available after synthesis of a new compound, a theoretical suggestion of a likely structure can tremendously help the structure determination through refinement for example.

The most common approach in the field of crystal structure prediction is to treat it as an optimization problem. [^1]
Researchers use optimization algorithms to search for the minimum of the relevant thermodynamic potential (e.g., the energy at 0 K, 0 atm) by varying the crystal's degrees of freedom (lattice constants, atomic positions). This optimization is extremely challenging as the energy landscape is very rugged and full of local minima. Very computationally expensive advanced optimization techniques (e.g., simulated annealing and genetic algorithm) are usually necessary to tackle this optimization problem. 

In a departure to this traditional approach, the methods we have developed use a combination of data mining and *a initio* computations in the density functional theory (DFT) framework to tackle this problem with a limited computational budget. The basic idea is to learn the chemical rules governing phase stability from a database of experimentally known compounds. Embedding those rules in a mathematical model, we can predict what are the most likely compounds to form in a given chemical system. Finally, a last step consists in testing those candidates for stability using ab initio computations (see link to manual thermo).


### The Ionic Substitution based Structure Prediction Method

The compound prediction model available on the web site now through the structure predictor app is based on our recent work on the data mining of ionic substitutions. In this section we will briefly explain the idea of the approach and how to use the web site. More details can be found in Hautier et al.[^2]

### The basic idea

[[image:Subst_ex.png|thumb|right|300px|Figure 1: An example of ionic substitution]]

It is common for chemists to propose new compounds from the substitution of
another, chemically similar, ion. For instance, as illustrated in Figure 1, knowing that BaTiO<sub>3</sub> forms a perovskite structure,
one can deduct that it is likely for another chemically similar ion as Ca<sup>2+</sup> to form the same structure. We have
implemented a mathematical model that learns these substitution rules from a database of experimentally
observed crystal structure (e.g., the ICSD). Basically, what the model provides is a probability
distribution for any ionic substitution. In Figure 2 we show the matrix indicating the date mined
substitution tendency for two ionic species obtained from this work. The ions have been sorted by Mendeleev number and therefore groups of chemically similar ions (e.g., the transition metals) are grouped together. Red colors indicate that two ions
tend to substitute while blue is associated with pair of species not substituting to each other.

[[image:Ions_correl_60_best_23_Jul_an_2.png|thumb|right|300px|Figure 2: Data mined tendency for ionic substitutions. Red indicates high substitution tendency. Blue indicates that the tow ions tend to not substitute]]

### The compound prediction procedure

The product of our data mining approach is a probability function indicating how likely is a specific set of ionic substitutions. The model we used was inspired by previous work in the field of machine translation. In this field, it is the probability for a word in one language to be able to be substituted by a word in another language that is sought for. In our case, the words are replaced by ions.
After we built this probability function from a database of experimental data (here the ICSD), we can perform compound predictions. Figure 3 illustrates the procedure for 4 ions (but this can be generalized to any number of species). Targeting a specific combinations of 4 ions (e.g., Ba<sup>2+</sup>, Fe<sup>3+</sup>, La<sup>3+</sup>, O<sup>2-</sup> ), we look for any substitution from known compounds (in the ICSD) that have a high enough probability to be likely to form a new stable compound. If the substitution is higher than a certain threshold we keep it as a possible candidate, otherwise we disregard it and go to the next ICSD compound. There is also a step making sure we do not form duplicate structures and we only form charge balanced compounds.

[[image:Substitution_flow_chart2.png|thumb|right|300px|Figure 3: Procedure for proposing new compound candidates in a quaternary system using the ionic substitution probability]]

From this procedure, we can see that the threshold to set is quite important. A higher threshold will give you less false positives (suggested compounds that are not stable) but also less true positives. On the other hand, a too low threshold will give you more false positives but also more true positives. There is a compromise to find between how exhaustive you want to be and how many candidates you can have in terms of computational budget (that you will have to test down the road for stability using DFT).

### Performance and Limitations

### Using the Structure Predictor

#### Entering Inputs

Practically, the procedure for getting predictions consists in 3 steps

1. Pick elements: choose in the periodic table what element constitute the chemical space you are interested in. For instance if you want to make predictions for battery materials based on Li, Mn and O, you should pick those three elements.

2. Pick oxidation states: the model use the oxidation states to make predictions. V<sup>3+</sup> does not substitute with the same elements than V<sup>5+</sup>. So, if you want to study Mn<sup>3+</sup> compounds you pick +3 for Mn, +1 for Li (no other choices anyway) and O<sup>2-</sup>. Sometimes you do not know what oxidation states you are interest in. Let say you want all Li-Mn-O compounds regardless of the oxidation state of Mn. Then, I would suggest running the model several times, one for Mn<sup>2+</sup>, one for Mn<sup>3+</sup>, one for Mn<sup>4+</sup>. This should cover all the chemical space you are looking at.

3. Pick a threshold. Be careful, the threshold depends on the number of species in your model. The probability model are actually not the same depending on the number of species they have (even though they are built on common building blocks). We suggest to use: -3 for binaries, -4 for ternaries and -5 for quaternaries. Of course, if you want less candidates you should reduce those numbers but those are pretty standard values that should work in most cases.

4. type your e-mail and click results. An e-mail will be sent to you with the results of the prediction. We provide a log file indicating the ionic substitutions, their probability and from which ICSD entry. We also provide cif files for the predicted compounds as well as VASP files ready to be run with standard parameters. We do not provide any DFT results due our limited computational budget for the moment. It is the responsibility of the user to run the predictions. Also, as the pseudopotentials are proprietary in VASP (POTCARs) we do not provide those but a script is sent along that can be run to make sure the POTCARs are built from a directory containing all pseudopotentials.

#### Interpreting the Results

The results are given as a set of cifs or VASP runs. These are '''only''' candidate structures. Typically, those candidates need to be tested for stability against each other (seeing what is the lowest energy structure amongst the candidates at a given composition) but also against other phases known in nature. For instance, if a AB compound is proposed and its energy is higher than a combination of half A<sub>2</sub>B and half AB<sub>2</sub>. This stability analysis can be performed using the convex hull construction that will effectively test the stability of the phases against each other and come with a set of stable phases that are on the hull. Figure 4 shows a convex hull (in green) for an A-B system.Blue points indicate phases that are not on the hull and therefore unstable and red points indicate stable phases. For instance, the construction shows directly that the phase γ at AB will decompose into α<sub>1</sub> and β<sub>2</sub>.

[[image:Convexhull.png|thumb|right|300px|Figure 1: An example of the convex hull construction]]


More information about phase stability and convex hull can be obtained in the phase diagram app manual [https://materials.nersc.gov/wiki/index.php/Phase_Diagram_App_Manual].

Please note that we only presented an approach for building zero K, zero pressure phase diagrams. It is possible to use the candidates proposed by the model to perform more advanced stability studies for instance at finite temperature. This is more expensive computationally though as the different entropy components (configuration, vibration, etc...) need to be taken into account.

Finally, as we present an usage of our candidates for computations, an experimentalist can also use these candidates to test different structures versus a powder diffraction pattern.

### Future features

In the future, we want to give the user the option to perform substitution of several ions for one ion in a starting structure. For instance, if one is interested in ternary oxychlorides (M, O<sup>2-</sup>, Cl<sup>1-</sup>) there will be only few ternary compounds that will be good candidates for a substitution generating oxychlorides (e.g., oxybromides). A strategy to increase the pool of possible structure is to allow substitution of one ion by O<sup>2-</sup> and Cl<sup>-</sup>. For instance, we would start with an oxide and substitute the O<sup>2-</sup> by a mixture of O<sup>2-</sup> and Cl<sup>-</sup>. The amount of O and Cl will be set to achieve charge balance and a simple model (electrostatics or other) could be used to pick an ordering of the two substituted species.

The only data mined model accessible now is the substitution predictor. We have developed another model based on correlations between crystal structures at different compositions.[^3,4] We plan to give access to this model in the future. The two models are complimentary: the model based on correlations between structure is more efficient in data rich regions (e.g., ternary oxides) while the ionic substitution model is more efficient in data sparse regions (e.g., quaternaries).

### Citation

To cite the Structure Predictor App, please reference the following works:

- G. Hautier, V. Ehrlacher, C.C. Fischer, A. Jain, G. Ceder, Data Mined Ionic Substitutions for the Discovery of New Compounds, Inorganic Chemistry, vol. 50, 2011, pp. 656-663.
- A. Jain, G. Hautier, C. J. Moore, S. P. Ong, C. C. Fischer, T. Mueller, K. A. Persson, and G. Ceder, A high-throughput infrastructure for density functional theory calculations, Computational Materials Science, vol. 50, 2011, pp. 2295-2310.

### References

[^1]: 10.1038/nmat2321
[^2]: 10.1021/ic102031h
[^3]: 10.1021/cm100795d
[^4]: 10.1038/nmat1691

### Authors

- Geoffroy Hautier
- Anubhav Jain
