```bash
ros2 launch ros2_ctrl_nav launch_sim.launch.py world:=./src/ros2_ctrl_nav/worlds/room.world 

ros2 run teleop_twist_keyboard teleop_twist_keyboard --ros-args --remap /cmd_vel:=/cmd_vel_keyb

rviz2 -d src/ros2_ctrl_nav/config/nav.rviz

ros2 run twist_mux twist_mux --ros-args --params-file ./src/ros2_ctrl_nav/config/twist_mux.yaml -r cmd_vel_out:=diff_cont/cmd_vel_unstamped

ros2 launch slam_toolbox online_async_launch.py params_file:=./src/ros2_ctrl_nav/config/mapper_params_online_async.yaml use_sim_time:=true

ros2 launch nav2_bringup navigation_launch.py use_sim_time:=true


# For map_server or amcl
ros2 run nav2_util lifecycle_bringup map_server
ros2 run nav2_util lifecycle_bringup amcl
```