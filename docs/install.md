---
id: install
title: Installing BlueWhale
sidebar_label: Installing
---

This guide explains how to get up and running with BlueWhale.  If you have issues, please [file them on GitHub](https://github.com/facebookresearch/BlueWhale/issues/new)!

## Requirements

### Python3 (recommended for mac: Anaconda)

All of BlueWhale code depends on Python 3's type inference system.  For mac users, we recommend using [Anaconda](https://www.continuum.io/downloads) instead of the system implementation of python. Install anaconda and verify you are using Anaconda's version of python before installing other dependencies: `which python` should yield an Anaconda path.

### Caffe2

BlueWhale runs on any platform that supports caffe2. To install caffe2, you can use conda:

```
conda install -c caffe2 caffe2
```

Alternatively, you can build from source outlined in this tutorial: [Installing Caffe2](https://caffe2.ai/docs/getting-started.html).

You may need to override caffe2's cmake defaults to use homebrew's protoc instead of Anaconda's protoc and to use Anaconda's Python instead of system Python.  Also add the following switch when running cmake to make sure caffe2 uses python3:

```
cmake -DPYTHON_EXECUTABLE=`which python3`
```

Also make sure cmake is using the **homebrew** version of glog, etc..  Sometimes caffe2
will try to use the anaconda version of these libraries, and that will cause errors.

### PyTorch

Some of our models are implemented in PyTorch which can be installed via conda:

```
conda install pytorch torchvision -c pytorch
```

Alternatively, you can build directly from source as outlined here: [Installing Pytorch](https://github.com/pytorch/pytorch#from-source). Sometimes the latest PyTorch changes are not included in the version conda installs which can lead to errors. In this case building PyTorch from source should mitigate the issue.


### Thrift

Most distributions contain Apache Thrift.  Because we are running python3, we need at least thrift 0.10.  For OS/X:

```
brew install thrift
```

Then we need the python bindings for thrift, which we can get from anaconda:

```
conda install thrift
```

### OpenAI Gym

Running models in OpenAI Gym environments requires platforms with OpenAI Gym support. Windows support for OpenAI Gym is being tracked [here](https://github.com/openai/gym/issues/11).

OpenAI Gym can be installed using [pip](https://pypi.python.org/pypi/pip) which should come with your python installation in the case of linux or with anaconda in the case of OSX.  To install the basic environments ([classic control](https://gym.openai.com/envs#classic_control), [toy text](https://gym.openai.com/envs#toy_text), and [algorithmic](https://gym.openai.com/envs#algorithmic)), run:

```
pip install gym
```

To install [all environments](https://gym.openai.com/envs/), run this instead:

```
pip install "gym[all]"
```

## Installation and Setup

Clone from source:

```
git clone https://github.com/facebookresearch/BlueWhale
cd BlueWhale
```

Create thrift generated code within the root directory:

```
thrift1 --gen py:json --out . ml/rl/thrift/core.thrift
```

To access caffe2 and import our modules:

```
export PYTHONPATH=/usr/local:./:$PYTHONPATH
```

## Running Unit Tests

From within the root directory, run all of our unit tests with:

```
python -m unittest discover
```

To run a specific unit test:

```
python -m unittest <path/to/unit_test.py>
```

## Building your own model

To build your own models, start by following our OpenAI Gym Tutorial [here.](openai_gym.md)
