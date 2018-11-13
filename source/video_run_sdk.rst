Running the SDK
================================

Before you can use the Mobius On-Premise SDK, you have to follow a few steps as explained in :ref:`installation-label`.
Running the SDK depends on the installation type (wheel or docker)


Docker version
^^^^^^^^^^^^^^^

1. Run docker image (in separate window, e.g., screen -S vision_server)
::

  nvidia-docker run -v mobius_vision_data:/data -v mobius_vision_redis:/var/lib/redis -p 5000:5000 -e CUDA_VISIBLE_DEVICES="0" -e NUM_WORKERS="40" -e MOBIUS_TOKEN="<your_token>" -it mobius_labs/mobius_sdk:1.1

2. Test installation
::

  curl 127.0.0.1:5000/video/tag -X POST -F "data=@./your_video.mp4"

The above command should return an information message similar to the one below:
::

  {"message":"video_tagging","status":"ongoing","task_id":"599600ef-817f-413e-85f5-d4fc55313164"}
  

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

  curl 127.0.0.1:5000/video/tag -X POST -F "data=@./your_video.mp4"

The above command should return an information message similar to the one below:
::

  {"message":"video_tagging","status":"ongoing","task_id":"599600ef-817f-413e-85f5-d4fc55313164"}
