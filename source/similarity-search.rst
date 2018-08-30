Advanced: Similarity Search
=================================


Adding samples
--------------

To add images to SDK send POST request to the following endpoint.
::

  curl 127.0.0.1:5000/similarity/add?id=<unique_id> -X POST -F "data=@./your_img.jpg"

where id is optional argument. ID should be unique. Without the argument system will generate random ID and return it as a response.

You can do it from python as well.
::

  def add_sample(img_path, i):
      with open(img,'rb') as image:
          data = {'data': image}
          r = requests.post('http://127.0.0.1:5000/similarity/add?id=%d'%i, files=data).json()
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
