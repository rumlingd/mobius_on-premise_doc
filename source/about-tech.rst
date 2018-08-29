About the Technology
======================================

This SDK uses advanced algorithms for computer vision based on a technology called Deep Learning (DL).

DL technology has helped computers to understand images not just as a matrix of pixels
but to connect different levels such as lines, simple geometric shapes to complex objects such as faces and cars.
It gives computers some sense of hierarchical understanding on the content of images.

With this hierarchical understanding, computers can recognize complex objects in images.

The Mobius Vision SDK is shipped with two base models and a customizable mini-model that is built on top of the base models.
The reasoning behind this set up is that customization needs far less effort as the base models already include
lots of knowledge which can be leveraged directly for new objects or styles.


Object recognition with keywords
------------------------------------

The Mobius Vision SDK comes with a model for keywords that the computer can see in a given image.
Our over 5000 keywords have different levels of granularity. It differs between people and no people but also on a lower level
between men and women.
Given one image as an input, the model returns the keywords for the objects it detected with highest confidence.

.. image::
   data/keywords_tree.png
   :align: center

Currently, the SDK does not enable to pinpoint to the objects. So the computer recognizes that
there is an object in the given image but not where.

Aesthetics evaluation
-----------------------

The second module that is included in Mobius Vision is a model to evaluate the aesthetics of an image.


Customizable mini-model
------------------------

One powerful tool that comes with the SDK is a customizable and reusable mini-model.
It is built on top of our object recognition and aesthetics base models - so it can use their knowledge to understand properties of new objects or styles.

Optional mobile models porting
--------------------------------

The base models in this on-premise SDK are large models to be run on GPUs.
However, at Mobius Labs we also have great mobile models that are much smaller and faster.
The accuracy of these models is slightly lower. If a large speedup is necessary, please contact us about this option.

Advantages of on-premise installation compared to API service
---------------------------------------------------------------
This set-up has great advantages such as:

* Data privacy by design: the data always stays in your system
* Security as control over the data flow is kept
* Fast speed that is not depending on latency

at a moderate cost of:
* Slightly more difficult installation 
