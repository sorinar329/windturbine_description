# windturbine_description

A whole onshore wind turbine as a URDF environment: the IEA-3.4-130-RWT reference turbine
(110 m hub height, 130 m rotor) with its tower interior, service lift, crane hoist and the interior
of the nacelle, plus fault scenarios for robot inspection and maintenance.

## Contents

| Path | What it holds |
|---|---|
| `urdf/windturbine.urdf` | The healthy turbine |
| `urdf/scenarios/<name>.urdf` | A fault scenario: the turbine with the scenario's faults in place |
| `urdf/scenarios/<name>_ground_truth.yaml` | Which faults are active, where to see them, their severity, initial joint states and sensor signals |
| `urdf/inspection_points.yaml` | The frames to inspect and the direction to look from |
| `meshes/` | OBJ meshes with their materials; textures in `meshes/textures/` |
| `launch/display.launch.py` | RViz with joint sliders |

## Use

    colcon build --packages-select windturbine_description
    source install/setup.bash
    ros2 launch windturbine_description display.launch.py                                    # healthy
    ros2 launch windturbine_description display.launch.py urdf:=$(ros2 pkg prefix windturbine_description)/share/windturbine_description/urdf/scenarios/bring_the_tool.urdf

Meshes are referenced as `package://windturbine_description/meshes/...`.

## Frame convention

Frame `nacelle`: origin on the yaw axis at the top of the floor, X points upwind (towards the hub),
Z up. The real 4-6 degree shaft tilt is left out so the floor stays level for mobile robots.

URDF has no initial joint state, so faults that set a joint (for example a rotor lock left engaged)
list it under `initial_joint_states` in the scenario's ground truth.

## Origin

This package is generated from the `windturbine_model` repository, where the model is built in
Blender and the URDF is generated, by its `scripts/export_description_package.py`. Change the model
there and export again rather than editing the files here.

Textures are made from CC0 material sets by ambientCG; see `meshes/textures/ATTRIBUTION.txt`.
