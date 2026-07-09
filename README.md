# Follow Me (ROS) — external skill

Wraps the in-repo [`agenticros_follow_me`](https://github.com/agenticros/agenticros/tree/main/ros2_ws/src/agenticros_follow_me) node as mission capabilities `follow_person_ros` / `stop_follow_person_ros`.

This is **not** the same as the marketplace `followme` / in-gateway YOLO skill — perception and control run on the robot.

```bash
npx agenticros skills install agenticros/follow-me-ros
```

## Bringup

```bash
# From the AgenticROS ros2_ws
colcon build --packages-select agenticros_msgs agenticros_follow_me
source install/setup.bash
ros2 run agenticros_follow_me follow_me_node
```

## Mission example

```json
{
  "mission": {
    "name": "follow then stop",
    "steps": [
      {
        "id": "start",
        "capability": "follow_person_ros",
        "inputs": { "request": { "target_description": "" } }
      },
      {
        "id": "stop",
        "capability": "stop_follow_person_ros",
        "inputs": { "request": {} }
      }
    ]
  }
}
```

## Requirements

- Built `agenticros_msgs` + `agenticros_follow_me`
- Camera / depth topics configured for the follow node
- Transport with service calls (local / rosbridge preferred)
