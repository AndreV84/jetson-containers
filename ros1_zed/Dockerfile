FROM nvcr.io/nvidia/l4t-base:r32.4.3
RUN wget --no-check-certificate -O ZED_SDK_Linux_JP.run https://stereolabs.sfo2.cdn.digitaloceanspaces.com/zedsdk/3.2/ZED_SDK_Tegra_JP44_v3.2.1.run &&  chmod +x ZED_SDK_Linux_JP.run ; ./ZED_SDK_Linux_JP.run silent skip_tools && \
rm -rf /usr/local/zed/resources/* \
rm -rf ZED_SDK_Linux_JP.run && \
rm -rf /var/lib/apt/lists/*
# Setup ROS
RUN apt-get update -y && apt install gnupg2 -y && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y tzdata && \
    sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list' && \
    apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654 && \
    apt-get update -y && \
    DEBIAN_FRONTEND=noninteractive apt-get install ros-melodic-ros-base ros-melodic-rviz ros-melodic-rtabmap ros-melodic-rtabmap-ros python-rosinstall python-rosdep python-rosinstall-generator python-wstool build-essential nano \
        cmake usbutils git -y --allow-unauthenticated && \
    rm -rf /var/lib/apt/lists/*

# setup ros env
ENV ROS_WS /home/nvidia/ros_ws

RUN rosdep init && \
  rosdep update --rosdistro melodic && \
  mkdir -p $ROS_WS/src
RUN ln -sf /usr/lib/aarch64-linux-gnu/tegra/libv4l2.so.0 /usr/lib/aarch64-linux-gnu/libv4l2.so

WORKDIR $ROS_WS
RUN cd src ; git clone https://github.com/stereolabs/zed-ros-wrapper.git && git clone https://github.com/stereolabs/zed-ros-examples.git && \
    cd .. ; apt-get update -y && \
    . /opt/ros/melodic/setup.sh && \
    rosdep install --from-paths $ROS_WS/src --ignore-src -r -y && \ 
    rm -rf /var/lib/apt/lists/* && \
    catkin_make -DCMAKE_BUILD_TYPE=Release -DCMAKE_LIBRARY_PATH=/usr/local/cuda/lib64/stubs -DCUDA_CUDART_LIBRARY=/usr/local/cuda/lib64/stubs -DCMAKE_CXX_FLAGS="-Wl,--allow-shlib-undefined"
