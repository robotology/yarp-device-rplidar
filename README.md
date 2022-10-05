yarp-device-rplidar ![YARP logo](https://raw.githubusercontent.com/robotology/yarp/master/doc/images/yarp-robot-24.png "yarp-device-rplidar")
======================

This repository contains the [YARP](https://www.yarp.it/) device drivers for Slamtec rpLidar sensors.

The devices currently supported are:
- [rplidar A1](https://www.slamtec.com/en/Lidar/A1)
- [rplidar A2](https://www.slamtec.com/en/Lidar/A2)
- [rplidar A3](https://www.slamtec.com/en/Lidar/A3)
- [rplidar S2](https://www.slamtec.com/en/S2)

Here are the names of the Yarp device drivers and the compatibility list:
- `rpLidar`:  based on yarp direct serial port communication (tested just with: `A1`, not maintained anymore)
- `rpLidar2`: based on slamtec SDK 1.12 (tested with: `A1`, `A2`)
- `rpLidar3`: based on slamtec SDK 1.12 (major improvements with respect to rpLidar2, tested with: `A2`, `A3`)
- `rpLidar4`: based on slamtec SDK 2.0  (tested with: `A3`, `S2`)

NB: This repo is currently under development.
-------

Maintainers
--------------
This repository is maintained by:

| | |
|:---:|:---:|
| [<img src="https://github.com/randaz81.png" width="40">](https://github.com/randaz81) | [@randaz81](https://github.com/randaz81) |

