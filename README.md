# Example of connecting ardupilot with gazebo

### Instalation

Install ArduPilot by following instructions from https://github.com/AS4SR/general_info/wiki/ArduPilot:-Instructions-to-set-up-and-run-an-autopilot-using-SITL-and-Gazebo-simulator

If you get some errors when using commands:

````bash
sim_vehicle.py -f gazebo-iris --map --console -I0
gazebo --verbose worlds/iris_irlock_demo.world
````

you might need to add following commands to .bashrc script:

````bash
export GAZEBO_MODEL_PATH=~/ardupilot/ardupilot_gazebo/models_gazebo:~/ardupilot/ardupilot_gazebo/models
export GAZEBO_PLUGIN_PATH=/usr/lib/x86_64-linux-gnu/gazebo-7.0/plugins:/usr/lib/x86_64-linux-gnu/gazebo-7/plugins/
````

### Including ardupilot_plugin in your custom Gazebo model

Example of plugin is in ardupilot_multirotor_base.urdf.xacro (line 69).
What is needed is the name of IMU sensor, example of which you can find in the same file (lines 41 through 65).
Also you need the names of the rotor joints, as example they are described in file multirotor_base-urdf.xacro (line 62).

With those simple modifications you should be able to apply ardupilot SITL to any model you want.
If something was not done properly, Gazebo should output errors that occured.


### Arming Gazebo model

If your console is printing some errors when you are trying to ARM it,
you might want to try following sequence of commands:

````bash
mode guided
arm uncheck all
arm throttle
arm takeoff 40
````


### Multiple models

If you wish to control multiple models with Ardupilot, you have to start multiple instances of sim_vehicle.py script.
Each script has to have their own instance number (-I0, -I1, -I2 etc.).
Plugin in the model you wish to control with a particular instance has to have ports 9002+I\*10 and 9003+I\*10.
So each instance of SITL controls specific ports.


### Connecting with ROS

Instructions are on http://ardupilot.org/dev/docs/ros-sitl.html and http://ardupilot.org/dev/docs/ros-connecting.html.
I didn't have any problems with ROS so just follow instructions and everything should work just fine :)
