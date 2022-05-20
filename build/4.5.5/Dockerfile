FROM debian:bullseye-slim

ARG OPENCV_VERSION=4.5.5
ARG DEBIAN_FRONTEND=noninteractive

ENV build_deps="ca-certificates \
                wget \
                unzip \
                build-essential \
                cmake \
                pkg-config \
                libjpeg-dev \
                libatlas-base-dev \
                libavcodec-dev \
                libavformat-dev \
                libgtk2.0-dev \
                libgtk-3-dev \
                libswscale-dev \
                libtiff-dev \
                libv4l-dev \
                libx264-dev \
                libxvidcore-dev \
                libwebp-dev \
                libpng-dev \
                libavc1394-0 \
                libopenblas-dev \
                libgphoto2-dev"

RUN apt-get update && apt-get -y install --no-install-recommends ${build_deps}

RUN mkdir /tmp/opencv && \
    cd /tmp/opencv && \
    wget -O opencv.zip https://github.com/opencv/opencv/archive/${OPENCV_VERSION}.zip && \
    unzip opencv.zip && \
    wget -O opencv_contrib.zip https://github.com/opencv/opencv_contrib/archive/${OPENCV_VERSION}.zip && \
    unzip opencv_contrib.zip && \
    mkdir /tmp/opencv/opencv-${OPENCV_VERSION}/build && cd /tmp/opencv/opencv-${OPENCV_VERSION}/build && \
    cmake \
    -D CMAKE_BUILD_TYPE=RELEASE \
    -D CMAKE_INSTALL_PREFIX=/usr/local \
    -D OPENCV_EXTRA_MODULES_PATH=/tmp/opencv/opencv_contrib-${OPENCV_VERSION}/modules \
    -D WITH_FFMPEG=NO \
    -D INSTALL_C_EXAMPLES=NO \
    -D INSTALL_PYTHON_EXAMPLES=NO \
    -D BUILD_ANDROID_EXAMPLES=NO \
    -D BUILD_DOCS=NO \
    -D BUILD_TESTS=NO \
    -D BUILD_PERF_TESTS=NO \
    -D BUILD_EXAMPLES=NO \
    -D BUILD_opencv_java=NO \
    -D BUILD_opencv_python=NO \
    -D BUILD_opencv_python2=NO \
    -D BUILD_opencv_python3=NO \
    -D OPENCV_GENERATE_PKGCONFIG=YES .. && \
    make -j4 && \
    make install && \
    cd && rm -rf /tmp/opencv

RUN apt-get remove python3-doc python3-tk python3-venv python3.9-venv python3.9-doc -qy && \
    apt-get clean autoclean && \
    apt-get autoremove --yes && \
    rm -rf /var/lib/{apt,dpkg,cache,log}/

ENV PKG_CONFIG_PATH /usr/local/lib/pkgconfig
ENV LD_LIBRARY_PATH /usr/local/lib
