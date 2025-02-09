# PMB2 Conveyor Control

## Installation

Pour pouvoir controller le tapis roulant, vous devrez installer le paquet suivant:

```bash
sudo apt install pal-ferrum-conveyor-controller pal-ferrum-conveyor-controller-msgs
```

et n'oubliez pas de ``catkin_make`` le package associé, et de source:

```bash
catkin_make_isolated --pkg pmb2_convoyer_control
```
```bash
source devel_isolated/pmb2_convoyer_control/setup.bash
```


## Via un script pré-défini

Vous pouvez utiliser le script ``conveyor_control.py``:

```bash
rosrun pmb2_conveyor_control conveyor_control.py <duration (s)> <speed> <reverse (True|False)>
```

## Via le module utilitaire

Vous aurez accès à un module utilitaire ``ConveyorController`` pour controller plus simplement le tapis roulant, exemple:

```py
#!/usr/bin/env python

import rospy

from pmb2_conveyor_control.ConveyorController import ConveyorController

# If the python node is executed as main process (sourced directly)
if __name__ == '__main__':

    duration_seconds = 3.0
    speed = 1.0
    reverse = False

    conveyorController = ConveyorController(safe_start=True)

    conveyorController.activate_convoyer(duration_seconds, speed, reverse)

    rospy.loginfo("Conveyor execution done!")
```
> ``safe_start`` défini si un sleep de durée ``safe_sleep`` devrait être exécuté après la création du publisher (ce qui peut résoudre des problèmes si le tapis roulant ne s'active pas)