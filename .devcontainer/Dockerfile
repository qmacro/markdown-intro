# syntax=docker/dockerfile:1

ARG VARIANT="20"
FROM --platform=linux/amd64 mcr.microsoft.com/vscode/devcontainers/javascript-node:${VARIANT}
ARG CAPVER="latest"

# Install some generally useful tools
RUN apt-get update \
    && apt-get -y install --no-install-recommends \
    curl git sqlite3 entr source-highlight

USER node
RUN mkdir -p $HOME/.local/bin/
RUN curl \
    --location \
    --url https://github.com/charmbracelet/glow/releases/download/v2.1.0/glow_2.1.0_Linux_x86_64.tar.gz \
    | tar \
      --directory $HOME/.local/bin \
      --strip-components 1 \
      --file - \
      --extract \
      --gunzip \
      glow_2.1.0_Linux_x86_64/glow
  
RUN curl \
    --location \
    --url https://github.com/maaslalani/slides/releases/download/v0.9.0/slides_0.9.0_linux_amd64.tar.gz \
    | tar \
      --directory $HOME/.local/bin \
      --file - \
      --extract \
      --gunzip \
      slides

# vi mode everywhere and nicer prompt KTHXBAI
RUN cat <<EOBASHRC >> /home/node/.bashrc
export EDITOR=vi
set -o vi
bind -x '"\C-l": clear'
export PATH=$PATH:$HOME/.local/bin
EOBASHRC

RUN echo 'export PS1=${PS1/\$ /\\\\n$ }' >> /home/node/.bashrc

# Ready!
WORKDIR /home/node
