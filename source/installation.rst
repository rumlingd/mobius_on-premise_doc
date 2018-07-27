Installation
==================

Before you can use the Mobius On-Premise SDK, you have to follow a few steps as explained here. There are two ways of installation: wheel package and docker image.


Requirements for the Mobius On-Premise SDK
-----------------------------------------

There are Requirements on the hardware and the software.

There are the following requirements:

*   CUDA 9+

Installation from wheel package
-------------------------

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

2. Install Mobius Vision package
::
  pip install mobius_vision-0.1.2-cp27-cp27mu-linux_x86_64.whl --user

3. Run redis server
::
  sudo service redis-server start


Installation from docker image
-------------------------

First, you need to install nvidia-docker2. If nvidia-docker2 are installed already then you can skip this step.

1. Install Docker CE
:: 
  https://docs.docker.com/install/linux/docker-ce/debian/#install-docker-ce

2. Add nvidia-docker repo to apt
::
  https://nvidia.github.io/nvidia-docker/

3. Install the nvidia-docker2 package and reload the Docker daemon configuration
::
  sudo apt-get install nvidia-docker2
  sudo pkill -SIGHUP dockerd

4. Add your user to the docker group.
::
  sudo usermod -aG docker $USER

5. Log out and log back in so that your group membership is re-evaluated.


Load Mobius Vision docker image
::
  docker load --input mobius_vision.tar


To check that image was loaded sucessfully run following command
::
  docker images

You should see something like this
::
  REPOSITORY TAG IMAGE ID CREATED SIZE
  mobius_labs/mobius_sdk 0.1 ef8d42276b3f 18 minutes ago 6GB