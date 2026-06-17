
Electrocardiogram (ecg)
=======================

Following the `BIDS Physiological recordings specification <https://bids-specification.readthedocs.io/en/stable/modality-specific-files/physiological-recordings.html>`_, M-BIDS uses the following additional Calibench requirements for ECG data.

In addition to the BIDS ``_physio.tsv.gz`` / ``_physio.json`` pair, ECG data MUST use the recording label ``ecg`` and should be organized as follows:

.. code-block:: text

    physio/
    ├── sub-<participant_label>_task-acquisition_recording-ecg_physio.json
    └── sub-<participant_label>_task-acquisition_recording-ecg_physio.tsv.gz


Column names in the ``ecg`` data files MUST be ``timestamp`` followed by ``ecg`` for experiments involving single recordings. For simultaneous parallel ECG recordings from different locations on the body, use ``timestamp`` followed by ``ecg1``, ``ecg2``, ``ecg3``, and so on.


These fields **MUST** be included in the JSON sidecar file:  
``<matches>_recording-ecg_physio.json``


Additional Metadata Fields
--------------------------

.. list-table:: Table 1: Required ECG-specific JSON fields
   :header-rows: 1
   :widths: 25 25 15 25

   * - Key
     - Description
     - Data Type
     - Possible Values
   * - ``Placement``
     - Configuration of the recorded ECG leads
     - Text
     - ``I``, ``II``, ``III``, ``aVF``, ``aVR``, ``aVL``, ``V1``, ``V2``, ``V3``, ``V4``, ``V5``, ``V6``, ``other``


Example TSV Data File
---------------------

Compressed ``*.tsv.gz`` files are headerless. The columns are defined by the JSON sidecar.

.. code-block:: text
    
    0.0	-0.093841552734375
    0.0004999999999881766	-0.096282958984375
    0.0009999999999763531	-0.097808837890625
    . . .

In this example, the sidecar ``Columns`` value is ``["timestamp", "ecg"]``.


Example JSON Sidecar
--------------------

.. code-block:: json

    {
        "Columns": [
            "timestamp",
            "ecg"
        ],
        "Manufacturer": "Biopac Systems",
        "ManufacturersModelName": "ECG100C",
        "DeviceSerialNumber": "1711008598",
        "SoftwareVersion": "Biopac AcqKnowledge 5.0.2",
        "StartTime": 0.0,
        "PhysioType": "generic",
        "timestamp": {
            "LongName": "Time",
            "Description": "a continuously increasing identifier of the sampling time registered by the device",
            "Origin": "System startup",
            "Units": "s"
        },
        "ecg": {
            "Description": "ECG Recording",
            "Placement": "underneath the right clavicle, as well as the left and right costal margin",
            "Units": "mV"
        },
        "SamplingFrequency": 2000.0,
        "TrimPoints": [
            882.7075,
            1530.7065
        ],
        "Duration": 647.999
    }

