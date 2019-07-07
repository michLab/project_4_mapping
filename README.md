# Where am I 

A third project from Udaicty Robotics Software Engineer Nanodegree.
A robot is haused in know environment (a map was generated using pgr_map_creator).
Localization is performed using Hokuyo laser scanner and AMCL package.
User can order movement using move_base package or Teleop package.

<p align="center">
  <img width="920" height="600" src="images/amcl_2.gif">
  <br>Robot localyzing himself in known map (AMCL)
</p>


## How to use

In order to run this package follow this steps:
* Make direcotry for catkin workspace:
```sh
mkdir -p path_to_my_workspace/workspace_name/src
```
* Go to the src directory and init catkin workspace:
```sh
cd path_to_my_workspace/workspace_name/src
catkin_init_workspace
```
* Go to `workspace_name` directory and pull this repository:
```sh
git init
git remote add origin link_to_this_repo
git pull
git checkout master
```
* Make catkin:
```sh
cd path_to_my_workspace/workspace_name
catkin_make
source devel/setup.bash
```
* Run ROS:
```sh
roslaunch my_robot world.launch
```
* In another terminal run amcl, move_base and gzserver:
```sh
cd path_to_my_workspace/workspace_name
source devel/setup.bash
roslaunch my_robot amcl.launch
```
* If you want to use Teleop in third terminal write:
```sh
cd path_to_my_workspace/workspace_name
source devel/setup.bash
rosrun teleop_twist_keyboard teleop_twist_keyboard.py
```

## Nodes
Three nodes are essential for where am I:
* `map_server` - which provides map data as a ROS service to other nodes such as the amcl node.
* `amcl` - performs Adaptative Monte Calro Localization
* `move_base` - performs robot path planning and robot controll

## Robot

Initialli robot is placed in location: x=-8, y=-2 (gazebo truth), but in AMCL it is assumed,
than robot is placed in location (0,0).

<p align="center">
  <img width="460" height="300" src="images/true_initial_robot_position.png">
  <br>A rrobot initial position in gazebo
</p>


To ensure proper localization after move the x and y position covarinaces were assumed to equal:
`cov_xx = 170m` and `cov_yy = 170m`. These values "covers" all given map, thanks than particles are spreaded uniformly on the whole map.
The maximum number of particles was chosen in emirical manner and equals 5000.
List of parameters worth of consideration when tuning:
* in AMCL:
  * `initial_pose_x`
  * `initial_pose_y`
  * `initial_pose_a`
  * `initial_cov_xx`
  * `initial_cov_yy`
  * `min_particles`
  * `max_particles`
  * `update_min_a`
  * `update_min_d`
* in move_base:
  * `max_vel_x`
  * `min_vel_x`
  * `max_vel_theta`
  * `min_in_place_vel_theta`
  * `controller_frequency`
  * `planner_frequency`
  * `pdist_scale`
  * `gdist_scale`
  * `occdist_scale`
  * `robot_radius`
  * `inflation_radius`
  * `cost_scaling_factor`


## License
The contents of this repository are covered under the [MIT License](./LICENSE.txt)


## Contributing

1. Fork it (<https://github.com/michLab/project_3_localization.git>)
2. Create your feature branch (`git checkout -b feature/fooBar`)
3. Commit your changes (`git commit -am 'Add some fooBar'`)
4. Push to the branch (`git push origin feature/fooBar`)
5. Create a new Pull Request
