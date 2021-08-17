From ubuntu:16.04

ENV PATH /usr/bin:$PATH
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
    libexpat-dev \
    2>&1 >/dev/null

# Set ENV
ENV RISCV /opt/riscv
RUN mkdir -p $RISCV
ENV PATH $PATH:$RISCV/bin
WORKDIR $RISCV
RUN git clone https://github.com/riscv/riscv-tools.git && \
    cd riscv-tools && \
    git submodule update --init --recursive && \
    cd $RISCV/riscv-tools && \
    git clone https://github.com/riscv/riscv-gnu-toolchain && \
    cd $RISCV/riscv-tools/riscv-gnu-toolchain && \
    sed -i 's/= git/= https/' .gitmodules && \
    cd $RISCV/riscv-tools/riscv-gnu-toolchain && \
    mkdir -p $RISCV/riscv64-gnu-toolchain && \
    ./configure --prefix=$RISCV/riscv64-gnu-toolchain && \
    make

ENV PATH $PATH:$RISCV/riscv64-gnu-toolchain
ENV PATH $PATH:$RISCV/riscv64-gnu-toolchain/bin

# RUN mkdir -p $RISCV/riscv32-gnu-toolchain \
#     && ./configure --prefix=$RISCV/riscv32-gnu-toolchain --with-arch=rv32gc --with-abi=ilp32d \
#     && make linux

# ENV PATH $RISCV/riscv32-gnu-toolchain:$PATH
# ENV PATH $RISCV/riscv32-gnu-toolchain/bin:$PATH
# ENV PATH $RISCV/riscv32-gnu-toolchain/riscv32-unknown-linux-gnu/bin:$PATH

WORKDIR $RISCV/riscv-tools
RUN cd riscv-pk && \
    git checkout master && \
    cd ../riscv-tests && \
    git checkout master && \
    cd env && \
    git checkout master && \
    cd .. \
    cd ../riscv-isa-sim && \
    git checkout master && \
    cd ../riscv-openocd && \
    git checkout riscv && \
    cd .. && \
    ./build.sh && \
    rm -rf $RISCV/riscv-tools/
WORKDIR $RISCV
