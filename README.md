# Grasp Pose Detection (GPD)

Grasp Pose Detection (GPD) is a package to detect 6-DOF grasp poses (3-DOF
position and 3-DOF orientation) for a 2-finger robot hand (e.g., a parallel
jaw gripper) in 3D point clouds. GPD takes a point cloud as input and produces
pose estimates of viable grasps as output. The main strengths of GPD are:

## Requirements

1. [PCL 1.9 or newer](http://pointclouds.org/)
2. [Eigen 3.0 or newer](https://eigen.tuxfamily.org)
3. [OpenCV 3.4 or newer](https://opencv.org)


## Installation

The following instructions have been tested on **Ubuntu 16.04**. Similar
instructions should work for other Linux distributions.

1. Install [PCL](http://pointclouds.org/) and
[Eigen](https://eigen.tuxfamily.org). If you have ROS Indigo or Kinetic
installed, you should be good to go.

2. Install OpenCV 3.4 ([tutorial](https://www.python36.com/how-to-install-opencv340-on-ubuntu1604/)).

3. Clone the repository into some folder:

   ```
   git clone https://github.com/atenpas/gpd
   ```

4. Build the package:

   ```
   cd gpd
   mkdir build && cd build
   cmake ..
   make -j
   ```

You can optionally install GPD with `sudo make install` so that it can be used by other projects as a shared library.


## Generate Grasps for a Point Cloud File

Run GPD on an point cloud file (PCD or PLY):

   ```
   ./detect_grasps ../cfg/eigen_params.cfg ../tutorials/krylon.pcd
   ```

The output should look similar to the screenshot shown below. The window is the PCL viewer. You can press [q] to close the window and [h] to see a list of other commands.

<img src="readme/file.png" alt="" width="30%" border="0" />

Below is a visualization of the convention that GPD uses for the grasp pose (position and orientation) of a grasp. The grasp position is indicated by the orange cross and the orientation by the colored arrows.

<img src="readme/hand_frame.png" alt="" width="30%" border="0" />

<a name="parameters"></a>
## 4) Parameters

Brief explanations of parameters are given in *cfg/eigen_params.cfg*.

The two parameters that you typically want to play with to improve on the
number of grasps found are *workspace* and *num_samples*. The first defines the
volume of space in which to search for grasps as a cuboid of dimensions [minX,
maxX, minY, maxY, minZ, maxZ], centered at the origin of the point cloud frame.
The second is the number of samples that are drawn from the point cloud to
detect grasps. You should set the workspace as small as possible and the number
of samples as large as possible.

## References

Andreas ten Pas, Marcus Gualtieri, Kate Saenko, and Robert Platt. [**Grasp
Pose Detection in Point Clouds**](http://arxiv.org/abs/1706.09911). The
International Journal of Robotics Research, Vol 36, Issue 13-14, pp. 1455-1473.
October 2017.
