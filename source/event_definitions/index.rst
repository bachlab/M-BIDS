Event Definitions
=================

Task events for behavioral experiments are saved as ``events.tsv`` and ``events.json`` files (see `BIDS Specification/Task Events <https://bids-specification.readthedocs.io/en/stable/modality-specific-files/task-events.html>`_).

In addition to the event definitions provided in the BIDS specification, M-BIDS requires event labels to be stored in an ``event_type`` column. The exact allowed event labels depend on the experiment type or benchmark challenge.

Expected file location
----------------------

Fear-conditioning event files should be stored together with the corresponding task recording files. The target folder depends on the available physiological modalities.

.. csv-table:: Table 1: Event file location by modality
   :header: "Available data", "Target folder", "Reason"
   :widths: 25, 20, 55

   "Eye-tracking only", "``beh/``", "Eye-tracking-only datasets can store task events and eye recordings in the behavioral folder."
   "SCR only", "``physio/``", "Skin conductance recordings are physiological recordings and should be stored in the physiology folder."
   "Eye-tracking and SCR", "``physio/``", "When physiological recordings are present together, the task recordings and corresponding events are stored in the physiology folder."

For an eye-tracking-only fear-conditioning dataset, the structure may look like this:

.. code-block:: text

    sub-01/
    └── ses-01/
        └── beh/
            ├── sub-01_ses-01_task-fearconditioning_events.json
            ├── sub-01_ses-01_task-fearconditioning_events.tsv
            ├── sub-01_ses-01_task-fearconditioning_recording-eye1_physio.json
            ├── sub-01_ses-01_task-fearconditioning_recording-eye1_physio.tsv.gz
            ├── sub-01_ses-01_task-fearconditioning_recording-eye2_physio.json
            └── sub-01_ses-01_task-fearconditioning_recording-eye2_physio.tsv.gz

For an SCR-only fear-conditioning dataset, the structure may look like this:

.. code-block:: text

    sub-<sub_id>/
    └── physio/
        ├── sub-<sub_id>_task-acquisition_events.json
        ├── sub-<sub_id>_task-acquisition_events.tsv
        ├── sub-<sub_id>_task-acquisition_recording-scr_physio.json
        └── sub-<sub_id>_task-acquisition_recording-scr_physio.tsv.gz

If both eye-tracking and SCR recordings are present, the files should be placed under ``physio/``. This placement follows the modality handling described by BEP020 and BEP045 and is supported by the BIDS importer.

Required columns
----------------

.. csv-table:: Table 1: Required additional columns in event definitions
   :header: "Column", "Description", "Data Type", "Example"
   :widths: 20, 45, 15, 20

   "``event_type``", "Type of event, expressed as a character string. The allowed values depend on the experiment type.", "String", "``CSpr``, ``CSpu``, ``CSm``, ``USp``"

Optional columns
----------------

Additional columns may be included when available or required by a specific dataset, experiment, or benchmark challenge.

.. csv-table:: Table 2: Optional event columns
   :header: "Column", "Description", "Data Type", "Example"
   :widths: 20, 45, 15, 20

   "``stimulus_name``", "Name or identifier of the presented stimulus.", "String", "``picture_01``, ``shock``, ``n/a``"
   "``HED``", "Hierarchical Event Descriptor tags describing the event.", "String", "``Sensory-event``"

Specific event types
--------------------

The following generic event types may be used to describe common experimental events.

.. csv-table:: Table 3: Generic event types
   :header: "Event Type", "Description"
   :widths: 30, 70

   "``block_start``", "Start of an experimental block."
   "``block_end``", "End of an experimental block."
   "``response``", "Generic participant response to stimuli."

Specific guidelines are different for different experiment types and are listed below:

.. toctree::
   :maxdepth: 1
   :caption: Events:

   events_fear_conditioning