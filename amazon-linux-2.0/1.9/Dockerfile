FROM amazonlinux:2

MAINTAINER Brett Hazen <brett@javajolt.com>

# Stolen from https://hub.docker.com/r/bitwalker/centos7-elixir/dockerfile

# Important!  Update this no-op ENV variable when this Dockerfile
# is updated with the current date. It will force refresh of all
# of the base images and things like `apt-get update` won't be using
# old cached versions when the Dockerfile is built.
ENV REFRESHED_AT=2020-01-20 \
    LANG=en_US.UTF-8 \
    HOME=/opt/app/ \
    # Set this so that CTRL+G works properly
    TERM=xterm \
    ERL_VERSION=22.2.2 \
    ELIXIR_VERSION=1.9.4

WORKDIR ${HOME}

# Install Erlang
RUN \
    mkdir -p /tmp && \
    yum install -y -q wget unzip make ncurses-compat-libs.x86_64 && \
    wget --no-verbose -P /tmp https://dl.fedoraproject.org/pub/epel/7/x86_64/Packages/e/epel-release-7-12.noarch.rpm && \
    yum install -q -y /tmp/epel-release-7-12.noarch.rpm && \
    yum update -y -q && \
    yum upgrade -y -q --enablerepo=epel && \
    yum install -y -q wxGTK-devel unixODBC-devel && \
    wget --no-verbose -P /tmp/ "https://packages.erlang-solutions.com/erlang/rpm/centos/7/x86_64/esl-erlang_${ERL_VERSION}-1~centos~7_amd64.rpm" && \
    rpm -Uvh "/tmp/esl-erlang_${ERL_VERSION}-1~centos~7_amd64.rpm" && \
    wget --no-verbose -P /tmp/ "https://github.com/elixir-lang/elixir/releases/download/v${ELIXIR_VERSION}/Precompiled.zip" && \
    unzip /tmp/Precompiled.zip -d /usr/local && \
    rm /tmp/Precompiled.zip && \
    mix local.rebar --force && \
    mix local.hex --force

CMD ["/bin/bash"]
