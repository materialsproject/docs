# X-Ray Absorption Spectra
## Methodology

All the spectra (only K-edge XANES currently) were computed using the [FEFF](http://leonardo.phys.washington.edu/index-feffproject.html) code. For each structure, spectra were computed with each symmetrically unique site 
in the structure as the absorbing site. The workflow used for the calculations can be found in the open source comprehensive materials science 
workflow package, [Atomate](https://github.com/hackingmaterials/atomate) [^1] in the <code>atomate.feff</code> namespace. The package leverages [Pymatgen](https://github.com/materialsproject/pymatgen) and 
[Fireworks](https://github.com/materialsproject/fireworks) packages for the generation of the input/output files for the calculations and for the workflow 
execution management respectively.

These results are intended to be semi-quantitative in that corrections, such as edge shifts and Debye-Waller damping, have not been included.

## Presentation of Spectra

The computed absorption coefficient for an element in the given structure is set to the absorption coefficient averaged over all the sites in the structure with that element.

See MP's database builder repository [Emmet](https://github.com/materialsproject/emmet) (<code>emmet.feff.builders.xas</code> module) for details.

## References

[^1]: 10.1016/j.commatsci.2017.07.030
