# High-pressure phase detection manual
So far, all computations in the materials project database have been ran assuming 0 pressure. However, sometimes 
experimental data refers to high-pressure phases. While the ICSD web site tags high-pressure phases, we could not 
technically retrieved this data. To detect high-pressure phase, we had instead to rely on an imperfect word detection 
in the journal title of the entry. Any entry with a journal title containing G[Pp]a, [kM]bar or [Pp]ressure will be 
considered as likely high-pressure phase and will be tagged with a warning accordingly.

## Authors
1. Geoffroy Hautier
2. Jordan Burns

# Unusual oxidation state detection manual
Unusual oxidation states (e.g., +2 for Al) can be the indication of a problem with the experiment or lead to large errors 
in computations (e.g., when an oxidation state requires electrons in the core of the pseudopotential to participate in 
bonding).

To tag the entries with less common oxidation states and warn the user about them, we performed statistics on all the 
unique entries in the ICSD. From this statistical analysis, we estimated the probability p(n|A) where n is an oxidation 
state and A is an element. For instance, we p(+2|Al) will be very low, as it is very rare to observe Al in a +2 state.

We decided to tag any entry with oxidation states according to the ICSD with a probability lower than 10%. Please note that 
this affect only compounds with assigned oxidation states in the ICSD.

## Authors
1. Geoffroy Hautier
2. Jordan Burns

# Volume Change Error manual
We have used the difference between the computed volume after DFT relaxation and the volume reported experimentally as an 
indicator of a problem with a computation or entry. The problem can come from the experimental side (for instance atomic 
positions wrongly assigned in the ICSD) or from the approximation used in DFT.

Our analysis focused only on GGA (without U) results. Our strategy consist in first establishing a volume change distribution 
from our large data set. After establishing this distribution, outliers will be easily identified and tagged with a warning.

## Volume Change Distribution in GGA
Our analysis focused on the GGA data in the database available on Friday September 23, 2011. In total, we considered 
11579 entries. We report on volume changes by computing:
$$ \Delta V=\frac{V_{GGA}-V_{exp}}{V_{exp}} $$
Where $$ V_{GGA} $$ is the unit cell volume obtained by GGA and $$ V_{exp} $$ the experimental volume given by the ICSD

### The issue with high pressure phases
If the data is right away used, we would observe a longer tail on the positive values. This data is from the high pressure 
phase. Indeed, while our computations have been performed at 0 atm, compounds characterized at high-pressure will show a 
lower experimental than computed volume. This is not per se an error but instead a discrepancy between the experimental and 
computational conditions. To mitigate, this issue we removed from this analysis any entry likely to refer to a high-pressure 
phase according to the methodology presented in [^1]

### The fitting of the distribution
After exclusion of the possible high-pressure phases, we have 10768 points available to study the difference between
experimental and computed volume. Figure 1 shows the histogram of volume difference. The distribution is symmetric but
its median is positive (3.2%) indicating a tendency for GGA to overestimate the volume. This is in agreement with the
know-how in the field established from previous studies on smaller set of compounds.

We obtained a very good fit to the data by using the a t-location scale distribution.[^2] A normal distribution could not 
be fitted to this data because of the heavy tail observed. Using matlab and a maximum likelihood approach, we obtained 
maximum likelihood estimates as well as confidence intervals for the three parameters of the distribution. Figure 2 shows 
the good agreement between the raw data and the t-location scale probability density distribution.

### The tagging of the entries
After fitting the distribution, it is possible to tag the entries outlying the distribution. We assigned a warning tag to 
any entry in our database with a volume error higher than the 95th percentile (situated at 9.6% volume change) and lower 
than the 5th percentile (situated at -3,2% volume change). Figure 3 shows these boundaries on the cumulative t-location 
scale distribution.

In total, 959 entries have been assigned a warning.

### Some examples of outliers detected by the volume difference
Here, we analyze some of the largest outliers found in our analysis. Through these examples, we illustrate what kind of 
errors can be observed.

#### YZn and YbZn
Both compounds (task_id: 11577 and 179, icsd_id: 106232, 206226) show enormous volume differences: 370% and 350% ! Looking 
at the data present in the ICSD, we found that the paper reference mentioned CsCl structures, while the entry given by the 
ICSD is a fcc based alloy. The volume discrepancy comes therefore from an erroneous export of the experimental data in the 
paper to the ICSD.

#### Sn
55% volume difference task_id: 7162 and icsd_id: 52487. This entry refers to a high pressure structure our algorithm did
not catch. It is not surprising to see the computed data reporting a much larger volume than the experimental obtained at 
high-pressure

#### TaMn<sub>2</sub>O<sub>3</sub>
-27% volume difference task_id: 7521, icsd_id: 15995 The icsd indicates already that the experimental data is dubious. 
There is a warning on the ICSD web site: "Unusual difference between calculated and measured density". The oxidation state 
reported for Ta: +2 is extremely rare.

#### MoS2
18% volume difference task_id: 1434, icsd_id: 644257 This is most likely due to an inherent error from GGA. The MoS2 
structure is layered and van der Waals interactions between the S atoms are essential to the geometry of the structure 
(c lattice parameter especially). However, it is known that GGA does not model well VDW interactions.

## Citation
To cite the Materials Project, please reference the following work:
* A. Jain, G. Hautier, C. J. Moore, S. P. Ong, C. C. Fischer, T. Mueller, K. A. Persson, and G. Ceder, A high-throughput infrastructure for density functional theory calculations, Computational Materials Science, vol. 50, 2011, pp. 2295-2310.

## Authors
1. Geoffroy Hautier
2. Jordan Burns

# Bond length Change Error manual
