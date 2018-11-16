About Mobius Vision Video SDK
======================================

A video can be seen as a sequence of images, which are called frames. Video content is typically recorded at 24 to 60 frames per second (fps), and typically is much larger than an image. For this reason, it makes most sense to process video content on-premise, rather than a cloud-based API, which would incur serious delays in the video processing pipeline. In some cases, such as for real-time applications, cloud-based solutions are even prohibitive.

|mobvis_video| is shipped with a video shot detection module, as well as a keywording and action recognition module, which are briefly summarized in the following. 


Video Shot Detection
---------------------

An important concept in videos is the one of 'shots'. While there are several definitions of what a shot is, for our intents and purposes, we define a shot as a sequence of frames where the semantics (that is, the content) only changes slowly. In order to perform a meaningful analysis of a video, it is highly beneficial to identify so-called 'video shot boundaries', or 'shot boundaries' for short. 

The figure below further illustrates the concept of 'shot boundaries', on the example of a short video that has been created from three separate 'clips'. Note that each clip is a video that has been recorded at one go, without turning the camera off. As one can see, while there are only *three clips* in the video, there are actually *five shots* detected. This is because the concent of the scene (and hence the concepts) change over time, even within a clip. In the first clip of the illustration, for example, the camera pans from a close-up of the flowers to the landscape shot of the mountain range with the river, which causes a 'shot' change.


.. image::
   data/shots_viz.png
   :align: center
   
   
The |mobvis_video| features a highly efficient shot boundary detector. With the shots identified, the SDK offers a shot-level keywording module, as well as an action detection module. 

.. note::
    
    If the shot boundary selection is switched off, the video will be segmented using *fixed* temporal segments (e.g., 3 seconds).


Video Tagging
----------------

Video Keywording (Static Concepts and Emotions)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

|mobvis_video| offers both a |lightweight_model| and a |performance_model| keywording model, which can identify over 5000 concepts and emotions. The |lightweight_model| model is computationally very efficient, but slightly less accurate than the performance one. As such, it is recommended in cases where speed matters, such as real-time applications. The |performance_model| model runs around 10 times slower, but offers the highest quality keywording results.

Since content can change quite drastically within a video, we offer both 'segment-level' as well as 'video-level' keywording. As the names suggest, segment-level keywording finds keywords for each individual segment, whereas video-level keywording provides keywords that are representative of the whole video. The figure above illustrates these concepts.





Action recognition
^^^^^^^^^^^^^^^^^^

A key difference between images and videos is that in a video, we can look at the temporal evolution of events, which allows us to identify actions, such as walking, running, jumping, etc. |mobvis_video| currently recongnizes 140 actions. 

As with the static keywording module, there is both a 'segment-level' and a 'video-level' action recognition. The video-level can be seen as a summary of the per-segment detected actions, sorted by the overall duration of the respective actions.  


(Soon) Highlights Detection
----------------------------

We are currently working hard to add a video highlighting feature to the |mobvis_video|. This feature allows to obtain 'highlight scores' for video segments, which allows to identify the most important parts of a video. This can be very useful for example in order to create a summary of a video that can be shown if someone is browsing through a video database.




Advantages of on-premise installation compared to API service
---------------------------------------------------------------
This set-up has several advantages over a (cloud-based) API service, including:

* Data privacy by design: the data always stays on your system
* Security as control over the data flow is kept
* Considerably faster, since the videos do not have to be sent to a server to be analyzed. This is particularly important for real-time applications.
