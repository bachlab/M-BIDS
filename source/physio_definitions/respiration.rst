Respiration (resp)
==================

Following the `BIDS Physiological recordings specification <https://bids-specification.readthedocs.io/en/stable/modality-specific-files/physiological-recordings.html>`_, M-BIDS uses the following additional Calibench requirements for respiratory data.

In addition to the BIDS ``_physio.tsv.gz`` / ``_physio.json`` pair, respiration data MUST use the recording label ``resp`` and should be organized as follows:

.. code-block:: text

    physio/
    ├── sub-<participant_label>_task-acquisition_recording-resp_physio.json
    └── sub-<participant_label>_task-acquisition_recording-resp_physio.tsv.gz


Column names in the ``resp`` data files MUST be ``timestamp`` followed by ``resp`` for experiments involving single recordings. For different types of respiratory measurements, use ``timestamp`` followed by ``resp1``, ``resp2``, ``resp3``, and so on.


These fields **MUST** be included in the JSON sidecar file:  
``<matches>_recording-resp_physio.json``


Additional Metadata Fields
--------------------------

.. list-table:: Table 1: Required respiration-specific JSON fields
   :header-rows: 1
   :widths: 25 25 15 25

   * - Key
     - Description
     - Data Type
     - Possible Values
   * - ``SensorType``
     - Type of sensors used for the respiratory measurements
     - Text
     - Bellows, Cushion, Strain Gauges,…
   * - ``Placement``
     - Placement of the respiratory measurement device
     - Text
     - Chest



Example TSV Data File
---------------------

Compressed ``*.tsv.gz`` files are headerless. The columns are defined by the JSON sidecar.

.. code-block:: text
  
    0.0	0.0347900390625
    0.0004999999999881766	0.03509521484375
    0.0009999999999763531	0.0347900390625
    . . .

In this example, the sidecar ``Columns`` value is ``["timestamp", "resp"]``.

Example JSON Sidecar
--------------------

.. code-block:: json

    {
        "Columns": [
            "timestamp",
            "resp"
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
        "resp": {
            "Description": "Respiratory Recording",
            "SensorType": "Belt",
            "Placement": "Chest",
            "Units": "V"
        },
        "SamplingFrequency": 2000.0,
        "TrimPoints": [
            882.7075,
            1530.7065
        ],
        "Duration": 647.999
    }

