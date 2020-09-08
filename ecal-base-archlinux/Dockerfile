FROM archlinux
MAINTAINER tobias.borgert@gmail.com

RUN pacman -Syu --noconfirm && \
    pacman -S --noconfirm base-devel && \
    pacman -S --noconfirm git pacman-contrib vim && \
    pacman -S --noconfirm cmake curl doxygen git graphviz hdf5 protobuf qt5-base

RUN useradd --uid 1306 --user-group --groups wheel --create-home --shell /bin/bash ecal

RUN sed -i '/ %wheel ALL=(ALL) NOPASSWD: ALL/s/^# //g' /etc/sudoers

USER 1306
RUN mkdir -p /home/ecal/Werkbank/c_c++/
WORKDIR /home/ecal/Werkbank/c_c++/
RUN git clone https://github.org/continental/ecal.git
WORKDIR /home/ecal/Werkbank/c_c++/ecal/
