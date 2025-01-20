No code for this chapter

Ver la version de ROS
```sh
rosversion -d

```

Ver los parametros en ROS
```sh
rosparam list

```

Poner un valor en un parametro ej Hello
```sh
#Setting parameter
#$ rosparam set parameter_name value
#Eg. 
$ rosparam set hello "Hello"
#Getting a parameter
#$ rosparam get parameter_name
$ rosparam get hello
#Output: "Hello"
```

## Ejemplo de funcionamiento de nodos uno de habla y otro de escucha junto a un launch para el despliegue de ambos
```sh
rosrun roscpp_tutorials talker
rostopic list
rosrun roscpp_tutorials listener
roslaunch roscpp_tutorials talker_listener.launch
```

## Ejemplo de turtlesim
- Topicos que se estan ejecuantodo
- Lista de servicios usados
- Parametros usados
- Uso de teclado para mover la tortuga
- Mover la tortuga en un cuadrado
- Llamado del servicio /reset para reiniciar a la tortuga


```sh
rosrun turtlesim turtlesim_node
rostopic list
rosservice list
rosparam list
rosrun turtlesim turtle_teleop_key
rosrun turtlesim draw_square
rosservice call /reset
```
## ROS GUI Tools: Rviz and Rqt

```sh
#Start roscore
$ roscore
#Start rviz
$ rosrun rviz rviz
#Start rqt_gui
$ rosrun rqt_gui rqt_gui
```

