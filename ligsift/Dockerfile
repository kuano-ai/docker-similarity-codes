FROM debian:buster
LABEL maintainer="Dave Wright<david.wright@kuano.ai>"

RUN echo 'deb http://deb.debian.org/debian experimental main' >> /etc/apt/sources.list

RUN apt-get update -y && apt-get upgrade -y &&\
 apt-get install -y --no-install-recommends zip unzip libxml2 &&\
 apt-get install -y build-essential &&\
 apt-get install -y -t experimental libopenbabel5 openbabel python-openbabel libopenbabel-dev &&\
 apt-get clean

WORKDIR /home
COPY LIGSIFT-master.zip .
RUN unzip LIGSIFT-master.zip
WORKDIR /home/LIGSIFT-master
COPY edited-Makefile Makefile
RUN make
ENV PATH="/home/LIGSIFT-master:$PATH"
WORKDIR /share
ENTRYPOINT ["LIGSIFT"]
