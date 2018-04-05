FROM ubuntu:16.04

ENV DEBIAN_FRONTEND noninteractive
ENV USER root

RUN apt-get update && \
    apt install -y xfce4 xfce4-goodies && \
    apt-get install -y tightvncserver && \
    mkdir /root/.vnc

ADD xstartup /root/.vnc/xstartup
RUN chmod 755 /root/.vnc/xstartup

ADD passwd /root/.vnc/passwd
RUN chmod 600 /root/.vnc/passwd

RUN mkdir -p /var/lib/samba/usershares/

RUN adduser --quiet --disabled-password --shell /bin/bash --home /home/newuser --gecos "User" guacadmin 

RUN echo guacadmin:guacadmin | chpasswd

# RUN echo 'startxfce4 &' | tee -a .vnc/xstartup

CMD /usr/bin/vncserver :1 -geometry 1280x800 -depth 24 && tail -f /root/.vnc/*:1.log

EXPOSE 5901