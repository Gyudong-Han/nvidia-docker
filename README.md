# NVIDIA Container Runtime for Docker

[![GitHub license](https://img.shields.io/badge/license-New%20BSD-blue.svg?style=flat-square)](https://raw.githubusercontent.com/NVIDIA/nvidia-docker/master/LICENSE)
[![Documentation](https://img.shields.io/badge/documentation-wiki-blue.svg?style=flat-square)](https://github.com/NVIDIA/nvidia-docker/wiki)
[![Package repository](https://img.shields.io/badge/packages-repository-b956e8.svg?style=flat-square)](https://nvidia.github.io/nvidia-docker)

![nvidia-gpu-docker](https://cloud.githubusercontent.com/assets/3028125/12213714/5b208976-b632-11e5-8406-38d379ec46aa.png)

## Quickstart

**Make sure you have installed the [NVIDIA driver](https://github.com/NVIDIA/nvidia-docker/wiki/Frequently-Asked-Questions#how-do-i-install-the-nvidia-driver) and docker 19.03**

```sh
### Ubuntu 14.04/16.04/18.04, Debian Jessie/Stretch
# Add the package repositories
curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add -
distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | sudo tee /etc/apt/sources.list.d/nvidia-docker.list
sudo apt-get update

sudo apt-get install -y libnvidia-container-plugin

#### CentOS 7 (docker-ce), RHEL 7.4/7.5 (docker-ce), Amazon Linux 1/2

distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.repo | sudo tee /etc/yum.repos.d/nvidia-docker.repo

sudo yum install -y libnvidia-container-plugin

#### Test nvidia-smi with the latest official CUDA image
$ docker run --gpus all nvidia/cuda:9.0-base nvidia-smi

# Start a GPU enabled container on two GPUs
$ docker run --gpus 2 nvidia/cuda:9.0-base nvidia-smi

# Starting a GPU enabled container on specific GPUs
$ docker run --gpus device=1,2 nvidia/cuda:9.0-base nvidia-smi
$ docker run --gpus device=UUID-ABCDEF,1 nvidia/cuda:9.0-base nvidia-smi

# Specifying a capability (graphics, compute, ...) for my container
# Note this is rarely if ever used this way
$ docker run --gpus all,capabilities=utilities nvidia/cuda:9.0-base nvidia-smi
```

#### Other distributions and architectures

Look at the [Installation section](https://github.com/nvidia/nvidia-docker/wiki/Installation-(version-2.0)) of the wiki.
For docker-ce on `ppc64le`, look at the [FAQ](https://github.com/nvidia/nvidia-docker/wiki/Frequently-Asked-Questions#do-you-support-powerpc64-ppc64le).


## Existing Users of nvidia-docker2 

If you have the nvidia-docker2 package already installed you can update to docker latest and profit from the latest `--gpu` feature. Alternatively you can still use the old behavior:

```
$ sudo apt-get update
$ sudo apt-get --only-upgrade install docker-ce # Alternatively Will automatically update nvidia-docker

# All of the following options will continue working
$ docker run --gpus all nvidia/cuda nvidia-smi
$ docker run --runtime nvidia nvidia/cuda nvidia-smi
$ nvidia-docker run nvidia/cuda nvidia-smi
```


## Changelog

New nvidia-docker packages have been released for docker 18.09.2 and 18.06.2 addressing [CVE-2019-5736](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-5736)

Update nvidia-docker to adress runc critical vulnerability that allows specially-crafted containers to gain administrative privileges on the host.
```sh
# On Ubuntu/Debian
sudo apt upgrade

# On Centos/RHEL/Amazon Linux
sudo yum upgrade
```

## Issues and Contributing

A signed copy of the [Contributor License Agreement](https://raw.githubusercontent.com/NVIDIA/nvidia-docker/master/CLA) needs to be provided to <a href="mailto:digits@nvidia.com">digits@nvidia.com</a> before any change can be accepted.

* Please let us know by [filing a new issue](https://github.com/NVIDIA/nvidia-docker/issues/new)
* You can contribute by opening a [pull request](https://help.github.com/articles/using-pull-requests/)
