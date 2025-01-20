# Creating a ROS Workspace

Se crea el espacio de trabajo este puede hacerse en cualquier lugar es importante mantener la estructura con el directorio src

```sh
mkdir -p ~/catkin_ws/src
cd catkin_ws/src
#Inicializa el WS
catkin_init_workspace
cd ~/catkin_ws
#Construccion del WS
catkin_make
#Hacer visible el WS accesible y visible
gedit .bashrc
#al final del archivo .bashrc poner la siguiente linea
# source ~/<workspace_name>/devel/setup.bash
source ~/catkin_ws/devel/setup.bash
#Cuando se tengan variables por agregar al ambiente de linux ejecutar
source ~/catkin_ws/devel/setup.bash
#Intalacion del ejecutable creado
catkin_make install
```

## Crear un paquete 

```sh
#Sintasis de un paquete
#catkin_create_pkg ros_package_name package_dependencies
cd ~/catkin_ws/src
catkin_create_pkg hello_world roscpp rospy std_msgs
```
- CMakeLists.txt : This file has all the commands to build the ROS source code inside the package and create the executable.

- package.xml : This is basically an XML file. It mainly contains the package dependencies, information, and so forth.

- src : The source code of ROS packages is kept in this folder. Normally, C++ files are kept in the src folder. If you want to keep Python scripts, you can create another folder called scripts inside the package folder.

- include: This folder contains the package header files. It can be automatically generated, or third-party library files go in it.

## Uso de librerias de clientes de ROS

We can write ROS nodes in any programming language. If there is any ROS client for that programming language, it is easier to create ROS nodes; otherwise, we may need to implement our own ROS concepts.

The following are the main ROS client libraries:

- roscpp : This is the ROS client library for C++. It is widely used for developing ROS applications because of its high performance.

- rospy : This is the ROS client library for Python (http://wiki.ros.org/rospy). Its advantage is saving development time. We can create a ROS node in less time than with roscpp. It is ideal for quick prototyping applications, but performance is weaker than with roscpp. Most of the command-line tools in ROS are coded using rospy such as roslaunch, roscore, and so forth.

- roslisp : This is the ROS client library of the Lisp language. It is mainly used in motion planning libraries on ROS, but it is not as popular as roscpp and rospy.

There are also experimental client libraries, including rosjava, rosnodejs, and roslua. The complete list of ROS client libraries is at http://wiki.ros.org/Client%20Libraries.

## Imprimir mesajes en nodos de ROS

ROS provides APIs to log messages. These messages are readable string that convey the status of the node.

In C++, the following functions log the node’s messages:

```C++
ROS_INFO(string_msg,args): Logging the information of node
ROS_WARN(string_msg,args): Logging warning of the node
ROS_DEBUG(string_msg ,args): Logging debug messages
ROS_ERROR(string_msg ,args): Logging error messages
ROS_FATAL(string_msg ,args): Logging Fatal messages
Eg: ROS_DEBUG("Hello %s","World");
```

In Python, there are different functions for the logging operations:

```python
rospy.logdebug(msg, *args)
rospy.logerr(msg, *args)
rospy.logfatal(msg, *args)
rospy.loginfo(msg, *args)
rospy.logwarn(msg, *args)
```

## Usar arduino

Paquete para usar arduino con ROS

```sh
sudo apt install ros-noetic-rosserial-arduino
```

Importar libreria de ROS a IDE de arduino para programacion del arduino
```sh
$ rosrun rosserial_arduino make_libraries.py .
```

uso del ejemplo File ➤ Examples ➤ ros_lib

Comando para encontrar puerto de conexión USB al arduino

```sh
dmesg
#Permiso para usar el arduino este puede estar conectado a otro puerto en este caso es el ttyACM0
$ sudo chmod 777 /dev/ttyACM0
#IDE de arduido se indica el puerto para programar
Goto Tools->Port->ttyACM0

#Starting roscore
roscore
#Se enlaza el nodo con el puerto
rosrun rosserial_python serial_node.py /dev/ttyACM0
#Se publica un valor en el topico /toggle_led 
rostopic pub toggle_led std_msgs/Empty --once
```