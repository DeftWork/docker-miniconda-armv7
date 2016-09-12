# Miniconda armv7 crossbuild
[![](http://dockeri.co/image/show0k/miniconda-armv7)](https://hub.docker.com/r/show0k/miniconda-armv7/)
[![Build Status](https://travis-ci.com/show0k/docker-miniconda-armv7.svg?token=q6kB4mpCcVGt4S3NTy9e&branch=master)](https://travis-ci.com/show0k/docker-miniconda-armv7)
[![CircleCI](https://circleci.com/gh/show0k/docker-miniconda-armv7.svg?style=svg)](https://circleci.com/gh/show0k/docker-miniconda-armv7)

Image used to build linux-armv7 conda packages on x64 hardware. 
It **doesn't need** to install qemu on the host, nor to have a kernel which support binfmt_misc.

This image integrate a [modified version of qemu](https://github.com/resin-io/qemu). For more informations on how to mimic the kernel support of binfmt_misc, look at [this](https://resin.io/blog/building-arm-containers-on-any-x86-machine-even-dockerhub/) post or [this one](https://github.com/dockerparis/trusted-cross-build). The image is inspired by [resin/armv7hf-debian-qemu](https://github.com/resin-io-projects/armv7hf-debian-qemu).


## Run it on x86_64 hardware
Every commands are started throw qemu, so you have nothing to do :

`docker run -it --rm show0k/miniconda-armv7 /bin/bash`

## Run it on ARM hardware
You have to override the entrypoint of qemu

`docker run -it --rm --entrypoint=/bin/bash show0k/miniconda-armv7`

## Continuous integration support
It works on Travis Ci and CircleCi ! Look at [.travis.yml](.travis.yml) or [circle.yml](circle.yml) to have basic ci examples.

## Docker build based on this image
Wrap your build steps to taint the environment with qemu allowing building on x86_64.

RUN [ "cross-build-start" ]
RUN echo do buid steps here
RUN [ "cross-build-end" ]
