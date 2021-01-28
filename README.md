# Proyecto1
#  Implementación de un sistema de percepción para el reconocimiento de seres humanos utilizando el Robot Pepper en un ambiente simulado.

## Contexto

Con el desarrollo de la robótica social, la interacción entre humanos y robots viene teniendo cabida mas a menudo en ambientes en donde comúnmente solo poblaban
humanos. Aquí encontramos a robots utilizados para dar clases académicas a niños,robot que sirven de recepcionistas, entre otros. Para una correcta interacción social, el robot tiene que tener en cuenta algunas restricciones sociales, tales como, respetar un espacio adecuado con las personas (Proxémica), no tener movimientos bruscos cuando esta cerca de una persona, no pasar por en medio de un grupo de personas, etc.
Implementar estas restricciones en un robot hace más fácil su inserción a un ambiente comúnmente poblado por humanos. Por lo tanto, hace falta que el robot presente un buen desempeño a nivel de percepción ya que es de vital importancia el reconocer y distinguir a las personas de otros objetos inertes, esto con el fin de brindar al robot información adecuada de tal manera que integre en su accionar restricciones sociales

Toda la Implementacion fue hecha en ROS Melodic and Ubuntu 18.04.

### Creditos


**Autor: [Marcos Daza Guardamino],
**Asesor: [Dennis Barrios Aranibar]

**Affiliation: [Electrical and Electronics Engineering Department, School of Electronics and Telecommunications Engineering, Universidad Católica San Pablo, Arequipa-Peru]

---

## Citas 

El metodo YOLO esta descrito en el siguiente paper: [You Only Look Once: Unified, Real-Time Object Detection](https://arxiv.org/abs/1506.02640).

Las especificacion sobre el Robot Pepper se muestran en el siguiente link: [Pepper_Robot](http://wiki.ros.org/pepper)



## Instalacion

### Dependencias

Todo la implementacion se ejecuta bajo el Sistema Operativo Robotic Operating System ([ROS]), especificamente en ROS MELODIC. Por lo tanto, se necesita instalar el distro Melodic, el siguiente link lo ayudara con estos pasos. (http://wiki.ros.org/melodic/Installation/Ubuntu).

### Implementaciones
Para una correcta instalacion del robot Pepper se debe seguir los siguientes pasos:
 
 Instalar las prinipales Dependencias del Pepper
 
    $sudo apt-get install ros-melodic-pepper-meshes
    $sudo apt-get install ros-melodic-gazebo-ros-control
    $sudo apt-get install ros-melodic-moveit*
    $sudo apt-get install ros-melodic-tf2-sensor-msgs ros-melodic-ros-control ros-melodic-ros-controllers ros-melodic-gazebo-ros ros-melodic-gazebo-plugins ros-melodic-controller-manager python-wstool ros-melodic-gazebo*

  Crear la carpeta principal 
  
    mkdir -p pepper_sim_ws/src
    cd pepper_sim_ws/src
    
  Clonar los paquetes del Robot Pepper
  
      git clone -b correct_chain_model_and_gazebo_enabled https://github.com/awesomebytes/pepper_robot
      git clone -b simulation_that_works https://github.com/awesomebytes/pepper_virtual
      git clone https://github.com/awesomebytes/gazebo_model_velocity_plugin
      git clone https://github.com/pal-robotics/ddynamic_reconfigure_python

  Compilar el programa
  
     cd ..
     catkin_make
  
  Luego de haber realizado es necesario modificar el archivo "bashrc"
  
    gedit ~/.bashrc
    export ROS_PEPPER_SIM_WS=<path_to_your_pepper_sim_ws_folder>
  
