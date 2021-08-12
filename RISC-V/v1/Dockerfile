From ubuntu:xenial

MAINTAINER mastuko <wqh21@mails.tsinghua.edu.cn>

# Install neccessary library
RUN apt-get update \
    && apt-get install -y git \
    autoconf \
    automake \
    autotools-dev \
    curl \
    python3 \
    libmpc-dev \
    libmpfr-dev \
    libgmp-dev \
    libusb-1.0-0-dev \
    gawk \
    build-essential \
    bison \
    flex \
    texinfo \
    gperf \
    libtool \
    patchutils \
    bc \
    zlib1g-dev \
    libexpat-dev \
    device-tree-compiler \
    pkg-config \
    2>&1 >/dev/null
    
# Set ENV
ENV RISCV /opt/riscv
RUN mkdir -p $RISCV
ENV PATH $RISCV/bin:$PATH
WORKDIR $RISCV
RUN git clone https://github.com/riscv/riscv-tools.git && \
  cd riscv-tools && git submodule update --init --recursive

WORKDIR $RISCV/riscv-tools

RUN git clone https://github.com/riscv/riscv-gnu-toolchain \
    && cd $RISCV/riscv-tools/riscv-gnu-toolchain \
    && sed -i 's/= git/= https/' .gitmodules
    
WORKDIR $RISCV/riscv-tools/riscv-gnu-toolchain

RUN ./configure --prefix=$RISCV \
    && make linux
    
WORKDIR $RISCV/riscv-tools
RUN ls $RISCV && ./build.sh



    
