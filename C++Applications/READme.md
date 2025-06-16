# C++ Applications
This repo. contain C++ applications are used in our systems and running in Raspberry pi.

## - Main Application 
## - Vehicle-To-Cloud 
## - Raspberry pi to ESP32 

  - This Application is designed to send an alert message to ESP32 which exists in main vehicle using UART2 by serial port (/dev/ttyAMA2) in Raspberry pi to inform driver about road damage which
    detected by AI Model then ESP32 send this message to another ESP32 which exist in another vehicle using ESP-NOW (simulate Vehicle-to-vehicle communication) to inform nearby drivers about this
    damage.
    
## - Raspberry pi to Arduino 

  - This Application is designed to send signal to Arduino using UART4 by serial port (/dev/ttyAMA4) in Raspberry pi which exists in main vehicle to take action ( Stop vehicle ) after detecting
     damage.
