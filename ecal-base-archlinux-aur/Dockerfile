FROM archlinux
MAINTAINER tobias.borgert@gmail.com

RUN pacman -Syu --noconfirm && \
    pacman -S --noconfirm base-devel && \
    pacman -S --noconfirm git pacman-contrib vim

RUN useradd --uid 1306 --user-group --groups wheel --create-home --shell /bin/bash ecal

RUN sed -i '/ %wheel ALL=(ALL) NOPASSWD: ALL/s/^# //g' /etc/sudoers

USER 1306
RUN mkdir -p /home/ecal/Werkbank/aur/
WORKDIR /home/ecal/Werkbank/aur/
RUN git clone https://aur.archlinux.org/ecal.git
WORKDIR /home/ecal/Werkbank/aur/ecal/
