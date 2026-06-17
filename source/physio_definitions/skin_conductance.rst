Skin Conductance (SCR)
======================

Following the `BIDS Physiological recordings specification <https://bids-specification.readthedocs.io/en/stable/modality-specific-files/physiological-recordings.html>`_, M-BIDS uses the following additional Calibench requirements for skin conductance data.

In addition to the BIDS ``_physio.tsv.gz`` / ``_physio.json`` pair, skin conductance data MUST use the recording label ``scr`` and should be organized as follows:

.. code-block:: text

    physio/
    ├── sub-<participant_label>_task-acquisition_recording-scr_physio.json
    └── sub-<participant_label>_task-acquisition_recording-scr_physio.tsv.gz


Column names in the ``scr`` data files MUST be ``timestamp`` followed by ``scr`` for experiments involving single recordings. For simultaneous parallel SCR recordings from different locations on the body, use ``timestamp`` followed by ``scr1``, ``scr2``, ``scr3``, and so on.


These fields **MUST** be included in the JSON sidecar file:  
``<matches>_recording-scr_physio.json``


Additional Metadata Fields
--------------------------

.. list-table:: Table 1: Required SCR-specific JSON fields
   :header-rows: 1
   :widths: 25 25 15 25

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


Example TSV Data File
---------------------

Compressed ``*.tsv.gz`` files are headerless. The columns are defined by the JSON sidecar.

.. code-block:: text
  
    0.0	3.3676146995269107
    0.0004999999999881766	3.3706664573394107
    0.0009999999999763531	3.3706664573394107
    ...

In this example, the sidecar ``Columns`` value is ``["timestamp", "scr"]``.

Example JSON Sidecar
--------------------

.. code-block:: json

    {
        "Columns": [
            "timestamp",
            "scr"
        ],
        "Manufacturer": "Biopac Systems",
        "ManufacturersModelName": "MP160CE",
        "DeviceSerialNumber": "1709a-0001C1F",
        "SoftwareVersion": null,
        "StartTime": 0.0,
        "PhysioType": "generic",
        "timestamp": {
            "LongName": "Time",
            "Description": "a continuously increasing identifier of the sampling time registered by the device",
            "Origin": "System startup",
            "Units": "s"
        },
        "scr": {
            "Description": "SCR Recording",
            "SCRCouplerType": "AC",
            "SCRCouplerVoltage": 0.5,
            "Placement": "right forearm",
            "Units": "uS",
            "MeasureType": "EDA-total"
        },
        "SamplingFrequency": 2000.0,
        "TrimPoints": [
            882.7075,
            1530.7065
        ],
        "Duration": 647.999
    }
