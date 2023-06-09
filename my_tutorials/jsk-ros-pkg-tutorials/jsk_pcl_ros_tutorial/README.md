# jsk_pcl_ros_samples

jsk_pcl_ros package samples

# Install
```
sudo apt-get install -y ros-noetic-jsk-pcl-ros
sudo apt-get install -y ros-noetic-jsk-visualization
git clone https://github.com/hoshianaaa/jsk_pcl_ros_samples.git
cd ~/catkin_ws

catkin build 
or
catkin_make

source ~/catkin_ws/devel/setup.bash

```
# Samples

## attention_clipper(領域の切り抜き)

- start process
```
roslaunch jsk_pcl_ros_samples attention_clipper.launch
```

![attention_clipper1](https://user-images.githubusercontent.com/40942409/111522713-e49c5d00-879d-11eb-88de-588b5b1f4d68.png)

- move bounding box
```
rostopic pub /attention_clipper/input/pose geometry_msgs/PoseStamped "header:
  seq: 0
  stamp:
    secs: 0
    nsecs: 0
  frame_id: 'base_link'
pose:
  position:
    x: 0.0
    y: 0.1
    z: 0.0
  orientation:
    x: 0.0
    y: 0.0
    z: 0.0
    w: 0.0"
```

![attention_clipper2](https://user-images.githubusercontent.com/40942409/111523346-858b1800-879e-11eb-8375-3107b5459416.png)

- change bounding box scale
```
rostopic pub /attention_clipper/input/box jsk_recognition_msgs/BoundingBox "header:
  seq: 0
  stamp: {secs: 0, nsecs: 0}
  frame_id: 'base_link'
pose:
  position: {x: 0.0, y: 0.1, z: 0.0}
  orientation: {x: 0.0, y: 0.0, z: 0.0, w: 0.0}
dimensions: {x: 0.2, y: 0.2, z: 0.2}
value: 0.0
label: 0"
```

![attention_clipper3](https://user-images.githubusercontent.com/40942409/111523770-021df680-879f-11eb-91f4-72ab7dc0fe33.png)

- control bounding box from gui

slide bar control

![Screenshot from 2022-08-20 05-02-25](https://user-images.githubusercontent.com/40942409/185698592-172b75b2-33da-45c7-ba0a-36ce0e254d27.png)

- multi bounding box
```
roslaunch jsk_pcl_ros_samples attention_clipper_multi.launch 
```

![Screenshot from 2021-03-18 04-53-53](https://user-images.githubusercontent.com/40942409/111529920-0e598200-87a6-11eb-9cb8-f6e991a1a1e1.png)


## detect_graspable_poses_pcabase(graspable pose detection)

```
roslaunch jsk_pcl_ros_samples detect_graspable_poses_pcabase.launch
```

![Screenshot from 2021-03-21 14-44-07](https://user-images.githubusercontent.com/40942409/111895762-0b85b800-8a58-11eb-9fb8-8461c23ee58d.png)

## Octree_voxel_grid(点群のボクセル化)
```
roslaunch jsk_pcl_ros_samples octree_voxel_grid.launch
```

change resolution(boxcel size) from rqt_reconfigure

```
rosrun rqt_reconfigure rqt_reconfigure
```
![Screenshot from 2021-03-24 04-41-32](https://user-images.githubusercontent.com/40942409/112209309-a8b13e00-8c5c-11eb-951e-209bef975879.png)


## HSI_color_filter(RGB点群のHSI色空間フィルター)

```
roslaunch jsk_pcl_ros_samples hsi_color_filter.launch
```

rqt_reconfigureでHSIのしきい値を変更できます。
```
rosrun rqt_reconfigure rqt_reconfigure
```

![Screenshot from 2021-03-30 22-29-35](https://user-images.githubusercontent.com/40942409/112997014-af353d80-91a7-11eb-8b02-83f0ea5db343.png)


## supervoxel segmentation

```
roslaunch jsk_pcl_ros_samples supervoxel_segmentation.launch
```

![Screenshot from 2021-04-18 17-47-29](https://user-images.githubusercontent.com/40942409/115139733-7b468d00-a06e-11eb-87b2-07b864ef6806.png)

- change parameter

```
rosrun rqt_reconfigure rqt_reconfigure
```

## normal_estimation_omp(法線推定)

```
roslaunch jsk_pcl_ros_samples normal_estimation_omp.launch
```

![Screenshot from 2021-05-02 02-37-04](https://user-images.githubusercontent.com/40942409/116790481-541ca080-aaef-11eb-91dc-f6a5c3e9eb92.png)

## multi_plane_sac_segmentation(平面検出)

```
roslaunch jsk_pcl_ros_samples multi_plane_sac_segmentation.launch
```

![Screenshot from 2021-05-05 13-54-35](https://user-images.githubusercontent.com/40942409/117098641-097a7d00-adaa-11eb-9fc0-8d06de02d2ae.png)

## region_growing_segmentation

```
roslaunch jsk_pcl_ros_samples region_growing_segmentation.launch
```

![Screenshot from 2021-05-05 17-32-45](https://user-images.githubusercontent.com/40942409/117115553-38075080-adc8-11eb-9ed8-4002a921bf8f.png)

## region_growing_multiple_plane_segmentation

```
roslaunch jsk_pcl_ros_samples region_growing_multiple_plane_segmentation.launch
```

![Screenshot from 2021-05-05 17-47-24](https://user-images.githubusercontent.com/40942409/117117154-2aeb6100-adca-11eb-9b7f-007bec146876.png)


## normal_direction_filter(法線方向フィルター)

```
roslaunch jsk_pcl_ros_samples normal_direction_filter.launch
```

![Screenshot from 2021-05-10 02-53-59](https://user-images.githubusercontent.com/40942409/117582346-8c9a2b00-b13c-11eb-8189-2796d228484c.png)

## eucliean_segmentation(距離によるクラスタリング)

- bunny.pcd
![Screenshot from 2022-08-11 20-20-33](https://user-images.githubusercontent.com/40942409/184122904-fcb78866-ee40-4033-9f6d-1c336361f411.png)

- karage.pcd

pcl_nodelet/clusteringの`tolerance`を変えると、結果が結構変わる  
  
tolerance: 0.1

![Screenshot from 2022-08-11 20-38-54](https://user-images.githubusercontent.com/40942409/184125311-49030dfb-7309-47d6-b925-a1a704232059.png)

tolerance: 0.04

![Screenshot from 2022-08-11 20-34-01](https://user-images.githubusercontent.com/40942409/184124735-36d1c31c-5d3d-40d0-bbec-a9036de5fb76.png)
