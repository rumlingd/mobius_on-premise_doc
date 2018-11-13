Aesthetics
===========

Prediction with the aesthetics module works in a similar way to the keywording module.
::

  curl 127.0.0.1:5000/predict/aesthetic -X POST -F "data=@./your_image.jpg"

Or in python
::

  def get_aesthetic(host, img):
     with open(img,'rb') as image:
         data = {'data': image}
         pred = requests.post('http://127.0.0.1:5000/predict/aesthetic', files=data).json()
     return pred

Prediction with large number of images
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Please note that prediction is time consuming. It's recommended to run predictions
in parallel.

Here is an example how to use multiprocessing in python to speed things up:
::

  from multiprocessing import Pool
  import requests

  pool = Pool(50)
  images = [path_to_image1, path_to_image2, ...] #List of image paths
  results = pool.map(get_aesthetic, images)
  pool.close()
  pool.join()