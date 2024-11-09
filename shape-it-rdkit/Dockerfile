FROM debian:bullseye
LABEL maintainer="Dave Wright<david.wright@kuano.ai>"

RUN apt-get update && apt-get -y install --no-install-recommends\
  build-essential\
  ca-certificates\
  cmake\
  git\
  libboost-dev\
  libboost-program-options-dev\
  libboost-iostreams-dev\
  libboost-regex-dev\
  python3-dev\
  librdkit-dev\
  python3-rdkit\
  libboost-python-dev\
  wget &&\
  apt-get clean -y

# Fails to build with python bindings but don't need them at the minute,
# so leaving this way for now.

WORKDIR /root
RUN mkdir opt
RUN git clone https://github.com/rdkit/shape-it.git &&\
  cd shape-it &&\
  mkdir build &&\
  cd build &&\
  #cmake -DCMAKE_INSTALL_PREFIX=/root/opt -DBUILD_RDKIT_SUPPORT=ON -DBUILD_PYTHON_SUPPORT=ON -DRDKIT_INCLUDE_DIR=/usr/include/rdkit -DBoost_INCLUDE_DIR=/usr/include .. &&\
  cmake -DCMAKE_INSTALL_PREFIX=/root/opt -DBUILD_RDKIT_SUPPORT=ON -DRDKIT_INCLUDE_DIR=/usr/include/rdkit .. &&\
  make -j $(( nproc > 2 ? nproc - 2 : 1 )) &&\
  make install
ENV PATH="/root/opt/bin/:$PATH"

WORKDIR /share
ENTRYPOINT ["shape-it"]
