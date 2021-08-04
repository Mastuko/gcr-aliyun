FROM mmoy/riscv-latex-python
RUN apt-get update \
    && apt-get install -y curl vim autoconf automake autotools-dev make gcc g++ python3 python3-dev python3-pip gtkwave
RUN pip3 install cocotb pytest pyelftools
RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh \
    && rustup install nightly \
    && cargo +nightly install racer \
    && cargo install --force rustfmt \
    && cargo install --force rls \
    && rustup component add rls-preview \
    && rustup component add rust-analysis \
    && rustup component add rust-src
    
