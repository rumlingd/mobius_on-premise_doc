Getting Started and Prediction
================================

Running the SDK
----------------

Running the SDK depends on the installation type (wheel or docker)


Wheel version
^^^^^^^^^^^^^^


1. Run server (in separate window, e.g., screen -S vision_server)
::

  CUDA_VISIBLE_DEVICES="" MOBIUS_TOKEN="<your_token>" gunicorn -w 10 -b 0.0.0.0:5000 mobius_vision.request_server.main:application

2. Run model server (in separate window, e.g., screen -S model_server)
::

  NUM_WORKERS="10" MOBIUS_TOKEN="<your_token>" run_all_models


3. Test installation
::

  curl 127.0.0.1:5000/predict -X POST -F "data=@./your_image.jpg"


Docker version
^^^^^^^^^^^^^^^

1. Run docker image
::

  nvidia-docker run -v sim_search_data:/data -v sim_search_redis:/var/lib/redis -p 5000:5000 -e CUDA_VISIBLE_DEVICES="0" -e NUM_WORKERS="10" -e MOBIUS_TOKEN="<your_token>" -it mobius_labs/mobius_sdk:0.1

2. Test installation
::

  curl 127.0.0.1:5000/predict -X POST -F "data=@./your_image.jpg"


Prediction with Pre-trained Modules
-----------------------------------

The SDK is shipped with two modules that were trained on our large image dataset.
These *pre-trained modules* can be used to obtain predictions for a wide range of applications.

**Keywording**

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

All keywords with a confidence above a certain threshold are returned.
For some simple images, the keywording module might only recognise a small number of matching keywords.
However, in cluttered scenes, there might be a long list of matching keywords. Depending of the image, the number
of returned keywords might vary.


**Aesthetics**

Prediction with the aesthetics module works in a similar fashion.
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
