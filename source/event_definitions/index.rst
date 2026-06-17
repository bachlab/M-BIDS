Event Definitions
=================

Task events are saved as ``events.tsv`` and ``events.json`` files (see the `BIDS Events specification <https://bids-specification.readthedocs.io/en/stable/modality-agnostic-files/events.html>`_).

In addition to the event definitions provided in the BIDS specification, M-BIDS requires event labels to be stored in an ``event_type`` column. The exact allowed event labels depend on the experiment type or benchmark challenge. For Calibench fear-conditioning datasets, these labels and the accompanying event columns are part of the importer contract and must be written exactly as documented.

Expected file location
----------------------

Fear-conditioning event files should be stored together with the corresponding task recording files. The target folder depends on the available physiological modalities.

.. csv-table:: Table 1: Event file location by modality
   :header: "Available data", "Target folder", "Reason"
   :widths: 25, 20, 55

   "Eye-tracking only", "``beh/``", "Eye-tracking-only datasets can store task events and eye recordings in the behavioral folder."
   "SCR only", "``physio/``", "Skin conductance recordings are physiological recordings and should be stored in the physiology folder."
   "Eye-tracking and SCR", "``physio/``", "When physiological recordings are present together, the task recordings and corresponding events are stored in the physiology folder."

For Calibench BEP020/BEP045 datasets, physiology and eye-tracking recordings are stored together in ``physio/``. The structure for one subject and task should look like this:

.. code-block:: text

    sub-<participant_label>/
    └── physio/
        ├── sub-<participant_label>_task-acquisition_events.json
        ├── sub-<participant_label>_task-acquisition_events.tsv
        ├── sub-<participant_label>_task-acquisition_recording-scr_physio.json
        ├── sub-<participant_label>_task-acquisition_recording-scr_physio.tsv.gz
        ├── sub-<participant_label>_task-acquisition_recording-ecg_physio.json
        ├── sub-<participant_label>_task-acquisition_recording-ecg_physio.tsv.gz
        ├── sub-<participant_label>_task-acquisition_recording-resp_physio.json
        ├── sub-<participant_label>_task-acquisition_recording-resp_physio.tsv.gz
        ├── sub-<participant_label>_task-acquisition_recording-eye2_physio.json
        ├── sub-<participant_label>_task-acquisition_recording-eye2_physio.tsv.gz
        ├── sub-<participant_label>_task-acquisition_recording-eye2_physioevents.json
        └── sub-<participant_label>_task-acquisition_recording-eye2_physioevents.tsv.gz

The same pattern is used for ``task-extinction``. A subject may contain only the modalities that were actually recorded, but every included recording must have a matching JSON sidecar.

For an SCR-only fear-conditioning dataset, the structure may look like this:

.. code-block:: text

    sub-<sub_id>/
    └── physio/
        ├── sub-<sub_id>_task-acquisition_events.json
        ├── sub-<sub_id>_task-acquisition_events.tsv
        ├── sub-<sub_id>_task-acquisition_recording-scr_physio.json
        └── sub-<sub_id>_task-acquisition_recording-scr_physio.tsv.gz

If both eye-tracking and physiological recordings are present, the files should be placed under ``physio/``. This placement follows the modality handling described by BEP020 and BEP045 and is supported by the BIDS importer.

Required M-BIDS columns
-----------------------

BIDS task events already define ``onset`` and ``duration`` columns. In addition to these BIDS columns, Calibench fear-conditioning ``events.tsv`` files MUST contain the following M-BIDS columns:

.. csv-table:: Table 2: Required additional ``events.tsv`` columns
   :header: "Column", "Description", "Data Type", "Example"
   :widths: 20, 45, 15, 20

   "``event_type``", "Type of event, expressed as a character string. The allowed values depend on the experiment type.", "String", "``CSpr``, ``CSpu``, ``CSm``, ``USp``"
   "``task_name``", "Experimental phase represented by the row.", "String", "``habituation``, ``acquisition``, ``extinction``"

Optional columns
----------------

Additional columns may be included when available or required by a specific dataset, experiment, or benchmark challenge. They must not replace or rename the BIDS columns or required M-BIDS columns listed above.

.. csv-table:: Table 3: Optional event columns
   :header: "Column", "Description", "Data Type", "Example"
   :widths: 20, 45, 15, 20

   "``stimulus_name``", "Name or identifier of the presented stimulus.", "String", "``square``, ``diamond``, ``shock``"
   "``HED``", "Hierarchical Event Descriptor tags describing the event.", "String", "``Sensory-event,Visual-presentation``"
   "``response``", "Participant response, when responses are part of the task.", "String", "``left``, ``right``, ``n/a``"
   "``response_time``", "Time between stimulus onset and participant response.", "Number", "``1.23``"

Specific event types
--------------------

The following generic event types may be used to describe common experimental events.

.. csv-table:: Table 4: Generic event types
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
