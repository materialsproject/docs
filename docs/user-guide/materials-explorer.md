# Initial release of Materials Explorer.
# Key features
## Basic search over multiple data fields.
```
from pymatgen import MPRester, Composition
import re
import pprint

mpr = MPRester()
c = Composition('Ni3O4')
data = mpr.query(criteria = {'pretty_formula': c.reduced_formula}, 
                 properties=['task_id', 'spacegroup', 'formation_energy_per_atom'])
```
## Complete data table with listing of stable and unstable phases.
```
import collections
from pandas import DataFrame
from pymatgen.ext.matproj import MPRester
from pymatgen.analysis.phase_diagram import PhaseDiagram, PDPlotter

a = MPRester()
data = collections.defaultdict(list)
entries = a.get_entries_in_chemsys(['Li', 'Ni', 'O'])
pd = PhaseDiagram(entries)

for e in pd.stable_entries:
    decomp, ehull = pd.get_decomp_and_e_above_hull(e)
    data["Materials ID"].append(e.entry_id)
    data["Composition"].append(e.composition.reduced_formula)
    data["Ehull"].append(ehull)    
    data["Decomposition"].append(" + ".join(["%.2f %s" % (v, k.composition.formula) for k, v in decomp.items()]))

df = DataFrame(data, columns=["Materials ID", "Composition", "Ehull", "Decomposition"])

print('Stable phases\n%s' % df)

for e in pd.unstable_entries:
    decomp, ehull = pd.get_decomp_and_e_above_hull(e)
    data["Materials ID"].append(e.entry_id)
    data["Composition"].append(e.composition.reduced_formula)
    data["Ehull"].append(ehull)    
    data["Decomposition"].append(" + ".join(["%.2f %s" % (v, k.composition.formula) for k, v in decomp.items()]))

df = DataFrame(data, columns=["Materials ID", "Composition", "Ehull", "Decomposition"])

print('\nUnstable phases\n%s' % df)
```
