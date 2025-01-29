# MKS-Robin_nanos_v1.3_UART
Guide on how to configure UART on MKS Robin nano-s v1.3
You can configure in UART mode only one motor, I configured the X axis and adding sensorless homing, installing a tmc2209 driver.

HOW TO:



è possibile configurare in modalità UART un solo motore, io ho configurato l'asse X e aggiungendo il sensorless homing, installando un driver tmc2209.
Come fare:
tagliare il pin TX dal driver (così che non faccia contatto con la scheda), 4 pin lato sinistro
saldare cavetto su quel pin e cablarlo un un canale libero (es. PC7)
dissaldare i 2 pin in orizzontale e saldare un cavo sul pin DIAG da cablare su un un canale libero (es. PA9)
installare il driver modificato

modificare il printer così:

[stepper_x]
#{ TMC2209 Extruder Driver
step_pin: PA6
dir_pin: PA1
enable_pin: !PA3 #}

full_steps_per_rotation: 200
rotation_distance: 40.23
microsteps: 16
endstop_pin: tmc2209_stepper_x:virtual_endstop
position_endstop = 0
position_max = 238
homing_speed = 50
homing_retract_dist = 0

[tmc2209 stepper_x]
uart_pin: PC7
run_current:  0.6
stealthchop_threshold: 9999
interpolate: true
uart_address: 3
diag_pin: ^PA9
driver_SGTHRS: 255


Ora basta finire di seguire la guida sul sonsorless sul sito klipper
