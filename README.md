# Advanced Road Safety System based on V2V and V2C Graduation_Project
This repository contains the necessary components to build an Our System on Embedded Linux. The project is organized into three main folders: Yocto Image, C++ Applications and OpenStreet Map.

## Table of Contenet 

   - [Yocto-Image](https://github.com/MariamReda25/Graduation_Project/tree/157d8279c205ab88b2c810da7cc742985eba0954/Yocto-image)
   - [C++ Applications](https://github.com/MariamReda25/Graduation_Project/tree/72abd4bbaed951cacf6dd190cba14f200e823133/C%2B%2BApplications)
   - [OpenStreet Map](https://github.com/MariamReda25/Graduation_Project/tree/56f30d593c06f0ac8b4a7d262e7e3b40016ca933/OpenStreet%20Map)
     
## Yocto-image

The Yocto Image folder contains the necessary configurations and recipes to build the Embedded Linux distribution customized for the System. Yocto Project is used to generate a minimal and efficient Linux image that includes all the required dependencies and components for running the system.

For detailed instructions on building the Yocto image and customizing it for your target platform, please refer to the README file located within the Yocto Image folder.


## C++ Applications 

The C++ Applications folder containe used applications to build our systems (vehicle-to-vehicle & vehicle-to-cloud & Main Application & communication between raspberry pi and arduino )

For detailed information and functionalities of those applications please refer to  README file located within the C++ Applications folder.

## OpenStreet Map 

The OpenStreet Map folder contain needed scripts ( request.py - server.py - intialize_db.py - Templates folder for map ) to plot detected damages on map using flask api and sqlit3 database fro toring damages 

For detailed information about OpenStreet Map , please refer to README file within OpenStreet Map folder.
