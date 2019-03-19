.. _installation-label:

Installation
==================

Before you can use the Mobius On-Premise SDK, you have to follow a few steps as explained here.
There are two ways of installation: wheel package and docker image. The docker image is very easy to install, but is around 6GB (for the GPU version).
The wheel package requires a few more steps to be installed, but is only around 400 MB. By default we provide a docker container. Therefore, our instructions focus on this set-up.


Requirements for the Mobius On-Premise SDK
-------------------------------------------

In order to run the Mobius Vision On-Premise SDK, the following software requirements have to be met:

*   Nvidia Drivers >= 396.37 (for GPU version)
*   docker >= 1.12
*   nvidia-docker2 (for GPU version)


Docker Installation
-------------------

To use GPU versions of Mobius Vision SDK you need to have nvidia-docker2. You can install it by instructions from https://github.com/NVIDIA/nvidia-docker or our instructions.

If nvidia-docker2 are installed already then you can skip this step.

1. Install Docker CE:
https://docs.docker.com/install/linux/docker-ce/ubuntu/


2. Add nvidia-docker repo to apt, as explained here:
  https://nvidia.github.io/nvidia-docker/

3. Install the nvidia-docker2 package and reload the Docker daemon configuration
::

  sudo apt-get install nvidia-docker2
  sudo pkill -SIGHUP dockerd

4. Add your user to the docker group.
::

  sudo usermod -aG docker $USER

5. Log out and log back in so that your group membership is re-evaluated.


Mobius Vision Installation
--------------------------

1. Build Mobius Vision docker image
::

  unzip mobius_sdk.zip
  cd mobius_sdk
  nvidia-docker build -t mobius_labs/mobius_sdk:latest -f Dockerfile .

3. To check that image was built sucessfully run following command
::

  docker images

You should see something like this
::

  REPOSITORY               TAG           IMAGE ID            CREATED             SIZE
  mobius_labs/mobius_sdk   latest        d4a9c41f3496        32 minutes ago      6.69GB

Now you are ready to run the SDK.
