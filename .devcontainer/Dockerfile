# See here for image contents: https://github.com/microsoft/vscode-dev-containers/tree/v0.166.1/containers/ubuntu/.devcontainer/base.Dockerfile

# [Choice] Ubuntu version: focal, jammy
ARG VARIANT="focal"
FROM mcr.microsoft.com/vscode/devcontainers/base:0-${VARIANT}

RUN apt-get update \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
    bash \
    build-essential \
    gdb \
    gcc \
    emacs \
    vim \
    nano \
    qemu \
    wget \
    xorg-dev \
    libncursesw5 \
    libncurses5-dev \
    dos2unix \
    expect \
    rsync \
    clang-format \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

RUN mkdir -p /pintos/src
COPY ./src /pintos/src

ENV PINTOS_HOME=/pintos
ENV PATH=/pintos/src/utils:$PATH

WORKDIR /pintos

RUN cd /pintos/src/misc && \
    wget --no-check-certificate https://sourceforge.net/projects/bochs/files/bochs/2.6.11/bochs-2.6.11.tar.gz && \
    env SRCDIR=/pintos/src/misc PINTOSDIR=/pintos DSTDIR=/usr/local sh ./bochs-2.6.11-build.sh /usr/local && \
    rm -f bochs-2.6.11.tar.gz

# Build only setitimer-helper (squish-pty/squish-unix need deprecated stropts.h)
RUN cd /pintos/src/utils && make setitimer-helper && cp setitimer-helper /usr/local/bin/

# RUN cd /pintos/src/threads && make

CMD ["bash"]
