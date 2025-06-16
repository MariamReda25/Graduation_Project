# C++ Applications
This repo. contain C++ applications are used in our systems and running in Raspberry pi.

## - Main Application 
## - Vehicle-To-Cloud 

  ![image](https://github.com/user-attachments/assets/906ee357-1c49-4402-b6d3-e28a239be89f)

## - Raspberry pi to ESP32 

  - This Application is designed to send an alert message to ESP32 which exists in main vehicle using UART2 by serial port (/dev/ttyAMA2) in Raspberry pi to inform driver about road damage which
    detected by AI Model by displaying alert message on LCD then ESP32 send this message to another ESP32 which exist in another vehicle using ESP-NOW (simulate Vehicle-to-vehicle communication) to
     inform nearby drivers about this damage.

    ![image](https://github.com/user-attachments/assets/9888d483-9af4-4ca9-9766-1625770648a5)

    
## - Raspberry pi to Arduino 

  - This Application is designed to send signal to Arduino which exists in main vehicle using UART4 by serial port (/dev/ttyAMA4) in Raspberry pi to take action ( Stop vehicle ) after detecting
     damage.

    ![image](https://github.com/user-attachments/assets/7536c4c6-11b5-488b-a295-05913424de47)
