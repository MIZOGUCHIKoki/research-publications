FROM --platform=linux/amd64 archlinux:latest

RUN echo "DisableSandbox" >> /etc/pacman.conf
RUN pacman -Syu --noconfirm

RUN pacman -S tamarin-prover --noconfirm

ENV MAUDE_LIB=/usr/share/maude
RUN echo 'export MAUDE_LIB=/usr/share/maude' >> /etc/profile
WORKDIR /home/tamarin