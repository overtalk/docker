# FROM gcc:8

# RUN wget https://github.com/Kitware/CMake/releases/download/v3.15.5/cmake-3.15.5-Linux-x86_64.sh \
#     -q -O /tmp/cmake-install.sh \
#     && chmod u+x /tmp/cmake-install.sh \
#     && mkdir /usr/bin/cmake \
#     && /tmp/cmake-install.sh --skip-license --prefix=/usr/bin/cmake \
#     && rm /tmp/cmake-install.sh

# ENV PATH="/usr/bin/cmake/bin:${PATH}"

# ARG BOOST_VERSION=1.72.0
# ARG BOOST_DIR=boost_1_72_0
# ENV BOOST_VERSION ${BOOST_VERSION}

# RUN wget http://downloads.sourceforge.net/project/boost/boost/${BOOST_VERSION}/${BOOST_DIR}.tar.bz2 \
#     && tar --bzip2 -xf ${BOOST_DIR}.tar.bz2 \
#     && cd ${BOOST_DIR} \
#     && ./bootstrap.sh \
#     && ./b2 --without-python --prefix=/usr -j 4 link=shared runtime-link=shared install \
#     && cd .. && rm -rf ${BOOST_DIR} ${BOOST_DIR}.tar.bz2 

# RUN apk add build-base
# RUN apk add cmake
# RUN apk add git

FROM gcc:8

ARG BOOST_VERSION=1.72.0
ARG BOOST_DIR=boost_1_72_0
ARG PROTOBUF_VERSION=3.6.1
ARG CMAKE_VERSION=3.15.5

ENV BOOST_VERSION ${BOOST_VERSION}
ENV PROTOBUF_VERSION ${PROTOBUF_VERSION}
ENV CMAKE_VERSION ${CMAKE_VERSION}

# install protobuf
RUN wget https://github.com/protocolbuffers/protobuf/releases/download/v${PROTOBUF_VERSION}/protobuf-all-${PROTOBUF_VERSION}.tar.gz \
    && tar -zxvf ./protobuf-all-${PROTOBUF_VERSION}.tar.gz \
    && cd ./protobuf-${PROTOBUF_VERSION} \
    && ./configure \
    && make \
    && make check \
    && make install \
    && ldconfig \
    && cd ..

# install boost
RUN wget http://downloads.sourceforge.net/project/boost/boost/${BOOST_VERSION}/${BOOST_DIR}.tar.bz2 \
    && tar --bzip2 -xf ${BOOST_DIR}.tar.bz2 \
    && cd ${BOOST_DIR} \
    && ./bootstrap.sh \
    && ./b2 --without-python --prefix=/usr -j 4 link=shared runtime-link=shared install \
    && cd .. \
    && rm -rf ${BOOST_DIR} ${BOOST_DIR}.tar.bz2

# install cmake
RUN wget https://github.com/Kitware/CMake/releases/download/v${CMAKE_VERSION}/cmake-${CMAKE_VERSION}-Linux-x86_64.sh \
    -q -O /tmp/cmake-install.sh \
    && chmod u+x /tmp/cmake-install.sh \
    && mkdir /usr/bin/cmake \
    && /tmp/cmake-install.sh --skip-license --prefix=/usr/bin/cmake \
    && rm /tmp/cmake-install.sh \
    && cd ..

ENV PATH="/usr/bin/cmake/bin:${PATH}"
