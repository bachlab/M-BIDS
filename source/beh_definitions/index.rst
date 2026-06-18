Behavioral And Phenotype Definitions
====================================

Calibench fear-conditioning datasets extend BIDS participant and phenotype metadata rules. Behavioral and participant-level metadata are stored at the dataset level using ``participants.tsv`` / ``participants.json`` (see the `BIDS participants file specification <https://bids-specification.readthedocs.io/en/stable/modality-agnostic-files/data-summary-files.html#participants-file>`_) and, when available, files in ``phenotype/`` (see the `BIDS phenotypic and assessment data specification <https://bids-specification.readthedocs.io/en/stable/modality-agnostic-files/phenotypic-and-assessment-data.html>`_).

Task events and physiological recordings are stored in ``physio/`` as documented in the event and physiology pages.

Participant metadata
--------------------

BIDS requires ``participant_id`` and allows participant descriptors such as ``age``, ``sex``, and ``handedness``. For Calibench datasets, the top-level ``participants.tsv`` file MUST contain one row per participant and the following columns:

.. csv-table:: Table 1: Required participant columns
   :header: "Column", "Description", "Example"
   :widths: 25, 55, 20

   "``participant_id``", "Participant label used in the dataset.", "``sub-<participant_label>``"
   "``age``", "Participant age in years.", "``23``"
   "``sex``", "Self-reported biological sex.", "``F``"
   "``handedness``", "Participant handedness.", "``left``"

The matching ``participants.json`` sidecar MUST document every column present in ``participants.tsv``. Column names in the TSV and JSON must match exactly.

Recommended levels:

.. csv-table:: Table 2: Recommended participant levels
   :header: "Column", "Allowed values"
   :widths: 30, 70

   "``sex``", "``M``, ``F``, ``O``, ``n/a``"
   "``handedness``", "``left``, ``right``, ``ambidextrous``, ``n/a``"

Phenotype metadata
------------------

BIDS stores participant-level questionnaire and assessment data in ``phenotype/``. For Calibench datasets, each phenotype TSV file MUST have a matching JSON sidecar with the same basename.

.. code-block:: text

    phenotype/
    ├── participant_info.tsv
    ├── participant_info.json
    ├── PreAcquisitionRatings.tsv
    ├── PreAcquisitionRatings.json
    ├── PostAcquisitionRatings.tsv
    ├── PostAcquisitionRatings.json
    ├── PostExtinctionRatings.tsv
    └── PostExtinctionRatings.json

Every phenotype TSV file MUST use ``participant_id`` as the first column. Every remaining TSV column MUST be documented by an exactly matching key in the JSON sidecar. The sidecar SHOULD include ``MeasurementToolMetadata`` with a short description and source URL when available.

Calibench phenotype files use these naming patterns:

.. csv-table:: Table 3: Phenotype files and column patterns
   :header: "File", "Required columns"
   :widths: 35, 65

   "``participant_info.tsv``", "``participant_id``, ``recorded_at``, ``room_temperature``, ``humidity``, ``age``, ``sex``, ``handedness``"
   "``PreAcquisitionRatings.tsv``", "``participant_id``, ``pre_acq_1`` through ``pre_acq_6``"
   "``PostAcquisitionRatings.tsv``", "``participant_id``, ``post_acq_1`` through ``post_acq_6``"
   "``PostExtinctionRatings.tsv``", "``participant_id``, ``post_ext_1`` through ``post_ext_8``"
   "``bfi60_german.tsv``", "``participant_id``, ``bfi60_1`` through ``bfi60_60``"
   "``gad7_german.tsv``", "``participant_id``, ``gad7_1`` through ``gad7_7``"
   "``ius18_german.tsv``", "``participant_id``, ``ius18_1`` through ``ius18_18``"
   "``phq9_german.tsv``", "``participant_id``, ``phq9_1`` through ``phq9_9``"
   "``soc12_german.tsv``", "``participant_id``, ``soc12_1`` through ``soc12_12``"
   "``stai20_german.tsv``", "``participant_id``, ``stai20_1`` through ``stai20_20``"

Stimulus presentation metadata
------------------------------

The BIDS Events specification defines ``StimulusPresentation`` metadata for visual stimuli and eye-tracking. For visual-stimulus or eye-tracking Calibench datasets, stimulus presentation metadata MUST be available in the task sidecar. These fields are stored in the corresponding ``*_events.json`` file under ``StimulusPresentation``.

.. note::

   All physical distance and size measurements in ``StimulusPresentation`` MUST be reported in millimeters. This applies to fields such as ``ScreenDistance`` and ``ScreenSize``.

.. csv-table:: Table 4: Required stimulus presentation fields
   :header: "Key", "Description", "Example"
   :widths: 35, 45, 20

   "``StimulusPresentation.ScreenDistance``", "Distance between participant and screen in millimeters.", "``500``"
   "``StimulusPresentation.ScreenOrigin``", "Origin of the screen coordinate system.", "``top, left``"
   "``StimulusPresentation.ScreenRefreshRate``", "Refresh rate of the screen in Hertz.", "``56``"
   "``StimulusPresentation.ScreenResolution``", "Screen resolution in pixels.", "``[1920, 1080]``"
   "``StimulusPresentation.ScreenSize``", "Physical screen size in millimeters.", "``[476.0, 268.0]``"

Example ``StimulusPresentation`` object:

.. code-block:: json

    {
        "StimulusPresentation": {
            "ScreenDistance": 500,
            "ScreenOrigin": [
                "top",
                "left"
            ],
            "ScreenRefreshRate": 56,
            "ScreenResolution": [
                1920,
                1080
            ],
            "ScreenSize": [
                476.0,
                268.0
            ]
        }
    }
