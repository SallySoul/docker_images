ARG TAG=latest
FROM ataber/petsc:$TAG

RUN apt-get update --fix-missing \
&&  apt-get upgrade -y --force-yes \
&&  apt-get install -y --force-yes \
    git \
    m4 \
    pkg-config \
&&  apt-get clean \
&&  rm -rf /var/cache/apt/archives/* /var/lib/apt/lists/*

ENV MFEM_DIR /opt/mfem
RUN cd /tmp && \
    git clone https://github.com/mfem/mfem.git && \
    cd mfem && \
    mkdir build && \
    cd build && \
    CXX=mpicxx cmake .. \
        -DCMAKE_INSTALL_PREFIX=$MFEM_DIR \
        -DMFEM_USE_MPI=YES \
        -DBUILD_SHARED_LIBS=1 \
        -DVERBOSE=YES && \
    make -j $(cat /proc/cpuinfo | grep processor | wc -l) && \
    make install && \
    cd /tmp && rm -rf mfem
