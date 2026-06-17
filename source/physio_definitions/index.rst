Physiology Data Definitions
===========================

M-BIDS extends the `BIDS Physiological recordings specification <https://bids-specification.readthedocs.io/en/stable/modality-specific-files/physiological-recordings.html>`_ with stricter Calibench naming and metadata rules. Each physiological modality SHOULD be stored in a separate modality-specific file with a matching JSON sidecar.

As in BIDS, compressed ``*_physio.tsv.gz`` files MUST NOT include a header row. The column names MUST be provided by the ``Columns`` list in the matching ``*_physio.json`` sidecar.

All Calibench physiology time-series files use ``timestamp`` as the first column. The timestamp column is a continuously increasing time value in seconds, relative to the start of the trimmed recording.

General file pattern
--------------------

.. code-block:: text

    sub-<participant_label>/
    └── physio/
        ├── sub-<participant_label>_task-acquisition_recording-scr_physio.json
        ├── sub-<participant_label>_task-acquisition_recording-scr_physio.tsv.gz
        ├── sub-<participant_label>_task-acquisition_recording-ecg_physio.json
        ├── sub-<participant_label>_task-acquisition_recording-ecg_physio.tsv.gz
        ├── sub-<participant_label>_task-acquisition_recording-resp_physio.json
        └── sub-<participant_label>_task-acquisition_recording-resp_physio.tsv.gz

The same pattern is used for ``task-extinction``. Eye-tracking recordings are also stored in ``physio/`` when they are aligned with physiological recordings.

Common sidecar fields
---------------------

BIDS defines common physiology sidecar fields such as ``Columns``, ``StartTime``, and ``SamplingFrequency``. In addition to these BIDS fields, every Calibench ``*_physio.json`` sidecar MUST contain the following fields when applicable:

.. csv-table:: Table 1: Common physiology sidecar fields
   :header: "Key", "Description", "Example"
   :widths: 25, 55, 20

   "``Columns``", "Column names for the matching headerless TSV file. The first entry must be ``timestamp``.", "``timestamp, scr``"
   "``StartTime``", "Time of the first sample relative to the recording start.", "``0.0``"
   "``SamplingFrequency``", "Sampling frequency in Hz.", "``2000``"
   "``PhysioType``", "Recording type used by the importer.", "``generic``"
   "``TrimPoints``", "Source-data time points used to trim the exported recording.", "``[882.7075, 1530.7065]``"
   "``Duration``", "Duration of the exported recording in seconds.", "``647.999``"
   "``timestamp``", "Metadata object describing the timestamp column.", "``Units: s``"

Modality-specific definitions
-----------------------------

Guidelines for individual modalities are given below.

.. toctree::
   :maxdepth: 1
   :caption: Physio Data Modalities:

   skin_conductance
   electrocardiogram
   respiration
   eyetracking
