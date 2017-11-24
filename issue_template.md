
Hi, I want to use the offline_backpack_3d example to generate a 3D map from a bag file.

Because our robot is not built on ROS, I converted the data from time stamped pcd files and IMU outputs to a Rosbag file using the Rosbag API.

I tried LOAM before and the data could be displayed on RVIZ correctly.

Our robot has a single VLP16 Lidar and a IMU on board. I only have acceleration and angular velocity availiable so I set the first term of the orientation covariance to -1 and 0s to all acceleration and angular velocity covariances.

I have edited the configuration files accordingly but nothing is showing up in RVIZ and local_trajectory_builder.cc throws warnings about empty range data and the trajectory seems to finish once it is generated.

Could you please take a look and help to point out where I might have missed? All relevant files can be found in the repo, if you need any additional info please let me know. Thanks!


Specifications:
Ubuntu 16.04 LTS, ROS Kinetic

Expected behavior:
3D mapping visualized by RVIZ

Actual behavior:
Nothing shows on RVIZ and empty packets warnings found in terminal output.

Terminal output:

```bash
... logging to /home/chen/.ros/log/e38529bc-d0b0-11e7-b1c4-7085c2452675/roslaunch-chen-desktop-13865.log
Checking log directory for disk usage. This may take awhile.
Press Ctrl-C to interrupt
Done checking log file disk usage. Usage is <1GB.

started roslaunch server http://chen-desktop:33387/

SUMMARY
========

PARAMETERS
* /rosdistro: kinetic
* /rosversion: 1.12.7
* /use_sim_time: True

NODES
/
  cartographer_occupancy_grid_node (cartographer_ros/cartographer_occupancy_grid_node)
  cartographer_offline_node (cartographer_ros/cartographer_offline_node)
  rviz (rviz/rviz)

ROS_MASTER_URI=http://localhost:11311

core service [/rosout] found
process[rviz-1]: started with pid [13883]
process[cartographer_offline_node-2]: started with pid [13884]
process[cartographer_occupancy_grid_node-3]: started with pid [13885]
[ INFO] [1511486525.320189023]: I1124 10:22:05.000000 13884 configuration_file_resolver.cc:40] Found '/home/chen/Documents/catkin_ws/install_isolated/share/cartographer_ros/configuration_files/backpack_3d_kaibo.lua' for 'backpack_3d_kaibo.lua'.
[ INFO] [1511486525.320403810]: I1124 10:22:05.000000 13884 configuration_file_resolver.cc:40] Found '/home/chen/Documents/catkin_ws/install_isolated/share/cartographer/configuration_files/map_builder.lua' for 'map_builder.lua'.
[ INFO] [1511486525.320434847]: I1124 10:22:05.000000 13884 configuration_file_resolver.cc:40] Found '/home/chen/Documents/catkin_ws/install_isolated/share/cartographer/configuration_files/map_builder.lua' for 'map_builder.lua'.
[ INFO] [1511486525.320476840]: I1124 10:22:05.000000 13884 configuration_file_resolver.cc:40] Found '/home/chen/Documents/catkin_ws/install_isolated/share/cartographer/configuration_files/sparse_pose_graph.lua' for 'sparse_pose_graph.lua'.
[ INFO] [1511486525.320502319]: I1124 10:22:05.000000 13884 configuration_file_resolver.cc:40] Found '/home/chen/Documents/catkin_ws/install_isolated/share/cartographer/configuration_files/sparse_pose_graph.lua' for 'sparse_pose_graph.lua'.
[ INFO] [1511486525.320591192]: I1124 10:22:05.000000 13884 configuration_file_resolver.cc:40] Found '/home/chen/Documents/catkin_ws/install_isolated/share/cartographer/configuration_files/trajectory_builder.lua' for 'trajectory_builder.lua'.
[ INFO] [1511486525.320618269]: I1124 10:22:05.000000 13884 configuration_file_resolver.cc:40] Found '/home/chen/Documents/catkin_ws/install_isolated/share/cartographer/configuration_files/trajectory_builder.lua' for 'trajectory_builder.lua'.
[ INFO] [1511486525.320656660]: I1124 10:22:05.000000 13884 configuration_file_resolver.cc:40] Found '/home/chen/Documents/catkin_ws/install_isolated/share/cartographer/configuration_files/trajectory_builder_2d.lua' for 'trajectory_builder_2d.lua'.
[ INFO] [1511486525.320680280]: I1124 10:22:05.000000 13884 configuration_file_resolver.cc:40] Found '/home/chen/Documents/catkin_ws/install_isolated/share/cartographer/configuration_files/trajectory_builder_2d.lua' for 'trajectory_builder_2d.lua'.
[ INFO] [1511486525.320760659]: I1124 10:22:05.000000 13884 configuration_file_resolver.cc:40] Found '/home/chen/Documents/catkin_ws/install_isolated/share/cartographer/configuration_files/trajectory_builder_3d.lua' for 'trajectory_builder_3d.lua'.
[ INFO] [1511486525.320788387]: I1124 10:22:05.000000 13884 configuration_file_resolver.cc:40] Found '/home/chen/Documents/catkin_ws/install_isolated/share/cartographer/configuration_files/trajectory_builder_3d.lua' for 'trajectory_builder_3d.lua'.
[ INFO] [1511486525.326487647]: I1124 10:22:05.000000 13884 submaps.cc:295] Added submap 1
[ INFO] [1511486525.326521432]: I1124 10:22:05.000000 13884 map_builder_bridge.cc:82] Added trajectory with ID '0'.
[ INFO] [1511486525.329351465]: I1124 10:22:05.000000 13884 offline_node_main.cc:204] Processed 0 of 73.2201 bag time seconds...
[ INFO] [1511486525.329830904, 1511486521.044940109]: I1124 10:22:05.000000 13884 ordered_multi_queue.cc:172] All sensor data for trajectory 0 is available starting at '636470833213447401'.
[ WARN] [1511486525.367680831, 1511486537.244711109]: W1124 10:22:05.000000 13884 local_trajectory_builder.cc:120] Dropped empty range data.
[ WARN] [1511486525.406219644, 1511486553.244683109]: W1124 10:22:05.000000 13884 local_trajectory_builder.cc:120] Dropped empty range data.
[ WARN] [1511486525.443202849, 1511486569.244686109]: W1124 10:22:05.000000 13884 local_trajectory_builder.cc:120] Dropped empty range data.
[ WARN] [1511486525.481055692, 1511486585.244682109]: W1124 10:22:05.000000 13884 local_trajectory_builder.cc:120] Dropped empty range data.
[ INFO] [1511486525.500091728, 1511486593.244685109]: I1124 10:22:05.000000 13884 map_builder_bridge.cc:99] Finishing trajectory with ID '0'...
[ INFO] [1511486525.500332218, 1511486593.244685109]: I1124 10:22:05.000000 13884 map_builder_bridge.cc:108] Running final trajectory optimization...
Optimizing: Done.     
[ INFO] [1511486525.500387012, 1511486593.244685109]: I1124 10:22:05.000000 13934 constraint_builder.cc:278] 0 computations resulted in 0 additional constraints.
[ INFO] [1511486525.500408083, 1511486593.244685109]: I1124 10:22:05.000000 13934 constraint_builder.cc:280] Score histogram:
Count: 0
[ INFO] [1511486525.500422593, 1511486593.244685109]: I1124 10:22:05.000000 13934 constraint_builder.cc:281] Rotational score histogram:
Count: 0
[ INFO] [1511486525.500434616, 1511486593.244685109]: I1124 10:22:05.000000 13934 constraint_builder.cc:283] Low resolution score histogram:
Count: 0
[ INFO] [1511486525.500460885, 1511486593.244685109]: I1124 10:22:05.000000 13884 offline_node_main.cc:236] Elapsed wall clock time: 0.180468 s
[ INFO] [1511486525.500480703, 1511486593.244685109]: I1124 10:22:05.000000 13884 offline_node_main.cc:240] Elapsed CPU time: 0.226582 s
[ INFO] [1511486525.500503326, 1511486593.244685109]: I1124 10:22:05.000000 13884 offline_node_main.cc:244] Peak memory usage: 49568 KiB
[ INFO] [1511486525.500517999, 1511486593.244685109]: I1124 10:22:05.000000 13884 offline_node_main.cc:249] Writing state to '/home/chen/Downloads/data/test_imu_cart.bag.pbstream'...
Optimizing: Done.     
[ INFO] [1511486525.531054390, 1511486593.244685109]: I1124 10:22:05.000000 13929 constraint_builder.cc:278] 0 computations resulted in 0 additional constraints.
[ INFO] [1511486525.531081439, 1511486593.244685109]: I1124 10:22:05.000000 13929 constraint_builder.cc:280] Score histogram:
Count: 0
[ INFO] [1511486525.531099333, 1511486593.244685109]: I1124 10:22:05.000000 13929 constraint_builder.cc:281] Rotational score histogram:
Count: 0
[ INFO] [1511486525.531124052, 1511486593.244685109]: I1124 10:22:05.000000 13929 constraint_builder.cc:283] Low resolution score histogram:
Count: 0
0x20908e0 void QWindowPrivate::setTopLevelScreen(QScreen*, bool) ( QScreen(0x15f9340) ): Attempt to set a screen on a child window.
0x2093d50 void QWindowPrivate::setTopLevelScreen(QScreen*, bool) ( QScreen(0x15f9340) ): Attempt to set a screen on a child window.
0x2090ef0 void QWindowPrivate::setTopLevelScreen(QScreen*, bool) ( QScreen(0x15f9340) ): Attempt to set a screen on a child window.
0x209c0b0 void QWindowPrivate::setTopLevelScreen(QScreen*, bool) ( QScreen(0x15f9340) ): Attempt to set a screen on a child window.
[cartographer_offline_node-2] process has finished cleanly
log file: /home/chen/.ros/log/e38529bc-d0b0-11e7-b1c4-7085c2452675/cartographer_offline_node-2*.log
^C[cartographer_occupancy_grid_node-3] killing on exit
[rviz-1] killing on exit
shutting down processing monitor...
... shutting down processing monitor complete
done


```

Steps to reproduce the problem:
roslaunch cartographer_ros offline_backpack_3d_kaibo.launch bag_filenames:=${HOME}/Downloads/data/test_imu_cart.bag

