Skin Conductance (scr)
======================

Following the guidelines from 
`BIDS v1.10.0 <https://bids-specification.readthedocs.io/en/stable/modality-specific-files/physiological-recordings.html>`_, 
we propose the following **additional requirements** for skin conductance data.

Modality specific data SHOULD be split into modality specific files carrying the modality-label. Modality label for skin conductance is ``scr`` and scr specific data files would be organized as follows

.. code-block:: text

    physio/
    ├─ sub-01_ses-1_task-TaskName_recording-scr_physio.json 
    ├─ sub-01_ses-1_task-TaskName_recording-scr_physio.tsv.gz


Column names in the ``scr`` data files MUST be ``scr`` for experiments involving single recordings, or ``scr1``, ``scr2``, ``scr3``, ... for experiments involving simultaneous parallel SCR recordings from different locations on the body.


These fields **MUST** be included in the JSON sidecar file:  
``<matches>_recording-scr_physio.json``


Additional Metadata Fields
--------------------------

.. list-table:: Table 1: Required SCR-Specific JSON Fields
   :header-rows: 1
   :widths: 25 45 15 25

   * - Key
     - Description
     - Data Type
     - Possible Values
   * - ``SCRCouplerVoltage``
     - Voltage of the constant voltage SCR coupler (in V).
     - Number
     - e.g., 0.5
   * - ``SCRCouplerType``
     - Type of SCR coupler.
     - Text
     - ``AC``, ``DC``
   * - ``Placement``
     - Position of SCR electrodes on the body.
     - Text
     - ``thenar/hypothenar``, ``digits 2/3``, ...


Example Data
------------

Example values from the corresponding TSV file:

.. code-block:: text

    0.0198363792144107
    0.0152587424956607
    0.0198363792144107
    0.0152587424956607
    0.0198363792144107
    ...


Example JSON Sidecar
--------------------

.. code-block:: json

    {
        "Columns": [
            "scr"
        ],
        "Manufacturer": "Biopac",
        "ManufacturersModelName": "EDA100C",
        "DeviceSerialNumber": "1111-1111-1111",
        "SamplingFrequency": 2000,
        "SoftwareVersion": "Acquisition 1.10",
        "StartTime": 0,
        "PhysioType": "specified",
        "scr": {
            "Description": "SCR Recording",
            "SCRCouplerType": "AC",
            "SCRCouplerVoltage": 0.5,
            "Placement": "thenar",
            "Units": "microsiemens"
        }
    }
