Eyetracking (eye)
=================

Following the `BIDS Physiological recordings specification <https://bids-specification.readthedocs.io/en/stable/modality-specific-files/physiological-recordings.html>`_, including its `eye-tracking section <https://bids-specification.readthedocs.io/en/stable/modality-specific-files/physiological-recordings.html#eye-tracking>`_, M-BIDS uses the following additional Calibench requirements for eyetracking data.

BIDS recommends ``eye1``, ``eye2``, and ``eye3`` recording labels for eye-tracking. For Calibench automated processing, ``recording-eye1`` MUST correspond to the left eye and ``recording-eye2`` MUST correspond to the right eye. If only one eye was recorded or exported, include only the matching recording label and set ``RecordedEye`` accordingly.

When eye-tracking data are aligned with physiological recordings, the files are stored in ``physio/``:

.. code-block:: text

    physio/
    ├── sub-<participant_label>_task-acquisition_recording-eye2_physio.json
    ├── sub-<participant_label>_task-acquisition_recording-eye2_physio.tsv.gz
    ├── sub-<participant_label>_task-acquisition_recording-eye2_physioevents.json
    └── sub-<participant_label>_task-acquisition_recording-eye2_physioevents.tsv.gz

Eye-tracking physiological data
-------------------------------

**TSV file:** ``<matches>_recording-eye2_physio.tsv.gz``

Compressed ``*.tsv.gz`` files are headerless. The columns are defined by the JSON sidecar and MUST be ordered as follows:

.. csv-table:: Table 1: Required eye-tracking physiology columns
   :header: "Position", "Column", "Description"
   :widths: 15, 25, 60

   "1", "``timestamp``", "Time in seconds relative to the start of the exported recording."
   "2", "``x_coordinate``", "Horizontal gaze position for the recorded eye."
   "3", "``y_coordinate``", "Vertical gaze position for the recorded eye."
   "4", "``pupil_size``", "Pupil diameter."

.. code-block:: text

    0.0	240.70229166666667	169.03851851851852	2.1484500285714287
    0.0005000000000006111	240.28083333333336	168.76555555555555	2.151583707142857
    0.0009999999999994458	240.0329166666667	168.4925925925926	2.1534639142857146


**JSON sidecar:** ``<matches>_recording-eye2_physio.json``

Example of JSON sidecar: 

.. code-block:: json
    
    {
        "Description": "Converts EyeLink pupil AREA units to estimated pupil diameter in mm using PsPM-style calibration.",
        "Columns": [
            "timestamp",
            "x_coordinate",
            "y_coordinate",
            "pupil_size"
        ],
        "PhysioType": "eyetrack",
        "StartTime": 0.0,
        "SampleCoordinateSystem": "gaze-on-screen",
        "timestamp": {
            "LongName": "Time",
            "Description": "a continuously increasing identifier of the sampling time registered by the device",
            "Origin": "System startup",
            "Units": "s"
        },
        "x_coordinate": {
            "LongName": "Gaze position (x)",
            "Description": "Gaze position x-coordinate of the recorded eye",
            "Units": "mm"
        },
        "y_coordinate": {
            "LongName": "Gaze position (y)",
            "Description": "Gaze position y-coordinate of the recorded eye",
            "Units": "mm"
        },
        "pupil_size": {
            "Description": "Pupil diameter",
            "Units": "mm"
        },
        "RecordedEye": "right",
        "Manufacturer": "SR-Research",
        "ManufacturersModelName": "EyeLink 1000",
        "SoftwareVersions": "EyeLink 1000 Plus 5.15",
        "GazeRange": {
            "xmin": 0,
            "ymin": 0,
            "xmax": 476.0,
            "ymax": 268.0
        },
        "PupilFitMethod": "ELLIPSE",
        "MeasurementType": "DIAMETER",
        "SamplingFrequency": 2000,
        "TrimPoints": [
            14.395999999999958,
            654.015
        ],
        "Duration": 639.619
    }


Eye-tracking physioevents
-------------------------

The eye-tracking ``physioevents`` file contains events detected by the eye-tracker or derived from the eye-tracking time series. These files are separate from task ``events.tsv`` files.

**Files:**

* ``<matches>_recording-eye2_physioevents.tsv.gz``
* ``<matches>_recording-eye2_physioevents.json``

Compressed ``*.tsv.gz`` files are headerless. The columns are defined by the JSON sidecar and MUST be ordered as follows:

.. csv-table:: Table 2: Required eye-tracking physioevents columns
   :header: "Position", "Column", "Description"
   :widths: 15, 25, 60

   "1", "``onset``", "Event onset in seconds relative to the start of the exported eye recording."
   "2", "``duration``", "Event duration in seconds."
   "3", "``trial_type``", "Eye event type. Allowed values are ``fixation``, ``saccade``, ``blink``, and ``n/a``."
   "4", "``blink``", "Blink status. Use ``1.0`` for closed eye, ``0.0`` for open eye, and ``n/a`` when not applicable."
   "5", "``message``", "String messages logged by the eye-tracker, or ``n/a``."

.. code-block:: text

    0.09249999999999936	0.0120000000000004	saccade	0.0	n/a
    0.16900000000000048	0.2959999999999994	blink	1.0	n/a
    0.5240000000000009	0.0114999999999998	saccade	0.0	n/a

Example ``physioevents`` sidecar:

.. code-block:: json

    {
        "Columns": [
            "onset",
            "duration",
            "trial_type",
            "blink",
            "message"
        ],
        "Description": "Messages logged by the measurement device",
        "OnsetSource": "timestamp",
        "trial_type": {
            "Description": "Event type as identified by the eye-tracker's model.",
            "Levels": {
                "fixation": "Indicates a fixation.",
                "saccade": "Indicates a saccade.",
                "blink": "Indicates a blink.",
                "n/a": "Not applicable."
            }
        },
        "blink": {
            "Description": "Gives status of the eye.",
            "Levels": {
                "0": "Indicates if the eye was open.",
                "1": "Indicates if the eye was closed."
            }
        },
        "message": {
            "Description": "String messages logged by the eye-tracker."
        },
        "StartTime": 0.0,
        "SaccadeDetectionAlgorithm": "velocity threshold",
        "BlinkDetectionAlgorithm": "pupil threshold",
        "SourceDataframeColumns": [
            "timestamp",
            "x_coordinate",
            "y_coordinate",
            "pupil_size"
        ],
        "TrimPoints": [
            14.395999999999958,
            654.015
        ],
        "Duration": 639.619
    }

