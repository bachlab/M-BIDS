Event definitions for Fear Conditioning experiments
===================================================

Fear conditioning experiments involve **conditioned stimuli (CS)** and **unconditioned stimuli (US)**. In the default Calibench Fear Conditioning challenge, event labels distinguish between reinforced CS+ trials, unreinforced CS+ trials, CS- trials, delivered US events, omitted US events, and CS- matched US timepoints.

The ``events.tsv`` file **MUST** use the event labels defined below. These labels are part of the benchmark contract and are used by currently linked methods.

Event labels
------------

.. csv-table:: Table 1: Fear Conditioning event labels
   :header: "Stimulus", "Reinforced?", "Naming", "Description"
   :widths: 15, 15, 15, 55

   "``CS+``", "yes", "``CSpr``", "A reinforced conditioned trial."
   "``CS+``", "no", "``CSpu``", "An unreinforced conditioned trial."
   "``CS-``", "no", "``CSm``", "The non-conditioned stimulus."
   "``US``", "-", "``USp``", "The event in which an unconditioned stimulus, or threat, was present."
   "``US``", "-", "``USo``", "The event in which an unconditioned stimulus was absent, i.e. US omission in unreinforced CS+ trials."
   "``US``", "-", "``USm``", "The event where the US would have appeared in CS- trials, helping avoid bias in the comparison."

Required columns
----------------

The ``events.tsv`` file must contain the following columns:

.. csv-table:: Table 2: Required ``events.tsv`` columns
   :header: "Column", "Description", "Example"
   :widths: 20, 60, 20

   "``onset``", "Event onset in seconds, relative to the start of the recording.", "``10.0``"
   "``duration``", "Event duration in seconds. For point events such as omitted or expected US timepoints, this can be ``0.0``.", "``8.0``"
   "``event_type``", "Fear Conditioning event label. The value must be one of ``CSpr``, ``CSpu``, ``CSm``, ``USp``, ``USo``, or ``USm``.", "``CSpr``"

Additional columns, such as ``HED`` or ``stimulus_name``, may be included when available. However, for the default Calibench Fear Conditioning challenge, the mandatory event labels are the ones listed in Table 1.

Example ``events.tsv``
----------------------

An example ``events.tsv`` file looks like this:

.. code-block:: text

    onset	duration	event_type
    10.0	8.0	CSpu
    17.5	0.0	USo
    29.0	8.0	CSm
    36.5	0.0	USm
    50.0	8.0	CSm
    57.5	0.0	USm
    68.5	8.0	CSpu
    76.0	0.0	USo
    89.5	8.0	CSpr
    97.0	0.425	USp
    112.5	8.0	CSm

Interpretation notes
--------------------

``CSpr`` and ``CSpu`` both refer to CS+ trials, but they distinguish whether the trial was reinforced or unreinforced.

``USp`` marks a delivered unconditioned stimulus.

``USo`` marks an omitted US in an unreinforced CS+ trial.

``USm`` marks the matched timepoint where a US would have appeared during a CS- trial. This allows methods to compare responses at equivalent timepoints and helps avoid bias in the benchmark comparison.