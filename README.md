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



## Instalacion e Implementacion del Robot Pepper

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
  
#### Creacion de Ambiente de Simulacion
  Debido a que este proyecto esta orientado a un ambiente poblado por humanos, es necesario poner al robot en un mapa con personas.
 
  Se hace uso del mapa ISCA MUSEUM , el cual viene precagado en gazebo 9. Se busca este mapa en la pestana "Insert" para despues salvarlo y guardarlo en la carpeta
 
    ~/pepper_sim_ws/src/pepper_virtual/pepper_gazebo_plugin/worlds
    
   Modificamos el launch: Abrimos el archivo ubicado en 
 
    /pepper_sim_ws/src/pepper_virtual/pepper_gazebo_plugin/launch
     $gedit pepper_gazebo_plugin_in_office_CPU.launch

   Luego modificamos el argumento tal y como se ve en la linea siguiente, este paso se hace con el fin de llamar al mundo ISCA MUSEUM cada vez que ejecutemos nuestro programa.  
 
    <arg name="world_name" value="$(find pepper_gazebo_plugin)/worlds/museum.world"/>

   Finalmente guardamos los cambios con el nombre "pepper_gazebo_plugin_museum.launch"
   De la misma forma como se agrego el mundo ISCA MUSEUM se puede agregar los avatar (Personas) en el mundo, los cuales puedes ser ubicados de la manera que el usuario guste.
A continuacion, se va a lanzar o ejecutar al robot Pepper en el mundo ISCA MUSEUM junto con las Personas. 

    $roslaunch pepper_gazebo_plugin pepper_gazebo_plugin_museum.launch
    
### Teleoperacion del Robot Pepper     
   Rqt es una herramienta GUI principal para ROS. Este plugins que pueden ser configurado en cualquier configuración visual y cualquier número de vistas predefinidas. Para empezar ejecutamos el plugin Robot Steering. Lo que obtenemos es dos deslizadores, que representan la moción lineal y rotacional que queremos que tenga nuestro robot. En la parte superior del plugin, vemos una caja de texto con `/cmd_vel`. Alli pondremos `pepper/cmd_vel`. Representa el nombre del tema al que va dirigida la publicación.
   
    rosrun rqt_robot_steering rqt_robot_steering
    
  ![Rqt Teleoperacion:](rqt.jpg)

## Instalacion e Implementacion de YOLO para la Deteccion de Personas
 YOLO es básicamente un algoritmo de detección de objetos, es una red convolucional el cual predice múltiples cuadros delimitados. Yolo usa características de una imagen para predecir cada cuadro comparándolos con las clases que posee. YOLO divide una imagen en s x s celdas. En las que cada celda se encargara de predecir un objeto. Si el centro de ese objeto se encuentra en una celda de la cuadricula, esa celda será la responsable de la detección.
 
 
 
 
