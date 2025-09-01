Eyetracking (eye)
=================

Following the guidelines from 
`BEP020 <https://github.com/bids-standard/bids-specification/pull/1128>`_, 
we propose the following **additional requirements** for eyetracking data.

Modality specific data SHOULD be split into modality specific files carrying the modality-label. Modality label for skin conductance is ``ecg`` and ECG specific data files would be organized as follows

.. code-block:: text

    physio/
    ├─ sub-01_ses-1_task-TaskName_recording-eye1_physio.json 
    ├─ sub-01_ses-1_task-TaskName_recording-eye2_physio.json 
    ├─ sub-01_ses-1_task-TaskName_recording-eye1_physio.tsv 
    ├─ sub-01_ses-1_task-TaskName_recording-eye2_physio.tsv 

**For facilitating automated data processing, we REQUIRE ``eye1`` to correspond to the ``left`` eye, and ``eye2`` to correspond to the ``right`` eye.**

Eyetracking Physiological Data
------------------------------

**TSV file:** ``<matches>_recording-eye1_physio.tsv``  
- Contains eyetracking timeseries data.  
- Column names are **not required**.  

**JSON sidecar:** ``<matches>_recording-eye1_physio.json``  
- Must include metadata as specified in BEP020.  


Eyetracking Events
------------------

The eyetracking “physioevents” file contains information about physiological events detected by the eyetracker during the session.  

**Files:**  
- ``<matches>_physioevents.tsv``  
- ``<matches>_physioevents.json``  
