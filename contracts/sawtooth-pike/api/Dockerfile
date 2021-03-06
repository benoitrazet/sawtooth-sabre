# Copyright 2018 Cargill Incorporated
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

FROM rustlang/rust:nightly

# Temp fix to be able to build diesel on nightly
RUN rustup override set nightly-2018-05-15

RUN cargo install diesel_cli --no-default-features --features postgres

RUN apt-get update && apt-get install -y unzip

# Install libzmq

WORKDIR /
RUN curl -OLsS https://github.com/zeromq/libzmq/releases/download/v4.2.3/zeromq-4.2.3.tar.gz
RUN tar -xvf zeromq-4.2.3.tar.gz
RUN bash -c "cd zeromq-4.2.3 && \
    ./autogen.sh && \
    ./configure && \
    make check && \
    make install && \
    ldconfig"

# For Building Protobufs
RUN curl -OLsS https://github.com/google/protobuf/releases/download/v3.5.1/protoc-3.5.1-linux-x86_64.zip \
 && unzip protoc-3.5.1-linux-x86_64.zip -d protoc3 \
 && rm protoc-3.5.1-linux-x86_64.zip
ENV PATH=/protoc3/bin:$PATH

WORKDIR /project/api
