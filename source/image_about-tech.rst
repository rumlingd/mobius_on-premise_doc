About Mobius Vision Image SDK
======================================

This SDK uses advanced algorithms for computer vision based on a technology called Deep Learning (DL).

DL technology helps computers to understand images not just as a matrix of pixels
but to connect different levels such as lines, simple geometric shapes to complex objects such as faces and cars.
It gives computers some sense of complex understanding on the content and quality of images.


The Mobius Vision on-premise solution is shipped with two base models and a customizable mini-model that is built on top of the base models.
The reasoning behind this set up is that customization needs far less effort as the base models already include
a large body of knowledge that can be leveraged directly to identify new objects or styles.


Object recognition with keywords
------------------------------------

|mobvis_image| comes with a model for keywords that the computer can see in a given image.
Our over 5000 keywords have different levels of granularity. It differs between people and no people but also on a lower level
between men and women.
Given one image as an input, the model returns the keywords for the categories together with the confidence of the algorithm in the result.

.. image::
   data/keywords_tree.png
   :align: center

Currently, the on-premise solution does not enable to localize the objects. This means that the computer recognizes that
there is an object in the given image, but not where.

Aesthetics evaluation
-----------------------

The second module that is included in |mobvis_image| is a model to evaluate the aesthetics of an image.
The aesthetics style is defined by professional curators. Multiple millions of images were rated by the professional curators over multiple years.
The algorithm has learnt to differentiate between images of 'poor', 'average', 'good' and 'very good' aesthetics.
There was no further information provided to the algorithm. It has learnt by itself by evaluating many million examples how to define aesthetics. 


Customized Training
------------------------

One powerful tool that comes with the SDK is the customized training, which allows to train a custom and reusable mini-model.
It is built on top of our object recognition and aesthetics base models - so it can leverage their knowledge to understand properties of new objects or styles.

Optional mobile models porting
--------------------------------

The base models in this on-premise SDK are large models to run very accurately on GPUs.
However, at Mobius Labs we also have great tiny models for usage on mobile phones that are much smaller and faster.
The accuracy of these models is slightly lower. If a large speedup is necessary, please contact us about this option.

Advantages of on-premise installation compared to API service
---------------------------------------------------------------

* Data privacy by design: the data always stays in your system
* Security as control over the data flow is kept
* Fast speed that is not depending on latency
