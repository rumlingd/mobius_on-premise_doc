Advanced: Similarity Search
=================================

Overview and work flow
------------------------
It takes a few steps to run the whole similarity search with the Mobius Vision SDK.
Generally there is a difference between the very first usage and then usage in a running system.
In both cases samples have to be added. In the initial phase the system is trained with all images.
In the update step, only those images are added to the index list. This prevents the computationally heavy training procedure to be carried out again on all input images.

Initial phase:

#. Add samples
#. Train index
#. Search with query image

In a running system:

#. Add sample
#. Update index
#. Search with query image

The following illustration shows in a simplified manner how the SDK works.

.. image::
  data/similarity_search.png
  :align: left

Adding samples
--------------

The first step is to add images to the SDK by sending a POST request to the following endpoint.
::

  curl 127.0.0.1:5000/similarity/add?id=<unique_id> -X POST -F "data=@./your_img.jpg"

where id is an optional argument. Without this argument system will generate a random ID number and return it as a response.

.. note::

  The ID numbers for sample images should be unique since it's used internally to identify the images. We recommend either using numbers or a combination of numbers and letters. It should be passed as a sting.

You can add samples from python as well.
::

  def add_sample(img_path, ID):
    with open(img_path, 'rb') as image:
        data = {'data': image}
        r = requests.post('http://127.0.0.1:5000/similarity/add?id=%s' % ID, files=data).json()
    return r

Training
------------

To run index training send GET request to the following endpoint. You should add at least 1 000 images to train index successfully. Recommended number of images before train is 100 000.
::

  curl 127.0.0.1:5000/similarity/train

The request will return json with field task_id that can be used to get status of training:
::

  curl 127.0.0.1:5000/similarity/status/<task_id>


Updating
------------

To update index without retraining send GET request to the following endpoint.
::

  curl 127.0.0.1:5000/similarity/update

The request will return json with field task_id that can be used to get status of training:
::

  curl 127.0.0.1:5000/similarity/status/<task_id>


Search
------


To do search by image use the following endpoint.
::

  curl 127.0.0.1:5000/similarity/search -X POST -F "data=@./your_img.jpg"

Or in python:
::

  def search(img_path):
      with open(img,'rb') as image:
          data = {'data': image}
          r = requests.post('http://10.101.101.21:5000/similarity/search', files=data).json()
      return r


Output contain list of ID and distances.

Example of a output
::

  {
      'dist': [349.9123229980469, 363.0243835449219, 501.1552734375, 519.2177734375, 576.5772705078125, 663.9130859375, 667.498291015625, 671.4913940429688, 684.84228515625, 705.6535034179688],
      'result': ['1260', '140', '1267', '1685', '866', '1173', '583', '105', '4', '154'],
      'status': u'ok'
  }


You can control the number of results by enviroment variable SIMILARITY_SEARCH_NUM_RESULTS (use -e option for docker). Default value is 10.

You can use enviroment variable NPROB to balance between speed and accuracy. A value is integer between 1 and 100 (smaller value is faster but less accurate). Default and recommended value is 5.
