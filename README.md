# Package to Launch slam_toolbox

This package only contains launch and config files which call the slam_toolbox executables.
Note. presently the slam_toolbox is installed as binaries from the apt repository

## Which launch file to use?

1. The online_sync file would be preferred as it allows for better loop closure
2. The async is less computationally intensive as it does not process every frame that it receives

## Config file nitty-gritties

The config file has a few parameters which must be set right. As per the TF tree we developed
in [slam_toolbox_tf2](https://github.com/DockDockGo/slam_toolbox_tf2) and [repub_velo](https://github.com/DockDockGo/repub_velo) repositories, we configure the slam_tooblox to look at specific topics as shown below:

```yaml
  slam_toolbox:
  ros__parameters:

    # Plugin params
    solver_plugin: solver_plugins::CeresSolver
    ceres_linear_solver: SPARSE_NORMAL_CHOLESKY
    ceres_preconditioner: SCHUR_JACOBI
    ceres_trust_strategy: LEVENBERG_MARQUARDT
    ceres_dogleg_type: TRADITIONAL_DOGLEG
    ceres_loss_function: None

    # ROS Parameters
    odom_frame: odom
    map_frame: map
    base_frame: base_footprint
    scan_topic: /scan_new
    mode: mapping #localization
```

The mode here is set to mapping, but as shown it can also be set to localization. However,
in localization mode, a pre-existing map and the path to that map should be configured in the
same config file (not shown in here, since I'm yet to do localization myself).

