FROM ubuntu:22.04

#COPY data/sources.list /etc/apt/sources.list
COPY data/ruckig-0.9.2.tar.gz /home/

ENV TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
RUN sed -i -e 's/^APT/# APT/' -e 's/^DPkg/# DPkg/' /etc/apt/apt.conf.d/docker-clean
RUN apt-get update
RUN apt-get install -y sudo vim wget build-essential cmake gcc g++ libnlopt-dev libnlopt-cxx-dev python2 python-pip desktop-file-utils

RUN echo 'root:123' | chpasswd

RUN useradd -ms /bin/bash ubuntu
RUN echo 'ubuntu:123' | chpasswd
RUN usermod -aG sudo ubuntu

USER ubuntu
RUN mkdir /home/ubuntu/.pip
COPY data/pip.conf /home/ubuntu/.pip/pip.conf

USER root
RUN echo "deb [trusted=yes arch=amd64] http://deb.repo.autolabor.com.cn jammy main" | sudo tee /etc/apt/sources.list.d/autolabor.list
USER ubuntu
RUN cd /home/ubuntu
RUN echo "123" | sudo -S apt-get update
RUN echo "123" | sudo -S apt-get install -y ros-noetic-autolabor

#LABEL privileged=true
#RUN cd /home/ && tar xzvf ruckig-0.9.2.tar.gz && cd ruckig-0.9.2 && mkdir build && cd build && cmake -DCMAKE_BUILD_TYPE=Release .. && make && make install
RUN echo "source /opt/ros/noetic/setup.bash" >> /home/ubuntu/.bashrc
WORKDIR /home/ubuntu
