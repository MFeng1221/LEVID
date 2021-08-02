# LEVID

Usage and more information can be found below.

## Usage

How to run the code:

We recommend to run the code through docker. Some brief documentation can be found at https://docs.docker.com/.

1. Please build a docker image using the dockerfile provided.

``sudo docker pull fengfeng1221/LEVID:v0.1``

2. Pull the codes for CoLight.
``git clone https://github.com/MFeng1221/LEVID.git``

3. Please run the built docker image to initiate a docker container. Please remember to mount the code directory.

``sudo docker run -it -v /path/to/your/workspace/LEVID/:/LEVID/ --shm-size=8gb --name LEVID /bin/bash``

``cd LEVID``

(Alternatively, you can install the packages (included in the dockerfile) on your linux system)

Start an experiment by:

``python -O runexp.py``

Here, ``-O`` option cannot be omitted unless debug is necessary. In the file ``runexp.py``, the args can be changed.

* ``runexp.py``

  Run the pipeline under different traffic flows. Specific traffic flow files as well as basic configuration can be assigned in this file. For details about config, please turn to ``config.py``.

* ``run_baseline.py``

 Run the baseline in traditional transportation field


For most cases, you might only modify traffic files and config parameters in ``runexp.py``.

## Dataset

* synthetic data

  Traffic file and road networks can be found in ``data/1_3`` && ``data/3_3`` && ``data/6_6`` && ``data/10_10``.

* real-world data

  Traffic file and road networks of New York City can be found in ``data/NewYork``, it contains two networks at different scale: 196 intersection and 48 intersections. Jinan and Hangzhou dataset are also included. We have added HeFei dataset.


## Agent

* ``agent.py``

  An abstract class of different agents.

* ``MyLight_agent.py``

  Proposed Traffic sognal control model of LEVID. The pre-feature processing is done in ``anon_env.py``.

## Others

More details about this project are demonstrated in this part.

* ``config.py``

  The whole configuration of this project. Note that some parameters will be replaced in ``runexp.py`` while others can only be changed in this file, please be very careful!!!

* ``pipeline.py``

  The whole pipeline is implemented in this module:

  Start a simulator environment, run a simulation for certain time(one round), construct samples from raw log data, update the model and model pooling.

* ``generator.py``

  A generator to load a model, start a simulator enviroment, conduct a simulation and log the results.

* ``anon_env.py``

  Define a simulator environment to interact with the simulator and obtain needed data like features.

* ``construct_sample.py``

* Construct training samples from original data. Select desired state features in the config and compute the corrsponding average/instant reward with specific measure time.

* ``updater.py``

  Define a class of updater for model updating.

