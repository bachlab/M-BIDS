Respiration (resp)
=================

Following the guidelines from 
`BIDS v1.10.0 <https://bids-specification.readthedocs.io/en/stable/modality-specific-files/physiological-recordings.html>`_, 
we propose the following **additional requirements** for respiratory data.

Modality specific data SHOULD be split into modality specific files carrying the modality-label. Modality label for skin conductance is ``resp`` and resp specific data files would be organized as follows

.. code-block:: text

    physio/
    ├─ sub-01_ses-1_task-TaskName_recording-ecg_physio.json 
    ├─ sub-01_ses-1_task-TaskName_recording-resp_physio.tsv.gz


Column names in the ``resp`` data files MUST be ``resp`` for experiments involving single recordings, or ``resp1``, ``resp2``, ``resp3``, ... for experiments involving different types of respiratory measurements like chest volume, abdominal volume, pressure, etc.


These fields **MUST** be included in the JSON sidecar file:  
``<matches>_recording-resp_physio.json``


Additional Metadata Fields
--------------------------

.. list-table:: Table 1: Required SCR-Specific JSON Fields
   :header-rows: 1
   :widths: 25 45 15 25

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



Example Data
------------

Example values from the corresponding TSV file:

.. code-block:: text

    0.903930664062500
    0.901794433593750
    0.901184082031250
    0.899353027343750
    0.898132324218750
    0.896911621093750
    0.895080566406250
    . . .


Example JSON Sidecar
--------------------

.. code-block:: json

    {
        "Columns": [
    		"resp",
        ],
        "Manufacturer": "<Manufacturer-Name>",
        "ManufacturersModelName": "<Manufacturer-Model-Name>",
        "DeviceSerialNumber": "<Device-Serial-Number>",
        "SamplingFrequency": 2000,
        "SoftwareVersion": "<Software-version>",
        "StartTime": 0,
        "PhysioType": "specified",
        "resp": {
                "Description": "Respiratory Recording",
            "SensorType": "Belt",
            "Plaecement": "Chest",
            "Units": "Volts"
        }

    }

