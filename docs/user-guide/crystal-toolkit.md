# Crystal Toolkit

The Crystal Toolkit app allows one to load structures, either via MP material ids or via uploading CIF or POSCAR files, and generate new crystals by substituting or removing species. One can also specify a scaling matrix to change a loaded structure's supercell dimensions.

Once edits are made to a loaded structure, one can download the transformed structure as a CIF, POSCAR, etc. One can also submit a transformed structure to MP. If our automated algorithms determine that your structure is unique, we will compute the properties of your submitted compound and the results will appear on the website.

## MP-Complete (submitting structures)

We are continually adding new compounds and expanding the range of computed properties available. We have also received many valuable suggestions from users on new structures to include in our database. We believe that such user feedback is critical to ensuring that the Materials Project remains up-to-date and relevant, and MP-Complete is our initiative to facilitate the process.

You may recommend new crystals for calculation via the Crystal Toolkit:

- Load a structure, either by MP-ID or through file upload.
- (Optional) Modify an existing structure to create a novel compound.
- Click the “Submit Structure” button under the structure view.
- Check your [Dashboard](https://materialsproject.org/dashboard) for updates.

A one-minute video walkthrough of the process is available [here](https://www.youtube.com/watch?v=4c8MZdD0L3c).

## Monitoring the Status of Your Submissions

On your [Dashboard](https://materialsproject.org/dashboard), under Submitted Structures, each structure entry has a status label that corresponds to the 'state' of a corresponding FireWorks workflow ([reference of FireWorks states](https://materialsproject.github.io/fireworks/reference.html/)). Common states include:
 READY : calculations are ready to be performed for the submission, i.e. it has passed initial inspection, but the job has not started running.
 
<dl>
  <dt>REJECTED</dt>
  <dd>Calculations were not performed for a reason that is displayed.</dd>

  <dt>RESERVED</dt>
  <dd>At least one calculation has been submitted to the queue to run. The queue is finite in size, so READY jobs do not necessarily become immediately RESERVED.</dd>
  
  <dt>RUNNING</dt>
  <dd>Calculations are running. Depending on your structure, this stage could take a while.</dd>
  
  <dt>COMPLETED</dt>
  <dd>The submission has been fully processed, perhaps resulting in a new material on our website. We run our website database builders nightly, so completed calculations may not be immediately available.</dd>
</dl>
