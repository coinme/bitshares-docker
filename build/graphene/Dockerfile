FROM ubuntu:16.04
MAINTAINER Fabian Schuh <Fabian@cryptonomex.com>

## Core Utilities
RUN apt-get update
RUN apt-get -y upgrade
RUN apt-get install -y build-essential \
                       gcc-5 \
                       g++-5 \
                       cmake \
                       make \
                       libbz2-dev \
                       libdb++-dev \
                       libdb-dev \
                       libssl-dev \
                       openssl \
                       libreadline-dev \
                       autoconf \
                       libtool \
                       git \
                       autotools-dev \
                       libbz2-dev \
                       libicu-dev \
                       python-dev \
                       wget

## Boost 1.60
WORKDIR /
RUN wget -c 'http://sourceforge.net/projects/boost/files/boost/1.60.0/boost_1_60_0.tar.bz2/download'\
         -O /boost_1_60_0.tar.bz2
RUN tar xjf /boost_1_60_0.tar.bz2
WORKDIR boost_1_60_0/
RUN ./bootstrap.sh "--prefix=/opt/boost_1_60_0"
RUN ./b2 install

## Fetching Graphene
WORKDIR /
RUN git clone https://github.com/cryptonomex/graphene /graphene
WORKDIR /graphene
RUN git submodule update --init --recursive

## Building Graphene
RUN CC=gcc-5 CXX=g++-5 cmake -DBOOST_ROOT="/opt/boost_1_60_0" -DCMAKE_BUILD_TYPE=Release .
RUN make || make -j 1

