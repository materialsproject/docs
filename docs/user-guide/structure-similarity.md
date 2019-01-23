# Structure similarity
## Introduction
The similarity between two structures <i>i</i> and <i>j</i> is assessed on the basis of local coordination information from all sites in the two structures. [^1] [^2] The four basic steps involved are:

1. Find near(est) neighbors of all sites in both structures.
2. Evaluate each coordination pattern via coordination descriptors observed at each site to define site fingerprints.
3. Compute statistics of the descriptor values across all sites in a structure to define structure fingerprints.
4. Use structure fingerprints to rate the (dis)similarity between the two (vectors representing the two) structures.

## Near-neighbor finding
We use a novel method called CrystallNN to find near(est) neighbors in periodic structures. While the method will be introduced shortly[^3], it is already available through the python package [pymatgen](https://github.com/materialsproject/pymatgen).

## Site Fingerprints
The second step of the structure similarity calculation is the computation of a crystal site fingerprint, <b>v</b><sup>site</sup>, for each site in the two structures. The fingerprint is a 61-dimensional vector in which each element carries information about the local coordination environment computed with the <i>site</i> module of the python package [matminer](https://github.com/hackingmaterials/matminer). For example, the first two elements "wt CN<sub>1</sub>" and "single bond CN<sub>1</sub>" provide estimates of the likelihood (or weight) of how much the given site should be considered 1-fold coordinated (i.e., <i>w</i>|<sub>CN=1</sub>). The third element "wt CN<sub>2</sub>" provides a 2-fold coordination likelihood, whereas the fourth element "L-shaped CN<sub>2</sub>" holds the resemblance similarity to an L-shaped coordination geometry (also called local structure order parameter) given that we find a coordination configuration with 2 atoms (<i>q</i><sub>L</sub>|<sub>CN=2</sub>). The local structure order parameters can assume values between 0, meaning that the observed local environment has no resemblance with the target motif to which it is compared, and 1, which stands for perfect motif match. The remaining elements are: "water-like CN<sub>2</sub>," "bent 120 degrees CN<sub>2</sub>," "bent 150 degrees CN<sub>2</sub>," "linear CN<sub>2</sub>," "wt CN<sub>3</sub>," "trigonal planar CN<sub>3</sub>," "trigonal non-coplanar CN<sub>3</sub>," "T-shaped CN<sub>3</sub>," "wt CN<sub>4</sub>," "square co-planar CN<sub>4</sub>," "tetrahedral CN<sub>4</sub>," "rectangular see-saw-like CN<sub>4</sub>," "see-saw-like CN<sub>4</sub>," "trigonal pyramidal CN<sub>4</sub>," "wt CN<sub>5</sub>," "pentagonal planar CN<sub>5</sub>," "square pyramidal CN<sub>5</sub>," "trigonal bipyramidal CN<sub>5</sub>," "wt CN<sub>6</sub>," "hexagonal planar CN<sub>6</sub>," "octahedral CN<sub>6</sub>," "pentagonal pyramidal CN<sub>6</sub>," "wt CN<sub>7</sub>," "hexagonal pyramidal CN<sub>7</sub>," "pentagonal bipyramidal CN<sub>7</sub>," "wt CN<sub>8</sub>," "body-centered cubic CN<sub>8</sub>," "hexagonal bipyramidal CN<sub>8</sub>," "wt CN<sub>9</sub>," "q2 CN<sub>9</sub>," "q4 CN<sub>9</sub>," "q6 CN<sub>9</sub>," "wt CN<sub>10</sub>," "q2 CN<sub>10</sub>," "q4 CN<sub>10</sub>," "q6 CN<sub>10</sub>," "wt CN<sub>11</sub>," "q2 CN<sub>11</sub>," "q4 CN<sub>11</sub>," "q6 CN<sub>11</sub>," "wt CN<sub>12</sub>," "cuboctahedral CN<sub>12</sub>," "q2 CN<sub>12</sub>," "q4 CN<sub>12</sub>," "q6 CN<sub>12</sub>," "wt CN<sub>13</sub>," "wt CN<sub>14</sub>," "wt CN<sub>15</sub>," "wt CN<sub>16</sub>," "wt CN<sub>17</sub>," "wt CN<sub>18</sub>," "wt CN<sub>19</sub>," "wt CN<sub>20</sub>," "wt CN<sub>21</sub>," "wt CN<sub>22</sub>," "wt CN<sub>23</sub>," and "wt CN<sub>24</sub>." Note that <i>q<sub>n</sub></i> refers to Steinhardt bond orientational order parameter of order <i>n</i>. The resulting site fingerprint is thus defined as:  
$$
\mathbf{v}^\mathrm{site} = [w|_{\mathrm{CN}=1}, \quad w|_{\mathrm{CN}=2}, \quad q_\mathrm{L}|_{\mathrm{CN}=2}, \quad q_\mathrm{water}|_{\mathrm{CN}=2}, \quad \dots, \quad w|_{\mathrm{CN}=24}]^\mathrm{T}
$$

## Structure Fingerprints
The fingerprints from sites in a given structure are subsequently statistically processed to yield the minimum, maximum, mean, and standard deviation of each coordination information element. The resultant ordered vector defines a structure fingerprint, <b>v</b><sup>struct</sup>:

$$
\mathbf{v}^\mathrm{struct} = [

\min(w|_{\mathrm{CN}=1}), \quad \max(w|_{\mathrm{CN}=1}), \quad \mathrm{mean}(w|_{\mathrm{CN}=1}), \quad \mathrm{std}(w|_{\mathrm{CN}=1}), \dots,

\min(w|_{\mathrm{CN}=24}), \quad \max(w|_{\mathrm{CN}=24}), \quad \mathrm{mean}(w|_{\mathrm{CN}=24}), \quad \mathrm{std}(w|_{\mathrm{CN}=24})

]^\mathrm{T}
$$

## Structure Distance/Dissimilarity
Finally, structure similarity is determined by the distance, <i>d</i>, between two structure fingerprints <b>v</b><sub><i>i</i></sub><sup>struct</sup> and <b>v</b><sub><i>j</i></sub><sup>struct</sup>:

$$
d = || \mathbf{v}_{i}^\mathrm{struct} - \mathbf{v}_{j}^\mathrm{struct} ||
$$

A small distance value indicates high similarity between two structures, whereas a large distance (>1) suggests that the structures are very dissimilar. The spinel example below gives an approximate threshold up to which <b>distance you can still consider two structures to be similar (0.9)</b>. Anything beyond 0.9 is most certainly not the same structure prototype.

## Examples
* Diamond ([mp-66](https://materialsproject.org/materials/mp-66/)) vs. GaAs ([mp-2534](https://materialsproject.org/materials/mp-2534/)) $\rightarrow$ <i>d</i> = 0
* Diamond ([mp-66](https://materialsproject.org/materials/mp-66/)) vs. rocksalt ([mp-22862](https://materiahttps://materialsproject.org/materials/mp-5827/lsproject.org/materials/mp-22862/)) $\rightarrow$ <i>d</i> = 3.5724
* Diamond ([mp-66](https://materialsproject.org/materials/mp-66/)) vs. perfect CaTiO3 perovskite ([mp-5827](https://materialsproject.org/materials/mp-5827/)) $\rightarrow$ <i>d</i> = 3.5540
* Rocksalt ([mp-22862](https://materialsproject.org/materials/mp-22862/)) vs. perfect CaTiO3 perovskite ([mp-5827](https://materialsproject.org/materials/mp-5827/)) $\rightarrow$ <i>d</i> = 2.7417
* Ca(CoS2)2-spinel ([mvc-12728](https://materialsproject.org/materials/mvc-12728/)) vs. Si(CdO2)2-spinel ([mp-560842](https://materialsproject.org/materials/mp-560842/)) $\rightarrow$ <i>d</i> = 0.8877

Below is a python code snippet that allows you to quickly reproduce above results. You will need to install [pymatgen](https://github.com/materialsproject/pymatgen) and [matminer](https://github.com/hackingmaterials/matminer) for this to work. Both are easily accessible via the [Python Package Index](https://pypi.python.org/pypi).

```python
import numpy as np
from pymatgen import MPRester
from matminer.featurizers.site import CrystalNNFingerprint
from matminer.featurizers.structure import SiteStatsFingerprint

with MPRester() as mpr:

    # Get structures.
    diamond = mpr.get_structure_by_material_id("mp-66")
    gaas = mpr.get_structure_by_material_id("mp-2534")
    rocksalt = mpr.get_structure_by_material_id("mp-22862")
    perovskite = mpr.get_structure_by_material_id("mp-5827")
    spinel_caco2s4 = mpr.get_structure_by_material_id("mvc-12728")
    spinel_sicd2O4 = mpr.get_structure_by_material_id("mp-560842")

    # Calculate structure fingerprints.
    ssf = SiteStatsFingerprint(
        CrystalNNFingerprint.from_preset('ops', distance_cutoffs=None, x_diff_weight=0),
        stats=('mean', 'std_dev', 'minimum', 'maximum'))
    v_diamond = np.array(ssf.featurize(diamond))
    v_gaas = np.array(ssf.featurize(gaas))
    v_rocksalt = np.array(ssf.featurize(rocksalt))
    v_perovskite = np.array(ssf.featurize(perovskite))
    v_spinel_caco2s4 = np.array(ssf.featurize(spinel_caco2s4))
    v_spinel_sicd2O4 = np.array(ssf.featurize(spinel_sicd2O4))

    # Print out distance between structures.
    print('Distance between diamond and GaAs: {:.4f}'.format(np.linalg.norm(v_diamond - v_gaas)))
    print('Distance between diamond and rocksalt: {:.4f}'.format(np.linalg.norm(v_diamond - v_rocksalt)))
    print('Distance between diamond and perovskite: {:.4f}'.format(np.linalg.norm(v_diamond - v_perovskite)))
    print('Distance between rocksalt and perovskite: {:.4f}'.format(np.linalg.norm(v_rocksalt - v_perovskite)))
    print('Distance between Ca(CoS2)2-spinel and Si(CdO2)2-spinel: {:.4f}'.format(np.linalg.norm(v_spinel_caco2s4 - v_spinel_sicd2O4)))
```

## References
[^1]: N. E. R. Zimmermann, D. Winston, K. A. Persson, A. Jain, in preparation (2018)  
[^2]: 10.3389/fmats.2017.00034  
[^3]: H. Pan, J. Dagdelen, N. E. R. Zimmermann, A. Jain, in preparation (2018)

## Authors
Nils Zimmermann, Donny Winston, Handong Ling, Oxana Andriuc
