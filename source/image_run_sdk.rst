Running the SDK
===============

Before you can use the Mobius On-Premise SDK, you have to follow a few steps as explained in :ref:`installation-label`.


1. Run docker image (in separate window, e.g., screen -S vision_server)
::

  nvidia-docker run --init -v mobius_vision_data:/data -v mobius_vision_redis:/var/lib/redis -p 5000:5000 \
                    -e CUDA_VISIBLE_DEVICES="0" -e NUM_WORKERS="40" -e MOBIUS_TOKEN="<your_token>" \
                    -it mobius_labs/mobius_sdk:latest

.. note::

    Please make sure to insert the token you have received by email at "your_token" and double check the sdk name passed as the last argument.


2. Test installation
In the command line tool of the docker image you can test the installation by passing a jpg file by replacing the path and file name below.
::

  curl 127.0.0.1:5000/predict -X POST -F "data=@./your_image.jpg"
