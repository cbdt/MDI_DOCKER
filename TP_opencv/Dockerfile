FROM ubuntu:18.04

RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y git

RUN git clone -b 3.4 https://github.com/opencv/opencv.git
WORKDIR /opencv

RUN apt-get install -y build-essential && \
    apt-get install -y cmake libgtk2.0-dev pkg-config libavcodec-dev libavformat-dev libswscale-dev && \
    apt-get install -y python-dev python-numpy libtbb2 libtbb-dev libjpeg-dev libpng-dev libtiff-dev libdc1394-22-dev

# Install OpenJDK-8
RUN apt-get update && \
    apt-get install -y openjdk-8-jdk && \
    apt-get install -y ant && \
    apt-get clean;

# Fix certificate issues
RUN apt-get update && \
    apt-get install -y ca-certificates-java && \
    apt-get clean && \
    update-ca-certificates -f;

ENV JAVA_HOME /usr/lib/jvm/java-8-openjdk-amd64/
RUN export JAVA_HOME

RUN mkdir build && cd build && cmake -DBUILD_SHARED_LIBS=OFF .. && make -j8

VOLUME /opencv/build

# docker run -t -i -v exec/tmp/:/tmp/data -v <container_id>:/opencv ubuntu /bin/bash
# run cp -r /opencv/ /tmp/data
# opencv build folder is now on local machine