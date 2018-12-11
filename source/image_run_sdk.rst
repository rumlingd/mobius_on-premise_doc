Running the SDK
===============

Before you can use the Mobius On-Premise SDK, you have to follow a few steps as explained in :ref:`installation-label`.


1. Run docker image (in separate window, e.g., screen -S vision_server)
::

  nvidia-docker run -v mobius_vision_data:/data -v mobius_vision_redis:/var/lib/redis -p 5000:5000 -e CUDA_VISIBLE_DEVICES="0" -e NUM_WORKERS="40" -e MOBIUS_TOKEN="<your_token>" -it mobius_labs/mobius_sdk:1.1

2. Test installation
::

  curl 127.0.0.1:5000/predict -X POST -F "data=@./your_image.jpg"