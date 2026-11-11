# SR18 on a mobile robot: first evaluation

I’m Alex from Benewake. This checklist is for developers comparing 3D LiDAR options on a real robot. It helps define a first measurement, not a claim that SR18 will fit a particular robot or navigation stack.

## 1. Draw the measurement job

Record the sensor's proposed height and orientation, the robot body's occlusions, and the nearest low object or floor patch that must be observed. For a ray tilted downward by angle θ from horizontal at height `h`, its intersection with a level floor is approximately `h / tan(θ)` away. This is a planning estimate only: use the actual channel angles, mount geometry, and a raw point cloud before deciding coverage.

The [SR18 product page](https://en.benewake.com/SR18/index.html) lists 18 channels, a 360° × 48° field of view (−8° to +40°), 30 m at 10% reflectivity, and a minimum range of ≤0.15 m. None of those headline figures alone proves that a specific low object will be detected.

## 2. Capture evidence before tuning navigation

| Check | Record |
| --- | --- |
| Mechanical and electrical fit | Hardware revision, measured mount pose, body occlusions, supply, connector, adapter and the released manual used for wiring. The product pages list RS485 at 3,125,000 bit/s but differ on the supply range. Before powering the unit, confirm the supported voltage and connector pinout in the released documentation for the hardware revision you received. |
| Static raw cloud | A measured flat wall, a low object at several distances, point coordinates, channel/ring ID when available, timestamps, invalid returns and decoder version. |
| Moving raw cloud | Slow, controlled motion with sensor and host timestamps; record any IMU stream. |
| Navigation cloud | Compare raw points against deskew, downsampling, height filters and the costmap. A point lost in filtering is a different problem from a missing raw return. |

The product page lists 5/10 Hz configurable and IP66. Confirm the settings and enclosure of the actual unit. Do not treat the IP rating of the sensor as a rating for the robot's connector or cable installation.

## 3. Decide the next experiment

- If the **raw** cloud covers the target, check whether the processing chain preserves it and whether timestamps align with the robot's motion.
- If the raw cloud misses it, check mounting height, tilt, body occlusion and the actual vertical channel angles before changing the navigation algorithm.
- If coverage still misses the required patch, compare another mount or an additional near-field sensor using the same measured targets.

This checklist does not validate safe stopping, driver compatibility or detection of every material. Test on the actual robot and environment.

## Product information and feedback

The [official SR18 page](https://en.benewake.com/SR18/index.html) has the current product information, documents and pre-order path. The [October 30, 2026 announcement](https://en.benewake.com/NewsUpdates/info_itemid_6194.html) says worldwide availability starts November 30, 2026; confirm current availability with Benewake before planning a purchase.

If a checklist item is unclear or missing, open an issue in this repository with the measurement task and public, non-sensitive details. Please do not post private robot logs or credentials.
