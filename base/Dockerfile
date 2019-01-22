FROM ubuntu:18.04

RUN apt-get -y update && \
    apt-get -y install apt-utils build-essential curl wget unzip sudo git cmake vim && \
    apt-get -y install mpich libopenblas-dev liblapack-dev libmetis-dev libparmetis-dev libboost-dev gfortran-6 && \
    apt-get -y clean

ENV ELEMENTAL_PATH /usr/local/elemental

ENV OPENBLAS_NUM_THREADS 1

# Install Elemental
RUN cd /root && \
    git clone git://github.com/elemental/Elemental.git && \
    cd Elemental && \
    git checkout 0.87 && \
    mkdir build && \
    cd build && \
    CC=gcc-7 CXX=g++-7 FC=gfortran-7 cmake -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=$ELEMENTAL_PATH .. && \
    nice make -j4  && \
    make install  && \
    cd /root && \
    rm -rf Elemental

ENV ARPACK_PATH /usr/local/arpack

# Install arpack
RUN cd /root && \
    git clone https://github.com/opencollab/arpack-ng && \
    cd arpack-ng && \
    git checkout 3.5.0 && \
    mkdir build && \
    cd build && \
    cmake -DMPI=ON -DBUILD_SHARED_LIBS=ON -DCMAKE_INSTALL_PREFIX=${ARPACK_PATH} .. && \
    nice make -j4 && \
    make install && \
    cd /root && \
    rm -rf arrack-ng

# Install arpackpp
RUN cd /root && \
    git clone https://github.com/m-reuter/arpackpp && \
    cd arpackpp && \
    git checkout 88085d99c7cd64f71830dde3855d73673a5e872b && \
    mkdir build && \
    cd build && \
    cmake -DCMAKE_INSTALL_PREFIX=${ARPACK_PATH} .. && \
    make install && \
    cd /root && \
    rm -rf arpackpp

ENV EIGEN3_PATH /usr/local/eigen3

# Install Eigen
RUN cd /root && \
    curl -L http://bitbucket.org/eigen/eigen/get/3.3.4.tar.bz2 | tar xvfj - && \
    cd eigen-eigen-5a0156e40feb && \
    mkdir build && \
    cd build && \
    cmake -DCMAKE_INSTALL_PREFIX=${EIGEN3_PATH} .. && \
    nice make -j4 && \
    make install && \
    cd /root && \
    rm -rf eigen-eigen-5a0156e40feb

ENV SPDLOG_PATH /usr/local/spdlog

RUN cd /root && \
    git clone https://github.com/gabime/spdlog.git && \
    cd spdlog && \
    mkdir $SPDLOG_PATH && cp -r include/ $SPDLOG_PATH/include/ && \
    cd /root && rm -rf spdlog

ENV ASIO_PATH /usr/local/asio

RUN cd /root && \
    wget -O asio-1.12.1.zip https://sourceforge.net/projects/asio/files/asio/1.12.1%20%28Stable%29/asio-1.12.1.zip/download && \
    unzip asio-1.12.1.zip && \
    cd asio-1.12.1 && ./configure --prefix=$ASIO_PATH && make install -j4 && \
    cd /root && rm -rf asio-1.12.1 asio-1.12.1.zip

ENV LD_LIBRARY_PATH $ELEMENTAL_PATH/lib:$ARPACK_PATH/lib

ENV SYSTEM Linux
