Keywording
==========

The *pre-trained* image keywording module can be used to obtain predictions for a wide range of applications.

This is an example for prediction:
::

  curl 127.0.0.1:5000/predict/concepts -X POST -F "data=@./your_image.jpg"

You can call the endpoint from python
::

  def get_keywords(img):
     with open(img,'rb') as image:
         data = {'data': image}
         pred = requests.post('http://127.0.0.1:5000/predict/concepts', files=data).json()
     return pred

.. note::

    Depending of the image, the number of returned keywords might vary in this mode.

All keywords with a confidence above a certain threshold are returned.
For some simple images, the keywording module might only recognise a small number of matching keywords.
However, in cluttered scenes, there might be a long list of matching keywords.

There are a number of arguments that can be passed to alter behaviour of image keywording. The arguments can be passed by adding a “?” after the tag command, followed by the argument=value. Several arguments are separated using the “&”. The following example illustrates this:
::
  
  curl 127.0.0.1:5000/predict/concepts?top_k=10&hierarchical_output=false -X POST -F "data=@./your_image.jpg"
  
Below is list of the different arguments that can be set, together with their default values.

* *top_k* (unspecified by default): Flag to obtain the highest scored `k` keywords
* *keyword_threshold* (default *0.55*): Threshold on the confidence of keyword predictions
* *hierarchical_output* (default *true*): Flag to signal if keywords should be grouped by category


Prediction with large number of images
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Please note that prediction calls are time consuming. It's recommended to run predictions
in parallel.

Here is an example how to use multiprocessing in python to speed things up:

::

  from multiprocessing import Pool
  import requests

  pool = Pool(50)
  images = [path_to_image1, path_to_image2, ...] #List of image paths
  results = pool.map(get_keywords, images)
  pool.close()
  pool.join()
