.. image::
  data/green_Mobius_Vision_Logotype.png
  :align: left

About Mobius Vision SDK
==========================

AI powered Computer Vision that lives on the Edge
--------------------------------------------------

Empower your product with our pre-trained models and customize the models according to the use case.
This Computer Vision technology is engineered to work on GPUs with a Linux operating system.
We believe that privacy matters even in the 21st century, and therefore all processing happens on the device locally, and not somewhere on cloud servers.

Mobius Vision SDK is broadly split into |mobvis_image| and |mobvis_video|.

|mobvis_image| currently contains the following modules:

* Keywording module: Tag images with more than 5000 general keywords
* Aesthetics module: Estimate image aesthetics (based on data from professional curators)
* Customization module: Add custom keywords and/or style allowing everyone to retrain our models to fit to specific needs
* Similarity Search: Find similar looking images by providing a reference image

|mobvis_video| currently contains the following modules:

* Video shot detection module: Identify sequences of frames with the same semantical content
* Keywording module: Tag videos with more than 5000 general keywords, both at video-shot-level as well as at video-level
* Action recognition module: Detect over 100 actions in video shots
* (Coming soon) Video highlighting module: Score the shots of a video to identify the highlights.
* (Coming soon) Video search module: Search for similar videos given a short video query.
