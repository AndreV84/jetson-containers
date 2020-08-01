# jetson-containers
 ## ros1_realsense-cuda
 to build  #from the folder with downloaded Dockerfile:
 
 docker build . -t ros1_realsense_cuda
 
 To run:
 
 xhost +
 
 docker run -it --rm --net=host --runtime nvidia -e DISPLAY=$DISPLAY --privileged --ipc=host -v /tmp/.X11-unix/:/tmp/.X11-unix/ -v /tmp/argus_socket:/tmp/argus_socket --cap-add SYS_PTRACE realsense_cuda:latest /bin/bash -c '. devel/setup.bash; roslaunch realsense2_camera rs_camera.launch'
can be also executed as just one example either from the container or from system wide folder

## ros2_realsense

it is a dashing ros2 with the default realsense sdk retrieved from apt repository; intel might have revoked the repositories from the public access, however, temporarily


## ros1_zed

to build: build . -t ros1_zed

to run:

xhost +

docker run -it --rm --net=host --runtime nvidia -e DISPLAY=$DISPLAY --privileged --ipc=host -v /tmp/.X11-unix/:/tmp/.X11-unix/ -v /tmp/argus_socket:/tmp/argus_socket --cap-add SYS_PTRACE ros1_zed:latest /bin/bash -c '. devel/setup.bash; roslaunch zed_rtabmap_example zed_rtabmap.launch'

docker run -it --rm --net=host --runtime nvidia -e DISPLAY=$DISPLAY --privileged --ipc=host -v /tmp/.X11-unix/:/tmp/.X11-unix/ -v /tmp/argus_socket:/tmp/argus_socket --cap-add SYS_PTRACE ros1_zed:latest /bin/bash -c '. devel/setup.bash;  roslaunch zed_wrapper zed.launch'
