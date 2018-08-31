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

The first step is to add images to the docker volume by sending a POST request to the following endpoint.
::

  curl 127.0.0.1:5000/similarity/add?id=<unique_id> -X POST -F "data=@./your_img.jpg"

where id is an optional argument. Without this argument the system will generate a random ID number and return it as a response.

.. note::

  The ID numbers for sample images should be unique since it's used internally to identify the images. We recommend either using numbers or a combination of numbers and letters. It should be passed as a string.

You can add samples from a python script as well.
::

  def add_sample(img_path, ID):
    with open(img_path, 'rb') as image:
        data = {'data': image}
        r = requests.post('http://127.0.0.1:5000/similarity/add?id=%s' % ID, files=data).json()
    return r

The SDK is then processing these images to extract numerical features according to our pre-trained Mobius keywording model. For keeping all samples we generate an auxiliary structure we call an "index".

.. warning::

  This step is very computationally heavy. If the number of images is very large (more than 1 million) it may take more than one day to process all images on a single GPU.

Training
------------

For the search the extracted numerical representation of the images has to be further processed. The index training enables fast search and adaptation to the given image data.

To run index training send GET request to the following endpoint.
::

  curl 127.0.0.1:5000/similarity/train

.. note::

  You should add at least 1 000 images for successful index training. We recommended to use at least 100 000 images.

The request will return a json file with the field task_id that can be used to get status of training:
::

  curl 127.0.0.1:5000/similarity/status/<task_id>

The following error messages could appear:

* *'need more samples'* displayed if the number of samples is less than 1000
* *'no samples'* if no samples have been added for training
* *'no index, train first'* update function can only be called after one training has been carried out

.. note::

  Although this process is quite fast it may take several hours to process all images.

Search
------

After adding the sample images to the docker volume as well as the index and training on all samples, the search function can be used.

To do search with a query image use the following endpoint.
::

  curl 127.0.0.1:5000/similarity/search -X POST -F "data=@./your_query_img.jpg"


Or this call from a python script:
::

  def search(img_path):
      with open(img_path, 'rb') as image:
          data = {'data': image}
          r = requests.post('http://127.0.0.1:5000/similarity/search', files=data).json()
      return r

.. note::

  Our search call is very fast and should generally run in less than 1 second.

The output is split into three parts:

* One list of distances in floating point precision that quanifies the similarity of similar images found. The list is sorted ascending since the lowest distance means that the similarity was highest.
* One list of image IDs that have been stored in the index and correspond to the specific similar images found with distances in first list
* A status message that says 'ok' if no error occurred in the search.


Example of an output
::

  {
      'dist': [349.9123229980469, 363.0243835449219, 501.1552734375, 519.2177734375, 576.5772705078125, 663.9130859375, 667.498291015625, 671.4913940429688, 684.84228515625, 705.6535034179688],
      'result': ['1260', '140', '1267', '1685', '866', '1173', '583', '105', '4', '154'],
      'status': u'ok'
  }


You can control the number of similar images returned by the environment variable SIMILARITY_SEARCH_NUM_RESULTS (use -e option for docker). The default value is 10.

.. note::

  You can use the environment variable NPROB to balance between speed and accuracy. It has to be an integer between 1 and 100 (With a smaller value the search is faster but less accurate). The default and recommended value is 5.

Updating
------------

In many cases it might be desired to add more images after the initial training. For this case you can use the update function that preserves previously added images in the index and adds the new images without retraining.

.. note::

  Images have to be added to the docker volume as a first step before the update function can be run.

To update the index send a GET request to the following endpoint.
::

  curl 127.0.0.1:5000/similarity/update

The request will also return a json file with a task_id that can be used to get status of updating:
::

  curl 127.0.0.1:5000/similarity/status/<task_id>

.. warning::

  This step is also computationally heavy. If the number of images is very large (more than 1 million) it may take several hours to process all images on a single GPU.

Then search can be carried out on the previously added images and the new images at once.
