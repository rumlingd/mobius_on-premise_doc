Video Tagging
=======================================
The video tagging module has been trained on our large in-house image dataset to provide state-of-the-art keywording results. Depending on the licence, it consists of a video shot detector, a keywording module for static concepts and emotions, as well as an action recognition module.

In the following, we show an example of how to do prediction of keywords and/or actions on videos. 
First, we need to send the video to the (local) vision server for analysis.
::

  curl 127.0.0.1:5000/video/tag -X POST -F "data=@./your_video.mp4"

The above command will return an information message:
::

  {"message":"video_tagging","status":"ongoing","task_id":"599600ef-817f-413e-85f5-d4fc55313164"}

The **task_id** will be required in the next step.
  
Depending on various factors, including duration and resolution of the video, but also the type of keywording model selected (|lightweight_model| or |performance_model|), the time until the keywording is finished will vary. 
With the following command, you can check the status of the process at any time. 
::
  
  curl 127.0.0.1:5000/status/<task_id>
  
where you would replace <task_id> with 599600ef-817f-413e-85f5-d4fc55313164 in the example above. 

If the video is still being processed, the status message will be:
::
  
  {"status": "ongoing", "message": "video_tagging"}
  
When the processing is finished, the status message will contain the keywording results (static and/or actions, depending on your licence):
::
  
  {"status": "success", "result": [{"keywords": [["people", 0.9846186637878418], 
  ["adult", 0.7601927518844604], ["indoors", 0.717658519744873], ...], 
  "time_stamps": [0.0, 19.333333333333332], 
  "actions": [["painting", 0.8850449323654175]]}]}

All keywords with a confidence above a certain threshold are returned (0.5 by default).

.. note::
    
    Depending on the complexity of a video shot, the number of keywords returned will vary. In addition, in case the shot
    detector in disabled, the results might also be of lower quality in cases where a segment contains different shots (and hence, potentially very different concepts). 
    

Optional arguments
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

There are a number of arguments that can be passed:

* keyword_threshold (default 0.5): Threshold on the confidence of the keyword predictions
* keyword_topk (default 50): Maximum number of keywords to be returned *per video shot*
* action_threshold (default 0.6): Threshold on the confidence of action predictions
* action_topk (default 1): Maximum number of actions to be returned *per video shot*

The arguments can be passed by adding a "?" after the tag command, followed by the argument=value. Several arguments are separated using the "&". The following example illustrates this:
::
  
  curl 127.0.0.1:5000/video/tag?keyword_threshold=0.6&action_threshold=0.7 -X POST -F "data=@./your_video.mp4"


Error messages
^^^^^^^^^^^^^^

If there is an error on one of the input arguments, the following status message will be returned:
::
  
  {'status': 'error', 'message': 'wrong_arguments_format', 'arg': 'keyword_topk'}
  
If the video format is not supported, the status message is:
::
  
  {'status': 'error', 'message': 'video_reading_error'}
  

Prediction in Python
^^^^^^^^^^^^^^^^^^^^

The code snipped below shows how prediction can be done in Python.

::
    #import time
    
    def analyze_video(video_path):
         with open(video_path,'rb') as video:
             data = {'data': video}
             res = requests.post('http://127.0.0.1:5000/video/tag', files=data).json()
             task_id = res['task_id']
             msg = requests.get('http://127.0.0.1:5000/status/' + task_id).json()
             
             while(msg['status'] is 'ongoing'):
                 msg = requests.get('http://127.0.0.1:5000/status/' + task_id).json()
                 #time.sleep(1.0)
                 
             if(msg['status'] == 'success'):
                pred = msg['result']
             else:
                pred = msg['status']
        
        return pred





  
