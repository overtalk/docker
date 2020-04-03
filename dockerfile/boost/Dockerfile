FROM alpine:latest
LABEL maintainer="me"
LABEL description="An environment with Boost C++ Libraries based on Alpine Linux."

ARG BOOST_VERSION=1.72.0
ARG BOOST_DIR=boost_1_72_0
ENV BOOST_VERSION ${BOOST_VERSION}

# Use bzip2-dev package for Boost IOStreams library support of zip and bzip2 formats
# Use openssl package for wget ssl_helper issue
RUN apk add --no-cache --virtual .build-dependencies \
    openssl \
    linux-headers \
    build-base \
    && wget http://downloads.sourceforge.net/project/boost/boost/${BOOST_VERSION}/${BOOST_DIR}.tar.bz2 \
    && tar --bzip2 -xf ${BOOST_DIR}.tar.bz2 \
    && cd ${BOOST_DIR} \
    && ./bootstrap.sh \
    && ./b2 --without-python --prefix=/usr -j 4 link=shared runtime-link=shared install \
    && cd .. && rm -rf ${BOOST_DIR} ${BOOST_DIR}.tar.bz2 \
    && apk del .build-dependencies

RUN apk add build-base
RUN apk add cmake
RUN apk add git

CMD sh
