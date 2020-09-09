ARG OS
ARG ARCH
FROM blutkoete/ecal-base:latest-${OS}-${ARCH}
MAINTAINER tobias.borgert@gmail.com

WORKDIR /home/ecal/Werkbank/c_c++/ecal
ARG TAG
RUN git checkout ${TAG}
RUN mkdir -p /home/ecal/Werkbank/c_c++/ecal/_build 
WORKDIR /home/ecal/Werkbank/c_c++/ecal/_build
RUN cmake .. -DCMAKE_BUILD_TYPE=Release -DECAL_THIRDPARTY_BUILD_PROTOBUF=OFF -DECAL_THIRDPARTY_BUILD_CURL=OFF -DECAL_THIRDPARTY_BUILD_HDF5=OFF -DCMAKE_INSTALL_PREFIX=/usr -DCMAKE_INSTALL_SYSCONFDIR=/etc && \
    make -j4

USER 0
RUN make install

USER 1306
WORKDIR /home/ecal
