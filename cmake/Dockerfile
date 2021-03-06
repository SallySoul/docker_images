FROM ubuntu

RUN apt-get update --fix-missing \
&&  apt-get upgrade -y \
&&  DEBIAN_FRONTEND=noninteractive apt-get install -y \
    wget \
    software-properties-common \
    make \
    build-essential \
    clang-tidy \
    iwyu \
    cppcheck \
    doxygen \
    graphviz \
    libopenmpi-dev \
    openmpi-bin \
    google-perftools \
    libgoogle-perftools-dev \
    lldb \
    valgrind \
&&  rm -rf /var/cache/apt/archives/* /var/lib/apt/lists/*

RUN wget -O - https://apt.llvm.org/llvm-snapshot.gpg.key | apt-key add - && \
    apt-add-repository "deb http://apt.llvm.org/bionic/ llvm-toolchain-bionic-8 main" && \
    apt-get update --fix-missing && \
    apt-get install -y clang-8 && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

ARG CMAKE_MAJOR_VERSION=3.14
ARG CMAKE_MINOR_VERSION=1
ARG CMAKE_VERSION=$CMAKE_MAJOR_VERSION.$CMAKE_MINOR_VERSION

RUN cd /tmp \
    && wget https://cmake.org/files/v$CMAKE_MAJOR_VERSION/cmake-$CMAKE_VERSION.tar.gz \
    && tar xf cmake-$CMAKE_VERSION.tar.gz \
    && cd cmake-$CMAKE_VERSION \
    && ./bootstrap \
    && make -j $(cat /proc/cpuinfo | grep processor | wc -l) \
    && make install \
    && cd .. \
    && rm -rf cmake*

ENV CC clang-8
ENV CXX clang++-8
ENV MPI_C mpicc
ENV MPI_CXX mpicxx

RUN mkdir /app
WORKDIR /app
