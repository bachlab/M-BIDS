Event Definitions
=================

Task events for behavioral experiments are saved as ``events.tsv`` and ``events.json`` files (see `BIDS Specification/Task Events <https://bids-specification.readthedocs.io/en/stable/modality-specific-files/task-events.html>`_).

In addition to the event definitions provided in the BIDS specification, M-BIDS requires event labels to be stored in an ``event_type`` column. The exact allowed event labels depend on the experiment type or benchmark challenge.

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