FROM ubuntu:20.04
MAINTAINER tobias.borgert@gmail.com

ARG DEBIAN_FRONTEND=noninteractive
RUN apt update && \
    apt upgrade -y && \
    apt install -y gnupg2 \
                   ca-certificates \
                   wget \
                   software-properties-common \
                   libssl-dev \
                   build-essential \
                   cmake \
                   git \
                   doxygen \
                   graphviz \
                   build-essential \
                   zlib1g-dev \
                   qt5-default \
                   libhdf5-dev \
                   libprotobuf-dev \
                   libprotoc-dev \
                   protobuf-compiler \
                   libcurl4-openssl-dev

RUN useradd --uid 1306 --user-group --create-home --shell /bin/bash ecal
USER 1306

RUN mkdir -p /home/ecal/Werkbank/c_c++/
WORKDIR /home/ecal/Werkbank/c_c++/
RUN git clone --recursive git://github.com/continental/ecal.git
