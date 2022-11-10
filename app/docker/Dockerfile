# Copyright 2020 Alex Woroschilow (alex.woroschilow@gmail.com)
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
# http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
FROM ubuntu:20.04
ENV DEBIAN_FRONTEND=noninteractive 

ENV PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

RUN apt-get update -y --fix-missing
RUN apt-get -y upgrade

RUN apt-get install -y apt-utils
RUN apt-get install -y software-properties-common

RUN apt-get install -y kmod make gcc wget
RUN apt-get install -y fuse
RUN apt-get install -y file unzip
RUN apt-get install -y cmake gcc

RUN add-apt-repository ppa:obsproject/obs-studio
RUN apt-get update -y --fix-missing
