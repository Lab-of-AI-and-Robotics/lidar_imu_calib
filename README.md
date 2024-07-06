# lidar_imu_calib

### overview

when develop slam based on 3D lidar, we often use imu to provide priori for matching algorithm(icp, ndt), so the transform between lidar and imu need to be calibrated.For matching algorithm, attitude in transfom is more important than position in transform, and position often be set to 0. So this repo concentrate on calibrate attitude component in transform between lidar and imu.

### Modified
- Result extrinsic parameters
   - The original repo only shows imu to lidar extrinsic parameters.
   - This code shows both imu to lidar and lidar to imu extrinsic parameters as the calibration results.
   - **Note that for LIO-SAM, we need lidar to imu extrinsic parameters**
- Launch file

### prerequisite 

- [ROS](http://wiki.ros.org/kinetic/Installation/Ubuntu)
### compile
```
mkdir -p catkin_ws/src   
cd catkin_ws/src
git clone https://github.com/chennuo0125-HIT/lidar_imu_calib.git
cd ..
catkin_make -DCATKIN_WHITELIST_PACKAGES="ndt_omp;lidar_imu_calib"
```
### run step

1. use rosbag tool record imu and lidar data

   ```
   rosbag record /imu /lidar_points
   ```

2. config launch file

   ```
   lidar_topic: lidar data topic name
   imu_topic: imu data topic name
   bag_file: *.bag file record imu and lidar data topic
   ```


3. start

   ```bash
   roslaunch lidar_imu_calib calib_exR_lidar2imu.launch \
   bag_file:=<path of the bag file> \
   lidar_topic:=<lidar topic name> \
   imu_topic:=<imu topic name>
   ```
### reference
[https://blog.csdn.net/weixin_37835423/article/details/110672571](https://blog.csdn.net/weixin_37835423/article/details/110672571)
   
