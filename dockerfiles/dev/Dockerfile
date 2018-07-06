FROM ubuntu:18.04

RUN apt-get update && \
    apt-get install --no-install-recommends -y \
    ca-certificates curl file \
    libssl-dev \
    pkg-config \
    sudo \
    && rm -rf /var/lib/apt/lists/*

RUN apt-get update && \
    apt-get install --no-install-recommends -y \
    qtcreator ninja-build make cmake g++ extra-cmake-modules \
    kdesdk-scripts \
    gdb valgrind git \
    qtdeclarative5-dev-tools qtdeclarative5-dev qtquickcontrols2-5-dev \
    libqt5charts5-dev libqt5svg5-dev qml-module-qtcharts \
    qt5-doc qtbase5-doc qtcharts5-doc qtcreator-doc qtquickcontrols2-5-doc \
    qtquickcontrols5-doc qtsvg5-doc qttools5-doc \
    qmlscene \
    && rm -rf /var/lib/apt/lists/*

ADD ./bin/rust_qt_binding_generator /usr/bin/

# Once all the package/lib installs are complete, configure the local user
# and switch to userland.
ARG DEVELOPER_UID
ARG DEVELOPER_GID

# Make a user and group to match the user running the build
RUN groupadd -g ${DEVELOPER_GID} developer \
    && useradd -u ${DEVELOPER_UID} \
               -g ${DEVELOPER_GID} \
               -G users \
               -G sudo \
               --create-home developer \
    && echo "developer ALL=(ALL) NOPASSWD:ALL" > /etc/sudoers.d/00-developer

# !!! Anything requiring root should happen before this point.
USER developer

ARG RUST_TOOLCHAIN=1.27.0

RUN curl https://sh.rustup.rs -sSf | sh -s -- \
  --default-toolchain $RUST_TOOLCHAIN -y

RUN /home/developer/.cargo/bin/rustup target add x86_64-pc-windows-gnu

VOLUME /code
WORKDIR /code

