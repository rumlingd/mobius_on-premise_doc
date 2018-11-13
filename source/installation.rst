.. _installation-label:

Installation
==================

Before you can use the Mobius On-Premise SDK, you have to follow a few steps as explained here. There are two ways of installation: wheel package and docker image. The docker image is very easy to install, but is around 5GB (for the GPU version). The wheel package requires a few more steps to be installed, but is only around 400 MB.


Requirements for the Mobius On-Premise SDK
-------------------------------------------

In order to run the Mobius Vision On-Premise SDK, the following software requirements have to be met:

*   CUDA 9+ (requires a GPU)
*   Python 2.7
*   ffmpeg 2.8.15 (only for |mobvis_video|)


Installation from docker image
-------------------------------

1. First, you need to install nvidia-docker2. If nvidia-docker2 are installed already then you can skip this step and move to step 2.

  1.1 Install Docker CE: 
  https://docs.docker.com/install/linux/docker-ce/ubuntu/


  1.2. Add nvidia-docker repo to apt, as explained here: 
    https://nvidia.github.io/nvidia-docker/

  1.3. Install the nvidia-docker2 package and reload the Docker daemon configuration
  ::

    sudo apt-get install nvidia-docker2
    sudo pkill -SIGHUP dockerd

  1.4. Add your user to the docker group.
  ::

    sudo usermod -aG docker $USER

  1.5. Log out and log back in so that your group membership is re-evaluated.


2. Load Mobius Vision docker image
::

  docker load --input mobius_vision.tar


3. To check that image was loaded sucessfully run following command
::

  docker images

You should see something like this
::

  REPOSITORY TAG IMAGE ID CREATED SIZE
  mobius_labs/mobius_sdk 0.1 ef8d42276b3f 18 minutes ago 6GB


Installation from wheel package
--------------------------------
0. Confirm that the python version you are running is 2.7
::

  python --version

1. Install prerequisites
::

  sudo apt-get update
  sudo apt-get install -y \
  redis-server \
  python-pip \
  python3-pip \
  libsm6 \
  libgtk2.0-0
  pip install gunicorn Cython tensorflow-gpu==1.8 mxnet-cu90 onnx --user

2. Copy the wheel file to your server, and change to that directory.

3. Install Mobius Vision package
::

  pip install mobius_vision-0.1.2-cp27-cp27mu-linux_x86_64.whl --user

4. Run redis server
::

  sudo service redis-server start

Now you are ready to move to the next page.
