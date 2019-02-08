Running the SDK
================================

Before you can use the Mobius On-Premise SDK, you have to follow a few steps as explained in :ref:`installation-label`.

1. Run docker image (in separate window, e.g., screen -S vision_server)
::

  nvidia-docker run -v mobius_vision_data:/data -v mobius_vision_redis:/var/lib/redis -p 5000:5000 -e CUDA_VISIBLE_DEVICES="0" -e NUM_WORKERS="40" -e MOBIUS_TOKEN="<your_token>" -it mobius_labs/mobius_sdk:1.1

2. Test installation
::

  curl 127.0.0.1:5000/video/tag -X POST -F "data=@./your_video.mp4"

The above command should return an information message similar to the one below:
::

  {"message":"video_tagging","status":"ongoing","task_id":"599600ef-817f-413e-85f5-d4fc55313164"}
  
