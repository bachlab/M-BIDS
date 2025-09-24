Behavioral Experiment Definitions
=================

Metadata information and experimental setup information for behavioral experiments is saved in  ``beh.json`` files (see `BIDS Specification/Behavioral experiments (with no neural recordings) <https://bids-specification.readthedocs.io/en/stable/modality-specific-files/behavioral-experiments.html>`_). 

In addition to the fields mentioned the existing BIDS specification, in case of experiments involving eyetracking or visual stimulus, the following fields are REQUIRED:

.. list-table:: Table 1: Required StimulusPresentation Information
   :header-rows: 1
   :widths: 25 25 25 25

   * - Key
     - Description
     - Data Type
     - Example Values
   * - ``StimulusPresentation.ScreenDistance``
     - Distance between the participant's eye and the screen (in meters).
     - Number
     - e.g., 0.7
   * - ``StimulusPresentation.ScreenOrigin``
     - Location of the spatial coordinates' origin for the visual stimuli presentation.
     - Text list
     - ``["top","left"]``, ``["center","center"]``, etc.
   * - ``StimulusPresentation.ScreenRefreshRate``
     - Refresh rate of the screen (in Hertz)
     - Number
     - ``60``
   * - ``StimulusPresentation.ScreenResolution``
     - Resolution of the screen (in pixels)
     - Number list
     - ``["1024","768"]``,
   * - ``StimulusPresentation.ScreenSize``
     - Size of the screen (in meters)
     - Number list
     - ``["0.312","0.226"]`` 


Example of ``_beh.json`` sidecar: 

.. code-block:: text
  
  {
  "Columns": [
      "pupil_size",
      "x_coordinate",
      "y_coordinate"
  ],
  "Manufacturer": "SR-Research",
  "ManufacturersModelName": "EYELINK II CL v4.56 Aug 18 2010",
  "TaskName": "Delay Fear Conditioning",
  "TaskDescription": "Participants are presented with a series of images(CS). Some images(CSp) are followed by an aversive unconditioned stimulus (USp) while others(CSm) are not(USm).",
  "CogAtlasID": "https://www.cognitiveatlas.org/task/id/trm_5023ef8eab626/",
  "CogPOID": "http://wiki.cogpo.org/index.php?title=Classical_Conditioning_Paradigm",
  "SOA": 3.5,
  "StimulusPresentation": {
    "ScreenDistance": 700,
    "ScreenOrigin": [
      "top",
      "left"
    ],
    "ScreenRefreshRate": 60,
    "ScreenResolution": [
      1024,
      768
    ],
    "ScreenSize": [
      312.42,
      226.89
    ]
  }