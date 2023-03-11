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
FROM ubuntu:22.04

ENV PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
ENV DEBIAN_FRONTEND=noninteractive 

RUN apt-get update -y --fix-missing && \
    apt-get -y upgrade

RUN apt-get install -y apt-utils apt-file && \
    apt-get install -y software-properties-common

RUN apt-get install -y kmod make gcc wget && \
    apt-get install -y fuse sudo && \
    apt-get install -y file unzip && \
    apt-get install -y cmake gcc && \
    apt-get install -y cmake ninja-build pkg-config clang clang-format build-essential curl ccache git

RUN apt-get install -y libavcodec-dev libavdevice-dev libavfilter-dev libavformat-dev libavutil-dev libswresample-dev \
    libswscale-dev libx264-dev libcurl4-openssl-dev libmbedtls-dev libgl1-mesa-dev libjansson-dev libluajit-5.1-dev \
    python3-dev libx11-dev libxcb-randr0-dev libxcb-shm0-dev libxcb-xinerama0-dev libxcb-composite0-dev libxcomposite-dev \
    libxinerama-dev libxcb1-dev libx11-xcb-dev libxcb-xfixes0-dev swig libcmocka-dev libxss-dev libglvnd-dev libgles2-mesa \
    libgles2-mesa-dev libwayland-dev libpci-dev 

# libsrt-dev
# libsrt-openssl-dev

RUN apt-get install -y qtbase5-dev qtbase5-private-dev libqt5svg5-dev qtwayland5 
# && \
#     apt-get install -y qt6-base-dev qt6-base-private-dev libqt6svg6-dev qt6-wayland
#  && \
# apt-get install -y libnss3-dev libnss3 libnspr4 libpipewire-0.3-dev

RUN apt-get install -y libasound2-dev libfdk-aac-dev libfontconfig-dev libfreetype6-dev libjack-jackd2-dev libpulse-dev \
    libsndio-dev libspeexdsp-dev libudev-dev libv4l-dev libva-dev libvlc-dev libdrm-dev



RUN wget --output-document="/tmp/librist.deb" https://github.com/tsduck/rist-installer/releases/download/v0.2.7/librist_0.2.7.ubuntu21_amd64.deb
RUN dpkg -i /tmp/librist.deb || true
RUN apt-get -fy install

# RUN mkdir --parents /root/build/obsstudio && \
#     git clone --recursive https://github.com/obsproject/obs-studio.git /root/build/obsstudio

RUN mkdir --parents /root/build/cef_binary && \
    wget --output-document="/tmp/cef_binary.tar.bz2" https://cdn-fastly.obsproject.com/downloads/cef_binary_5060_linux64.tar.bz2 && \
    tar -xjf /tmp/cef_binary.tar.bz2 -C /root/build/cef_binary



