# The Materials API

The Materials API (MAPI) is an open API for accessing Materials Project data based on REpresentational State Transfer (REST) principles.
In a RESTful system, information is organized into **resources**, each of which is uniquely identified via a uniform resource identifier (URI).

While the MAPI is designed to be code base agnostic and can conceivably be used with any programming language supporting basic http requests, a convenient wrapper to MAPI has been implemented in the [Python Materials Genomics (pymatgen)](http://pypi.python.org/pypi/pymatgen) library to facilitate researchers in using the MAPI.
Please see the [#pymatgen wrapper](#pymatgen-wrapper) section.

For a quick overview, please refer to the following [slides](http://www.slideshare.net/shyuep/the-materials-api-v1).

For a comprehensive listing of all criteria available for advanced queries via the [#mpquery](#mpquery) endpoint, see [this repository](https://github.com/materialsproject/mapidoc).

## Resources

In the Materials Project, resources are generally packages of information about a material or an analysis (e.g., a reaction).
Currently supported information types (v2 of the REST API) include the following:

**Materials** - Standard calculated or experimental information about a material.

**Battery** - Battery application specific information.

**Reaction** - Information about a reaction.

## Authentication

### SSL Encryption

All requests to the Materials API must be done over HTTPS.
Non-secure http requests are not allowed and will result in a HTTP 403 (Forbidden) response.

### API keys

To access the Materials API, you will need your API key, except for certain free queries that do not require a key.
You can obtain your API key by logging into the Materials Project website, and going to [your dashboard](https://materialsproject.org/dashboard).
Your API key and a button to regenerate the key is provided at the top of the page.

Note that the API key effectively allows access to Materials Project data via your account.
You should therefore make all efforts to keep it secret and under no circumstances should you share your API key with anyone.
You will be held responsible for any violations conducted using your API key.
Should anyone else require access to the MAPI, they should register for an account on the Materials Project and generate their own API keys.

All MP https requests must supply API key as:

- A x-api-key header, e.g., {‘X-API-KEY’: ‘YOUR_API_KEY’} (recommended method) or
- As a GET (e.g., ?API_KEY=YOUR_API_KEY) or POST variable, e.g., {‘API_KEY’: ‘YOUR_API_KEY’}

The following is an example of a full url requesting for information of the material with material id 1234 with the API key supplied as a GET variable.

`https://www.materialsproject.org/rest/v2/materials/mp-1234/vasp?API_KEY=YOUR_API_KEY`

## Security

You agree not to use automated scripts to collect large fractions of the database and disseminate them.
You may collect large fractions of the database for analysis and to present processed results with proper attribution.
If you plan to download large datasets, please email heavy.api.use@materialsproject.org with the email address associated with your account and with your use case so that we can avoid flagging your account as abusing the service.
We may also suggest an efficient way for you to obtain the data you need.
We reserve the right to disable API keys as a security precaution against bots.

## API documentation

### General URI Format

All URIs in the MAPI are of the general form

`https://www.materialsproject.org/rest/v2/{request_type}[/{identifier}][/{parameters}]`

1. The initial part of the URI (<https://www.materialsproject.org/rest/v2/>) is a preamble, specifying a https REST request. The v2 denotes version 2 of the MAPI, to provide flexibility to support multiple versions of the API in future.
2. {request_type} specifies the kind of information or operation being requested. Currently supported request types include "materials", "battery", "reaction", "mpquery" and "api_check".
3. {identifier} is an identifier for the specific information requested. Depending on the {request_type}, an identifier may or may not be necessary.
4. {parameters} - Some requests require additional parameters to be provided.

### General Response Format

All responses from the Materials API are in the JavaScript Object Notation (JSON).
XML is not supported currently.
The responses generally are of the following form:

```json
 {
    valid_response: true,
    version: {
        pymatgen: "2.2.0",
        db: "2012.07.09",
        rest: "1.0"
    },
    created_at: "2012-08-29T05:21:51.232084",
    copyright: "Copyright 2012, The Materials Project",
    response: {response_content}
}
```

### Resource Details

#### materials (calculated materials data)

`GET https://www.materialsproject.org/rest/v2/materials/{material id, formula, or chemical system}/vasp/{property}`

Obtain material information based on an identifier.
The response is always a list of associative arrays, i.e., [ {key:value, ... }, {... }, ...].
The identifier can be a Materials Project material id (e.g., mp-1234), a formula, e.g. (Fe2O3), or a chemical system ("-" separated list of elemments, e.g., Li-Fe-O).
Specifying a formula or chemical system will return information for all materials with that formula or in that chemical system respectively.
Note that a chemical system includes all sub-systems, i.e., the Li-Fe-O chemical system will include all Li, Fe, O, FexOy, LixOy, LixFey, LixFeyOz compounds.

A property may be specified to request a specific subset of information.
If no property is specified, a set of typically useful properties is returned.
The materials id is always returned as part of the response.
Currently supported properties and their definitions are as follows:

##### Basic properties

<dl>
  <dt>pretty_formula</dt>
  <dd>A nice formula where the element amounts are normalized</dd>
  <dt>unit_cell_formula</dt>
  <dd>The full explicit formula for the unit cell</dd>
  <dt>icsd_ids</dt>
  <dd>List of Inorganic Crystal Structure Database (ICSD) ids for structures that have been deemed to be structurally similar to this material based on pymatgen's StructureMatcher algorithm, if any.</dd>
  <dt>energy</dt>
  <dd>Calculated vasp energy for structure</dd>
  <dt>energy_per_atom</dt>
  <dd>Calculated vasp energy normalized to per atom in the unit cell</dd>
  <dt>volume</dt>
  <dd>Final relaxed volume of the material</dd>
  <dt>density</dt>
  <dd>Final relaxed density of the material</dd>
  <dt>nsites</dt>
  <dd>Number of sites in the unit cell</dd>
  <dt>elements</dt>
  <dd>A array of the elements in the material</dd>
  <dt>nelements</dt>
  <dd>The number of elements in the material</dd>
  <dt>spacegroup</dt>
  <dd>An associative array containing basic space group information.</dd>
  <dt>initial_structure</dt>
  <dd>The initial input structure for the calculation in the pymatgen json representation (see later section).</dd>
  <dt>final_structure</dt>
  <dd>The final relaxed structure in the pymatgen json representation (see later section).</dd>
  <dt>structure</dt>
  <dd>An alias for final_structure.</dd>
  <dt>cif</dt>
  <dd>A string containing the structure in the CIF format.</dd>
</dl>

##### Thermodynamic properties

<dl>
  <dt>formation_energy_per_atom</dt>
  <dd>Calculated formation energy from the elements normalized to per atom in the unit cell</dd>
  <dt>e_above_hull</dt>
  <dd>Calculated energy above convex hull for structure. Please see Phase Diagram Manual for the interpretation of this quantity.</dd>
</dl>

##### Mechanical properties

<dl>
 <dt>elasticity</dt>
 <dd>Mechanical properties in the elastic limit. Contains the full elastic tensor as well as derived properties, e.g. Poisson ratio and bulk (K) and shear (G) moduli. Consult our hierarchical documentation for the particular names of sub-keys.</dd>
 <dt>piezo</dt>
 <dd>Piezoelectric properties. Contains a tensor and derived properties. Again, consult our repository for the names of sub-keys.</dd>
 <dt>diel</dt>
 <dd>Dielectric properties. Contains a tensor (one each for total and electronic contribution) and derived properties, e.g. dielectric constant, refractive index, and recognized potential for ferroelectricity.</dd>
</dl>

##### Calculation parameters

<dl>
 <dt>is_hubbard</dt>
 <dd>A boolean indicating whether the structure was calculated using the Hubbard U extension to DFT</dd>
 <dt>hubbards</dt>
 <dd>An array of Hubbard U values, where applicable.</dd>
 <dt>is_compatible</dt>
 <dd>Whether this calculation is considered compatible under the GGA/GGA+U mixing scheme.</dd>
</dl>

##### Electronic structure

<dl>
 <dt>band_gap</dt>
 <dd>The calculated band gap</dd>
 <dt>dos</dt>
 <dd>The calculated density of states in the pymatgen json representation</dd>
 <dt>bandstructure</dt>
 <dd>The calculated "line mode" band structure (along selected symmetry lines -- aka "branches", e.g. \Gamma to Z -- in the Brillouin zone) in the pymatgen json representation</dd>
 <dt>bandstructure_uniform</dt>
 <dd>The calculated uniform band structure in the pymatgen json representation</dd>
</dl>

##### Others

<dl>
 <dt>entry</dt>
 <dd>This is a special property that returns a pymatgen ComputedEntry in the json representation. ComputedEntries are the basic unit for many structural and thermodynamic analyses in the pymatgen code base.</dd>
 <dt>total_magnetization</dt>
 <dd>total magnetic moment of the unit cell</dd>
</dl>

Example responses:

1. `https://www.materialsproject.org/rest/v1/materials/24972/vasp`: [File:24972.txt](/static/mapi/24972.txt)
2. `https://www.materialsproject.org/rest/v1/materials/Fe2O3/vasp`: [File:Fe2O3.txt](/static/mapi/Fe2O3.txt)
3. `https://www.materialsproject.org/rest/v1/materials/Li-Fe-O/vasp`: [File:Li-Fe-O.txt](/static/mapi/Li-Fe-O.txt)
4. `https://www.materialsproject.org/rest/v1/materials/TiO2/vasp/energy`: [File:TiO2_energy.txt](/static/mapi/TiO2_energy.txt)
5. `https://www.materialsproject.org/rest/v1/materials/C/vasp/structure`: [File:C_structure.txt](/static/mapi/C_structure.txt)

#### materials (experimental data)

`GET https://www.materialsproject.org/rest/v2/materials/{formula}/exp`

Obtain experimental thermochemical information based on an formula. The response is always a list of associative arrays, i.e., [ {key:value, ... }, {... }, ...]. The associative arrays are pymatgen ThermoData objects in json representation.

Example response:

1. `https://www.materialsproject.org/rest/v1/materials/Fe2O3/exp`: [File:Fe2O3_exp.txt](/static/mapi/Fe2O3_exp.txt)

#### tasks (detailed calculation data)

`GET https://www.materialsproject.org/rest/v2/tasks/{task id}/{property}`

Obtain information about a particular calculation based on a task id. The response is always a list of associative arrays, i.e., [ {key:value, ... }, {... }, ...].

A property may be specified to request a specific subset of information. If no property is specified, a set of typically useful properties is returned. The materials id is always returned as part of the response. Currently supported properties and their definitions are as follows:

##### Basic properties list

<dl>
 <dt>pretty_formula</dt>
 <dd>A nice formula where the element amounts are normalized</dd>
 <dt>unit_cell_formula</dt>
 <dd>The full explicit formula for the unit cell</dd>
 <dt>icsd_id</dt>
 <dd>The Inorganic Crystal Structure Database id for the initial structure, if any.</dd>
 <dt>energy</dt>
 <dd>Calculated vasp energy for structure</dd>
 <dt>energy_per_atom</dt>
 <dd>Calculated vasp energy normalized to per atom in the unit cell</dd>
 <dt>volume</dt>
 <dd>Final relaxed volume of the material</dd>
 <dt>density</dt>
 <dd>Final relaxed density of the material</dd>
 <dt>nsites</dt>
 <dd>Number of sites in the unit cell</dd>
 <dt>elements</dt>
 <dd>A array of the elements in the material</dd>
 <dt>nelements</dt>
 <dd>The number of elements in the material</dd>
 <dt>initial_structure</dt>
 <dd>The initial input structure for the calculation in the pymatgen json representation (see later section).</dd>
 <dt>final_structure</dt>
 <dd>The final relaxed structure in the pymatgen json representation (see later section).</dd>
 <dt>structure</dt>
 <dd>An alias for final_structure.</dd>
</dl>

#### Thermodynamic properties list

<dl>
 <dt>formation_energy_per_atom</dt>
 <dd>Calculated formation energy from the elements normalized to per atom in the unit cell</dd>
 <dt>e_above_hull</dt>
 <dd>Calculated energy above convex hull for structure. Please see Phase Diagram Manual for the interpretation of this quantity.</dd>
</dl>

#### Calculation parameters list

<dl>
 <dt>is_hubbard</dt>
 <dd>A boolean indicating whether the structure was calculated using the Hubbard U extension to DFT</dd>
 <dt>hubbards</dt>
 <dd>An array of Hubbard U values, where applicable.</dd>
 <dt>is_compatible</dt>
 <dd>Whether this calculation is considered compatible under the GGA/GGA+U mixing scheme.</dd>
</dl>

#### Electronic structure list

<dl>
 <dt>band_gap</dt>
 <dd>The calculated band gap</dd>
 <dt>dos</dt>
 <dd>The calculated density of states in the pymatgen json representation</dd>
 <dt>incar</dt>
 <dd>The INCAR parameters used for the run.</dd>
 <dt>kpoints</dt>
 <dd>The KPOINTS grid used for the run.</dd>
 <dt>potcar</dt>
 <dd>The pseudopotentials used for the run.</dd>
</dl>

The responses are similar to the materials responses.

#### materials ids

`GET https://www.materialsproject.org/rest/v2/materials/{formula or chemical system}/mids`

Obtain the material ids relating to a formula or chemical system. The response is always a list of integers. This is one of the few types of queries that do not require an API key to be supplied.

Example responses:

1. <https://www.materialsproject.org/rest/v2/materials/Fe2O3/mids>
2. <https://www.materialsproject.org/rest/v2/materials/Fe-O/mids>

#### mpquery

`POST https://www.materialsproject.org/rest/v2/query`

Advanced query using Mongo-like language for flexible queries on the Materials Project database. This provides the possibility of queries which would otherwise not be possible using the other simpler REST forms.

For example, a POST to mpquery with

`{"criteria": "{'elements':{'$in':['Li', 'Na', 'K'], '$all': ['O']}, 'nelements':2}", "properties": "['formula', 'formation_energy_per_atom']"}`

will return the formula and formation energy per atom of all Li, Na and K oxides. Supported keywords include the following: elements, nelements, nsites, formula, normalized_formula, energy, energy_per_atom, density, e_above_hull, formation_energy_per_atom, material_id. For a comprehensive listing of all criteria available, see [this repository](https://github.com/materialsproject/mapidoc).

### Operations

#### api_check

`GET or POST https://www.materialsproject.org/rest/v1/api_check`

Checks if supplied API key (via GET, POST or x-api-key header) is a valid API key.

Example response:

<pre>{
    valid_response: true,
    api_key_valid: true
}
</pre>
