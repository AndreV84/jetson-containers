# jetson-containers
 # ros1_realsense-cuda
 to build  #from the folder with downloaded Dockerfile:
 
 docker build . -t ros1_realsense_cuda
 
 To run:
 
 docker run -it --rm --net=host --runtime nvidia -e DISPLAY=$DISPLAY --privileged --ipc=host -v /tmp/.X11-unix/:/tmp/.X11-unix/ -v /tmp/argus_socket:/tmp/argus_socket --cap-add SYS_PTRACE realsense_cuda:latest /bin/bash -c '. devel/setup.bash; roslaunch realsense2_camera rs_camera.launch'
can be also executed as just one example either from the container or from system wide folder
