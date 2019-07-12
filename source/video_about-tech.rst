About Mobius Vision Video SDK
======================================

A video can be seen as a sequence of images, which are called frames. Video content is typically recorded at 24 to 60 frames per second (fps), and typically is much larger than an image. For this reason, it makes most sense to process video content on-premise, rather than a cloud-based API, which would incur serious delays in the video processing pipeline. In some cases, such as for real-time applications, cloud-based solutions are even prohibitive.

|mobvis_video| is shipped with a number of modules, which are briefly described in the following; more details as well as sample commands can be found in the dedicated sections. 


Video Shot Detection
---------------------

An important concept in videos is the one of 'shots'. While there are several definitions of what a shot is, for our intents and purposes, we define a shot as a sequence of frames where the semantics (that is, the content) only changes slowly. In order to perform a meaningful analysis of a video, it is highly beneficial to identify so-called 'video shot boundaries', or 'shot boundaries' for short. 

The figure below further illustrates the concept of 'shot boundaries', on the example of a short video that has been created from three separate 'clips'. Note that each clip is a video that has been recorded at one go, without turning the camera off. As one can see, while there are only *three clips* (from three separate recordings) in the video, there are actually *five shots* detected. This is because the concent of the scene (and hence the concepts) change over time, even within a clip. In the first clip of the illustration, for example, the camera pans from a close-up of the flowers to the landscape shot of the mountain range with the river, which causes a 'shot' change.


.. image::
   data/shots_viz.png
   :align: center
   
   
The |mobvis_video| features a highly efficient shot boundary detector. With the shots identified, the SDK offers a shot-level keywording module, as well as an action detection module. 

.. note::
    
    If the shot boundary selection is switched off, the video will be segmented using *fixed* temporal segments (e.g., 3 seconds).


Video Tagging
----------------

|mobvis_video| offers both a |lightweight_model| and a |performance_model| keywording model, which can identify over 5000 concepts, emotions, and actions. The |lightweight_model| model is computationally very efficient, but slightly less accurate than the performance one. As such, it is recommended in cases where speed matters, such as real-time applications. The |performance_model| model runs around 10 times slower, but offers the highest quality keywording results.

Since content can change quite drastically within a video, we offer both 'segment-level' as well as 'video-level' keywording. As the names suggest, segment-level keywording finds keywords for each individual segment, whereas video-level keywording provides keywords that are representative of the whole video. The figure above illustrates these concepts.


Highlights Detection
----------------------------

The highlighting feature allows to obtain 'highlight scores' for video frames, which allows to identify the most important/interesting parts of a video. This can be very useful for example in order to create a summary of a video that can be shown if someone is browsing through a video database.




Advantages of on-premise installation compared to API service
---------------------------------------------------------------
This set-up has several advantages over a (cloud-based) API service, including:

* Data privacy by design: the data always stays on your system
* Security as control over the data flow is kept
* Considerably faster, since the videos do not have to be sent to a server to be analyzed. This is particularly important for real-time applications.
