FROM python:3.10-slim-bookworm

ENV DEBIAN_FRONTEND=noninteractive

# Docker in Docker
RUN apt-get update -qqy && apt-get install -qqy \
    apt-transport-https \
    ca-certificates \
    curl \
    lxc \
    iptables
RUN curl -sSL https://get.docker.com/ | sh

# Python package dependencies
RUN apt-get -yq update && \
    apt-get -yq install \
        build-essential=12.9 \
        cmake=3.25.1-1 \
        curl=7.88.1-10+deb12u6 \
        default-jdk=2:1.17-74 \
        git-lfs=3.3.0-1+b5 \
        libatlas3-base=3.10.3-13 \
        libblas-dev=3.11.0-2 \
        libfreetype-dev=2.12.1+dfsg-5+deb12u3 \
        libhdf5-dev=1.10.8+repack1-1 \
        libjpeg-dev=1:2.1.5-2 \
        libopenblas-dev=0.3.21+ds-4 \
        pkg-config=1.8.1-1 \
        swig=4.1.0-0.2 \
        unzip=6.0-28 \
        zlib1g-dev=1:1.2.13.dfsg-1
# build-essential - tornado
# cmake - lightgbm (older, non-wheel version)
# curl - Auto-WEKA
# default-jdk - Auto-WEKA
# libatlas3-base - Auto-WEKA
# libblas-dev - N/A
# libfreetype-dev - matplotlib (older, non-wheel version)
# libhdf5-dev - Keras
# libjpeg-dev - Pillow (older, non-wheel version)
# libopenblas-dev - Auto-WEKA
# pkg-config - matplotlib (older, non-wheel version)
# swig - auto-sklearn
# unzip - Auto-WEKA
# zlib - Pillow (older, non-wheel version)

ADD requirements.txt /tmp/requirements.txt
RUN pip3 install --disable-pip-version-check --no-cache-dir -r /tmp/requirements.txt && \
    rm /tmp/requirements.txt

# Auto-WEKA
ARG TARGETARCH
RUN useradd -s /bin/bash -m -d /home/user user
USER user
WORKDIR /home/user

RUN curl -L -O http://prdownloads.sourceforge.net/weka/weka-3-9-6.zip && \
    unzip weka-3-9-6.zip && \
    rm weka-3-9-6.zip && \
    unzip /home/user/weka-3-9-6/weka.jar arpack_combined.jar core.jar mtj.jar
ENV CLASSPATH="${CLASSPATH}:/home/user/weka-3-9-6/weka.jar:/home/user/arpack_combined.jar:/home/user/core.jar:/home/user/mtj.jar"

RUN java weka.core.WekaPackageManager -install-package netlibNativeLinux
RUN find /home/user/wekafiles/packages/netlibNativeLinux/lib/ && \
    (find /home/user/wekafiles/packages/netlibNativeLinux/lib/ -name "*aarch64*" -print0 | xargs -0 -I {} /bin/bash -c 'cp "{}" "$(echo "{}" | sed "s/aarch64/arm64/")"') && \
    (find /home/user/wekafiles/packages/netlibNativeLinux/lib/ -name "*x86_64*" -print0 | xargs -0 -I {} /bin/bash -c 'cp "{}" "$(echo "{}" | sed "s/x86_64/amd64/")"') && \
    (find /home/user/wekafiles/packages/netlibNativeLinux/lib/ -name "*i686*" -print0 | xargs -0 -I {} /bin/bash -c 'cp "{}" "$(echo "{}" | sed "s/i686/386/")"') && \
    find /home/user/wekafiles/packages/netlibNativeLinux/lib/ 
ENV CLASSPATH="${CLASSPATH}:/home/user/wekafiles/packages/netlibNativeLinux/lib/jniloader-1.2.jar:/home/user/wekafiles/packages/netlibNativeLinux/lib/native_system-java-1.2.jar:/home/user/wekafiles/packages/netlibNativeLinux/lib/netlib-native_system-linux-${TARGETARCH}-1.2-natives.jar:/home/user/wekafiles/packages/netlibNativeLinux/lib/native_ref-java-1.2.jar:/home/user/wekafiles/packages/netlibNativeLinux/lib/netlib-native_ref-linux-${TARGETARCH}-1.2-natives.jar"

RUN java weka.core.WekaPackageManager -install-package Auto-WEKA
ENV CLASSPATH="${CLASSPATH}:/home/user/wekafiles/packages/Auto-WEKA/autoweka.jar"

USER root
