# Help Us Expand Our Database

## What is MPComplete?

MPComplete is a service we offer to the community, whereby users can submit crystal structures to us that are not already in our database, that we then add to our calculation queue to calculate lattice parameters, relaxed atomic geometries, and total energies. This helps us to complete our database.

## What Crystal Structures Are Appropriate

Any bulk-like crystal structure can be submitted to the Materials Project using MPComplete. Please do not submit defects, surfaces, and the like, or organic compounds.

Two-dimensional materials can be submitted but we do not currently converge the vacuum layer, so please make sure there is sufficient vacuum in the cell (typically at least greater than 10 Å). Layered materials can also be submitted but note that we do not currently use a van der Waals functional so inter-layer spacing will not be calculated accurately.

## Submitting Crystal Structures via the Website

You can submit individual structures online using [Crystal Toolkit](crystal-toolkit.html) and using the 'Submit to MPComplete' button. Crystal structures can be imported by uploading a CIF file or similar and can be optionally transformed by substituting atomic species or similar before submission. Please make sure to enter any comments or references as appropriate so that we can properly attribute the source of the crystal structure. 

A one-minute video walkthrough of the process is available [here](https://www.youtube.com/watch?v=4c8MZdD0L3c).

## Submitting Crystal Structures in Bulk

For bulk submission of structures it would be easier to use our *pymatgen* Python code and API to submit structures. Please contact us for detailed instructions at feedback@materialsproject.org

## Monitoring the Status of Your Submissions

On your [Dashboard](https://materialsproject.org/dashboard), under Submitted Structures, each structure entry has a status label that corresponds to the 'state' of a corresponding FireWorks workflow ([reference of FireWorks states](https://materialsproject.github.io/fireworks/reference.html/)).

Common states include:

* `READY`: calculations are ready to be performed for the submission, where the crystal structure has passed initial inspection, but the job has not started running.
* `REJECTED`: calculations were not performed, and an explanation for why the crystal structure was rejected will be shown.
* `RESERVED`: At least one calculation has been submitted to the queue to run. The queue is finite in size, so `READY` jobs do not necessarily become immediately `RESERVED`.
* `RUNNING`: Calculations are running. Depending on your structure, this stage could take a while.
* `COMPLETED`: The submission has been fully processed, and should result in a new material on our website in our next database release, provided it did not relax to a duplicate structure.
