FROM mmoy/riscv-latex-python
RUN apt-get update \
    && apt-get install -y curl vim autoconf automake autotools-dev make gcc g++ python3 python3-dev python3-pip gtkwave \
    && pip3 install cocotb pytest pyelftools \
    && /bin/bash -c "curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y"
ENV PATH=$PATH:$HOME/.cargo/bin
RUN /bin/bash -c 'source $HOME/.cargo/env; echo $HOME'
RUN /bin/bash -c '/root/.cargo/bin/rustup self update' \
    && /bin/bash -c '/root/.cargo/bin/rustup install nightly' \
    && /bin/bash -c '/root/.cargo/bin/cargo +nightly install racer' \
    && /bin/bash -c '/root/.cargo/bin/cargo install --force rustfmt' \
    && /bin/bash -c '/root/.cargo/bin/cargo install --force rls' \
    && /bin/bash -c '/root/.cargo/bin/rustup component add rls-preview' \
    && /bin/bash -c '/root/.cargo/bin/rustup component add rust-analysis' \
    && /bin/bash -c '/root/.cargo/bin/rustup component add rust-src'
