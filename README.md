# Proyecto Final (Motoman):

Se busca realizar la simulacion dinamica del Robot Motoman, por medio de los software ROS y Gazebo utilizando un controlador de movimiento, drive para lograr llegar al dinamismo mecanico del robot.

Para lograr la realizacion de este proyecto se tomó en cuanta la formulacion del prototipo compuesto por el URDF y el despliegue de los archivos Launch, para poder correr el prototipo en Gazebo. Fue de suma importancia el desarrollo de adecuados controladores de trayectoria para el robot, que se aplican como los Drivers del modelo del robot.

## Control

(https://github.com/fabianrl22/ProyectoFinal_Robotica/blob/master/Captura.JPG)

### Control de posicion:

Se puede aplicar un controlador de posición usando el paquete ros_control. Para hacer esto, se deben definir varias cosas más en el archivo URDF, incluidas las transmisiones, y un complemento de Gazebo. También es necesario un archivo /*.yaml para configurar el controlador y los archivos de inicio. 

### Control de trayectoria:

Se usó la interfaz Ros Incremental (La cual se puede encontrar en: http://wiki.ros.org/motoman_driver?action=AttachFile&do=get&target=MotoRos_EDS.pdf) para definir la reaccion del controlador en respuesta a un mensaje de trayecttoria dado por los msgs o los JoinTrajectory. El programa moto_ros_interface se suscribe a un mensaje trayectoria_msgs \ JointTrajectory e interpola entre los objetivos de posición y velocidad para proporcionar un movimiento suave con aproximaciones de aceleración lineal.

## Simulacion:

1. Se crea el espacio de trabajo y nos ubicamos allí:
        mkdir -p ~/catkin_ws/src
        cd ~/catkin_ws/src

2. Se clona este repositorio como:
        git clone https://github.com/fabianrl22/ProyectoFinal_Robotica.git

3. Instalar las siguientes dependencias:
        sudo apt-get install ros-indigo-industrial-msgs
        sudo apt-get install ros-indigo-industrial-robot-simulator
        sudo apt-get install ros-indigo-industrial-robot-client
        sudo apt-get install ros-indigo-ros-controllers

4. Confirmar las dependencias:
        rosdep install -i --from-paths src

5. Hacer Catkin-make:
        cd ~/catkin_ws
        catkin_make

Una vez el The moto_ros_interface se suscriba al trajector_msgs\JointTrajectory podemos correr los Launch:

6. Se inicia la simulacion en Gazebo y el simulador de interfaz MotoRos:
        roslaunch ma1400_sim complete.gazebo.launch

7. Activamos el controlador de trayectoria: 
        rosrun ma1400_sim trajectory_control.py

8. Activamos el controlador de posicion:
        rosrun ma1400_sim position_control.py 
