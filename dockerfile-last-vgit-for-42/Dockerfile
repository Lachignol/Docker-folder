FROM ubuntu:22.04

RUN apt-get update && apt-get install -y \
    build-essential \
    autoconf \
    automake \
    libssl-dev \
    libcurl4-openssl-dev \
    libexpat1-dev \
    gettext \
    wget \
    ca-certificates \
    zlib1g-dev \
    sudo

# Créer un utilisateur non-root
RUN useradd -m -s /bin/bash usergit && echo "usergit ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

USER usergit
ENV HOME=/home/usergit
WORKDIR /home/usergit

# Télécharger et extraire Git 2.51.0
RUN wget https://github.com/git/git/archive/refs/tags/v2.51.0.tar.gz -O git.tar.gz && \
    tar -xzf git.tar.gz && rm git.tar.gz

WORKDIR /home/usergit/git-2.51.0

# Compiler et installer Git dans $HOME/.local avec options openssl et curl
RUN make configure && \
    ./configure --prefix=$HOME/.local --with-openssl --with-curl && \
    make clean && make -j$(nproc) && make install && \
    mkdir -p $HOME/.local/share/git-core/templates && \
    cp -r /home/usergit/git-2.51.0/templates/* $HOME/.local/share/git-core/templates/

ENV PATH=$HOME/.local/bin:$PATH
ENV GIT_EXEC_PATH=$HOME/.local/libexec/git-core

RUN git --version

CMD ["git", "--version"]

