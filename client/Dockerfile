FROM debian:12

ENV DEBIAN_FRONTEND=noninteractive
ENV RUSTUP_HOME=/usr/local/rustup \
    CARGO_HOME=/usr/local/cargo \
    PATH=/usr/local/cargo/bin:$PATH

RUN apt-get update && \
    apt-get install -y \
        curl \
        build-essential \
        clang \
        cmake \
        libclang-dev \
        llvm-dev \
        net-tools \
        libxkbcommon-x11-0 \
        git \
        tor \
        xterm \
        pkg-config \
        iputils-ping \
        libglib2.0-dev \
        libssl-dev \
        libgtk-3-dev \
        dnsutils

RUN curl https://sh.rustup.rs -sSf | sh -s -- -y

RUN git clone https://git.disroot.org/Amnezichat/Amnezichat_TUI.git /opt/Amnezichat_TUI

WORKDIR /opt/Amnezichat_TUI/client
RUN cargo build --release

CMD bash -c "\
    if pgrep -x tor > /dev/null; then \
        echo 'Killing existing Tor process...'; \
        pkill -x tor; \
        sleep 1; \
    fi; \
    cargo run --release"
