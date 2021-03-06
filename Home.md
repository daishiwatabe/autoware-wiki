![Autoware.AI](https://static.wixstatic.com/media/984e93_bd79992caecb41dab100c391e648d9b8~mv2.png/v1/fill/w_1934,h_1148,al_c/984e93_bd79992caecb41dab100c391e648d9b8~mv2.png)

## Welcome to the Autoware.AI Wiki

Autoware.AI is **ROS-based open-source software**, enabling self-driving vehicles to be tested in private areas, urban roads, and highways. Another variant of Autoware, _a.k.a._, [Autoware.Auto](https://gitlab.com/AutowareAuto), is also under development for the purpose of commercial deployment of self-driving vehicles with functional safety capabilities. The current version of Autoware.AI provides, but not limited to, the functional modules described below. 

_Localization_ depends on **3D high-definition map** data and the **NDT** algorithm. The result of _Localization_ is complemented by the **Kalman Filter** algorithm, using odometry information obtained from **CAN** messages and **GNSS/IMU** sensors.
 
_Detection_ is empowered by **camera** and **LiDAR** devices in combination with **3D high-definition map** data. The _Detection_ module uses **deep learning** and **sensor fusion** approaches.

_Tracking_ and _Prediction_ are realized with the **Kalman Filter** algorithm and the lane network information provided by **3D high-definition map** data.
 
_Planning_ is based on **probabilistic robotics** and **rule-based systems**, partly using **deep learning** approaches as well. 

_Control_ defines motion of the vehicle with a twist of **velocity** and **angle** (also **curvature**). The _Control_ module falls into both the Autoware-side stack (**MPC** and **Pure Pursuit**) and the vehicle-side interface (**PID** variants). 

To conclude, Autoware provides a complete software stack for self-driving vehicles. [Join Autoware](https://www.autoware.org/) now, and your contribution will be loved by the world.

## Getting Started

1. [Installation](https://github.com/CPFL/Autoware/wiki/Installation)
1. [ROSBAG Demo](https://github.com/CPFL/Autoware/wiki/ROSBAG-Demo)
1. [Simulation Demo](https://github.com/CPFL/Autoware/wiki/Simulation-Demo)
1. [Field Test](https://github.com/CPFL/Autoware/wiki/Field-Test)

## Communication Tools

1. [Slack](https://autoware.herokuapp.com/) (for everybody)
1. [ROS Discourse](https://discourse.ros.org/c/autoware) (for developers)
1. [ROS Answer](https://answers.ros.org/questions/scope:all/sort:activity-desc/tags:autoware/page:1/) (for users)

## Frequently Asked Questions

### History of Autoware 

The original version of Autoware was officially released in August 2015 by the research group of Nagoya University directed by Prof. Shinpei Kato. Later in December 2015, [Tier IV](https://www.tier4.jp) was founded by Prof. Shinpei Kato to maintain Autoware and apply it for real self-driving vehicles. As time goes by, Autoware has become an recognized open-source project on the GitHub. In December 2018, Tier IV decided to transfer the ownership of Autoware to [The Autoware Foundation](https://www.autoware.org), which was co-founded by Tier IV, [Apex.AI](https://www.apex.ai), and [Linaro](https://www.linaro.org/). Now that Autoware is maintained by The Autoware Foundation, the roadmap, policy, and future of Autoware can be determined by the member companies rather than a particular individual company. We believe this makes Autoware be a _true_ open-source project. 

### What is required to use Autoware?

Autoware requires 3D map data and LiDAR sensors at minimum. They are used for most of main functional modules, such as  localization, detection, tracking, prediction, and planning. Cameras enable Autoware to recognize traffic lights in combination with 3D map data, and can also enhance detection capabilities. GNSS and IMU are also useful to complement the result of Localization. Finally, you need a car with the Autoware interface. ROSBAG and the simulators can help you in case that you don't have a car.

### How to create 3D map data?

We suggest the following steps. First, you try creating small-scale 3D map data for private area testing, using the NDT mapping node provided by Autoware or using the [Autoware Tools](https://tools.tier4.jp/) (paid service). Once it goes well, you can contact a professional mapping company in your region to create large-scale 3D map data for public road testing. Examples of the mapping companies include [Aisan Technology](http://www.aisantec.co.jp/english/) and [Mandli](https://www.mandli.com/). Note that the NDT mapping node and the Autoware Tools are designed for closed environments, thus not suitable for creating large-scale 3D map data.

### Which car is available with Autoware?

Autoware requires a car to have an interface exposed to receive a twist of velocity and angle produced by the Autoware's _Control_ module. Such a car often implements a by-wire controller or a mechanical controller to actuate the steering and throttle. Examples of the car providers include [AutonomouStuff](https://autonomoustuff.com/product/astuff-automotive/) and [StreetDrone](https://streetdrone.com/vehicles/).

### Which computer can run Autoware in real-time?

Most of industrial PCs and gaming PCs with the Intel x86 architecture are good to begin with. For automotive applications, you can also consider the Arm architecture. Examples of Arm-based boards include [96Boards products](https://www.96boards.org/products/), [Xilinx products](https://www.xilinx.com/products/silicon-devices/soc/zynq-ultrascale-mpsoc.html), and [NVIDIA products](https://www.nvidia.com/en-us/self-driving-cars/drive-platform/). Many-core solutions are also provided with [Kalray MPPA](https://www.kalrayinc.com/products/) and [eSol MCOS](https://www.esol.com/embedded/).

### Can I contribute to the Autoware project?

Yes, of course. Please join [The Autoware Foundation](https://www.autoware.org)!

### More questions?

Visit [Slack](https://autoware.herokuapp.com/), [ROS Discourse](https://discourse.ros.org/c/autoware), and [ROS Answer](https://answers.ros.org/questions/scope:all/sort:activity-desc/tags:autoware/page:1/).