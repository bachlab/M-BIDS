
Electrocardiogram (ecg)
=======================

Following the guidelines from 
`BIDS v1.10.0 <https://bids-specification.readthedocs.io/en/stable/modality-specific-files/physiological-recordings.html>`_, 
we propose the following **additional requirements** for ECG data.

Modality specific data SHOULD be split into modality specific files carrying the modality-label. Modality label for skin conductance is ``ecg`` and ECG specific data files would be organized as follows

.. code-block:: text

    physio/
    ├─ sub-01_ses-1_task-TaskName_recording-ecg_physio.json 
    ├─ sub-01_ses-1_task-TaskName_recording-ecg_physio.tsv.gz


Column names in the ``ecg`` data files MUST be ``ecg`` for experiments involving single recordings, or ``ecg1``, ``ecg2``, ``ecg3``, ... for experiments involving simultaneous parallel ECG recordings from different locations on the body.


These fields **MUST** be included in the JSON sidecar file:  
``<matches>_recording-ecg_physio.json``


Additional Metadata Fields
--------------------------

.. list-table:: Table 1: Required SCR-Specific JSON Fields
   :header-rows: 1
   :widths: 25 45 15 25

   * - Key
     - Description
     - Data Type
     - Possible Values
   * - ``Placement``
     - Configuration of the recorded ECG leads
     - Text
     - ``I``, ``II``, ``III``, ``aVF``, ``aVR``, ``aVL``, ``V1``, ``V2``, ``V3``, ``V4``, ``V5``, ``V6``, ``other``


Example Data
------------

Example values from the corresponding TSV file:

.. code-block:: text

    -0.140686035156250
    -0.131378173828125
    -0.121612548828125
    -0.111236572265625
    -0.0994873046875000
    -0.0865173339843750
    -0.0727844238281250
    . . .



Example JSON Sidecar
--------------------

.. code-block:: json

    {
        "Columns": [
                "ecg",
        ],
        "Manufacturer": "<Manufacturer-Name>",
        "ManufacturersModelName": "<Manufacturer-Model-Name>",
        "DeviceSerialNumber": "<Device-Serial-Number>",
        "SamplingFrequency": 2000,
        "SoftwareVersion": "<Software-version>",
        "StartTime": 0,
        "PhysioType": "specified",
        "ecg": {
                "Description": "ECG Recording",
            "LeadConfiguration": "II",
            "Units": "mV"
        }
    }

