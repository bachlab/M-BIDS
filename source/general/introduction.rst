What is M-BIDS
======================
M-BIDS is a data standardization philosophy built on top of the `BIDS specification <https://bids-specification.readthedocs.io/en/stable/>`_. It introduces stricter guidelines tailored to individual experiment types.

Experimental data analysis often requires key metadata. While BIDS provides ways to store such metadata, its flexibility leads to variability. This variability creates friction when developing automated analysis pipelines.

M-BIDS (Machine-interpretable BIDS) addresses this by ensuring data is not only machine-readable, as BIDS intended, but also machine-interpretable.

For Calibench datasets, M-BIDS is intentionally stricter than regular BIDS. Event labels, column names, file locations, task labels, and sidecar fields must be written exactly as documented so automated importers can populate benchmark fields without guessing.

The current Calibench fear-conditioning layout follows BIDS 1.1.0 with BEP020 and BEP045-style organization. These extensions follow the `BIDS Extension Proposal mechanism <https://bids-specification.readthedocs.io/en/stable/extensions.html>`_. Task events, physiology, eye-tracking recordings, and eye-tracking physioevents are stored together when they are aligned for analysis. The documentation pages below define the exact column names and sidecar fields expected by the importer.
