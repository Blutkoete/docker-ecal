FROM ubuntu:18.04
MAINTAINER tobias.borgert@gmail.com

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
# eCal requires CMake >= 3.13
WORKDIR /tmp/cmake/
RUN wget https://github.com/Kitware/CMake/releases/download/v3.18.1/cmake-3.18.1.tar.gz && \
    tar -xvzf cmake-3.18.1.tar.gz
WORKDIR /tmp/cmake/cmake-3.18.1/
RUN ./bootstrap && \
    make && \
    make install

RUN useradd --uid 1306 --user-group --create-home --shell /bin/bash ecal
USER 1306

RUN mkdir -p /home/ecal/Werkbank/c_c++/
WORKDIR /home/ecal/Werkbank/c_c++/
RUN git clone --recursive git://github.com/continental/ecal.git
