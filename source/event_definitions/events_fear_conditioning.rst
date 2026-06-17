Event definitions for Fear Conditioning experiments
===================================================

Fear conditioning experiments involve **conditioned stimuli (CS)** and **unconditioned stimuli (US)**. This page extends the `BIDS Events specification <https://bids-specification.readthedocs.io/en/stable/modality-agnostic-files/events.html>`_ with the stricter event labels required by the Calibench Fear Conditioning challenge.

In the Calibench Fear Conditioning challenge, event labels distinguish between reinforced CS+ trials, unreinforced CS+ trials, CS- trials, delivered US events, omitted US events, and CS- matched US timepoints.

The ``events.tsv`` file **MUST** use the event labels defined below. These labels are part of the benchmark contract and are used by currently linked methods and importers.

Event labels
------------

.. csv-table:: Table 1: Fear Conditioning event labels
   :header: "Stimulus", "Reinforced?", "Naming", "Description"
   :widths: 15, 15, 15, 55

   "``CS+``", "yes", "``CSpr``", "A reinforced conditioned trial."
   "``CS+``", "no", "``CSpu``", "An unreinforced conditioned trial."
   "``CS-``", "no", "``CSm``", "The non-conditioned stimulus."
   "``US``", "-", "``USp``", "The event in which an unconditioned stimulus, or threat, was present."
   "``US``", "-", "``USo``", "The timepoint where the US would have appeared in an unreinforced CS+ trial."
   "``US``", "-", "``USm``", "The event where the US would have appeared in CS- trials, helping avoid bias in the comparison."

Required M-BIDS columns
-----------------------

BIDS task events already define ``onset`` and ``duration``. In addition to these BIDS columns, Calibench fear-conditioning ``events.tsv`` files MUST contain the following M-BIDS columns:

.. csv-table:: Table 2: Required additional ``events.tsv`` columns
   :header: "Column", "Description", "Example"
   :widths: 20, 60, 20

   "``event_type``", "Fear Conditioning event label. The value must be one of ``CSpr``, ``CSpu``, ``CSm``, ``USp``, ``USo``, or ``USm``.", "``CSpr``"
   "``task_name``", "Experimental phase represented by the row. Acquisition files can contain ``habituation`` and ``acquisition`` rows; extinction files contain ``extinction`` rows.", "``acquisition``"

Do not rename these columns. Additional columns may be included when available, but the importer expects the required columns and event labels listed here.

Optional columns
----------------

Calibench datasets may include the following optional columns. They are useful for interpretation and richer metadata, but they are not required by the Calibench fear-conditioning importer.

.. csv-table:: Table 3: Optional ``events.tsv`` columns
   :header: "Column", "Description", "Example"
   :widths: 20, 60, 20

   "``stimulus_name``", "Stimulus identifier. If present, use values documented in the sidecar levels.", "``square``, ``diamond``, ``shock``"
   "``HED``", "Hierarchical Event Descriptor tags for the event.", "``Sensory-event,Visual-presentation``"

Task entities and phases
------------------------

Calibench fear-conditioning files use the BIDS task entities ``task-acquisition`` and ``task-extinction``.

``task-acquisition`` files may include rows whose ``task_name`` is ``habituation`` before the acquisition trials. ``task-extinction`` files use ``task_name`` value ``extinction``.

When ``stimulus_name`` is present, use dataset-specific values documented in the event sidecar. Common Calibench values include:

.. csv-table:: Table 4: Stimulus names
   :header: "Value", "Description"
   :widths: 25, 75

   "``square``", "Geometric CS+ stimulus."
   "``diamond``", "Geometric CS- stimulus."
   "``shock``", "Electrical unconditioned stimulus."

Example ``events.tsv``
----------------------

An example ``task-acquisition`` ``events.tsv`` file with optional ``stimulus_name`` and ``HED`` columns looks like this:

.. code-block:: text

    onset	duration	event_type	stimulus_name	HED	task_name
    10.0	8.0	CSpu	square	Sensory-event,Visual-presentation,Experimental-condition/CS-plus,Experimental-condition/Unreinforced	habituation
    17.5	0.0	USo	square	Experimental-condition/CS-plus,Experimental-condition/Unreinforced,Experimental-condition/Expectation-violation	habituation
    41.5	8.0	CSm	diamond	Sensory-event,Visual-presentation,Experimental-condition/CS-minus	habituation
    49.0	0.0	USm	diamond	Experimental-condition/CS-minus,Experimental-condition/Expectation-violation,Somatosensory-stimulation	habituation
    134.4995	8.0	CSpr	square	Sensory-event,Visual-presentation,Experimental-condition/CS-plus,Experimental-condition/Reinforced	acquisition
    141.99950000000013	0.4253501000348478	USp	shock	Sensory-event,Somatosensory-stimulation,Aversive-stimulus	acquisition

Interpretation notes
--------------------

``CSpr`` and ``CSpu`` both refer to CS+ trials, but they distinguish whether the trial was reinforced or unreinforced.

``USp`` marks a delivered unconditioned stimulus.

``USo`` marks the omitted US timepoint in an unreinforced CS+ trial.

``USm`` marks the matched timepoint where a US would have appeared during a CS- trial. This allows methods to compare responses at equivalent timepoints and helps avoid bias in the benchmark comparison.
