# Database updates

!!! warning
Up-to-date release notes are now posted to
[this thread](https://discuss.materialsproject.org/t/materials-project-database-release-log/1609)
on our discussion forum.

!!! info
Confused about materials being "deprecated"? [More info here](/user-guide/deprecations).

## Current Database versions

### V2019.05

- Introduced a new `deprecated` field to materials. By default the website and API only search for materials that are not deprecated: {"deprecated": false}.
- Deprecated 15,000 and added 3,600 new materials. We will be recomputing the deprecated materials to fill these spaces back up. Some of these new relaxations may end up matching current materials, so the total number of materials is not guaranteed to be the same as in V2019.02.
- Fixed an issue with sandboxes not properly building the whole hull. Previously, only the sandboxed chemical systems were being recalculated for energy_above_hull searches

### V2019.02

- Added over 47,000 new materials from orderings of disordered ICSD as well as compounds from the Pauling File
- Finalized enforcing symmetry on piezo tensors
- Moved third order elastic data to elasticity_third_order so that people are not swamped by the mountain of information associated with it.

### V2018.12

- Adjusted the mp-id naming scheme to fix “mvc” ids taking over old mp-ids.
- Fixed piezoeletric max_direction to be a miller index rather than a unit vector.

### Version 2018.11, Release Date: 2018-11-01

We've released a new revision of the Materials Project database as part of major overhaul of our software infrastructure
to enable us to continue to build new properties and deliver them to you, the material science community, at an accelerating
pace. This has also caused some growing pains as we fix bugs we created in building our new infrastructure from scratch.

Many of our users have reported bugs and we are very grateful for that. We're making great strides in being as transparent
as possible so everyone knows what is changing. As part of this we've settled on a monthly release schedule including an
announcement that informs everyone on what has or has not changed. To kick this process off we have our current changes
for the MP Database Release V2018.11. This will be updated on a monthly basis with what has changed.

V2018.11

- Changed the grouping of magnetic materials to aggregate all magnetic orderings of a given material into a single
  material-id, and report the lowest energy ordering
- Fixed incorrect calculation and display of polycrystalline dielectric constants
- Fixed labeling of all materials as high-pressure. Note we're parsing ICSD tags for this labeling so while some materials
  may not conventionally be considered high-pressure, a single matching ICSD entry can tag a material as such. We would love
  to hear comments on how we could better tag high-pressure materials
- 5,849 new material ids.
- 3,556 retiring/re-aggregated material ids

### Version 2.0.0, Release Date: 04/13/2016

- Equivalent to old version "2014.04.18"
- Use major.minor.patch versioning, inspired by [semantic versioning](https://semver.org/), but for data. Arbitrarily choose "2" as the initial major version.
- When new data is added (typically nightly), db version remains the same
- When new kinds of data are added, bump the patch (x.y.Z) version
- When data organization (schema) changes, bump the minor (x.Y.z) version
- When calculation methodology changes, bump the major (X.y.z) version

## Old databases

Data from the earlier 'Materials Genome' web site, served prior to 10/10/2011, is no longer supported.

### Version 2014.04.18, Release Date: 04/18/2014

- Version unchanged until 04/13/2016. Renamed to "2.0.0" for semantic versioning.

### Version 0.5.1, Release Date: 10/10/2011

- Initial Materials Project Database

### Version 1.1, Release Date: 3/25/2011

- Removed fitted adjustments to P,S,C,Br,H<sub>2</sub> by default in the calculations.

### Version 1.0, Release Date: 2/28/2011

- Root database (MIT database with ICSD only entries)
