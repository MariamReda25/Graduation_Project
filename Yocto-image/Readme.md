# Start to customize image for Graduation Project #

## 📌 Pre-Development Stage :

- 1️⃣ Prepare Host Machine with Hardware and Software Requirements: 🔗 (https://docs.yoctoproject.org/ref-manual/system-requirements.html )

- 2️⃣ Choose YOCTO Realese : 🔗 (https://wiki.yoctoproject.org/wiki/Releases )
  
  Release choice decision --> Kirksone ✅
  
   1- Long term support ( request for help for non-common issue

   2- Old since 2022 so it used in development ( search for common issues)

- 3️⃣ Clone Pokey: 🔗(https://github.com/yoctoproject/poky)
  
  ```git clone https://github.com/yoctoproject/poky.git```
  
  ```cd poky```
  
  ```git checkout kirkstone```
  
  ## 📌 Development Stage :

  1️⃣ source "oe-init-build-env" script
 
    ```source oe-init-build-env Graduation_rpi5 ```

  2️⃣ Start integration needed Applications and Packages using Bottom-Up approach:

  ![image](https://github.com/user-attachments/assets/36ca6c7f-c206-46f8-8a98-c9b574222b69)

   
   ## -- ⚙️ Raspberry Pi Board support (BSP layer) --
  
            ``` cd ~/poky ```
  
            ``` git clone -b kirkstone git://git.yoctoproject.org/meta-raspberrypi ``` (this link from 🔗 https://layers.openembedded.org/layerindex/branch/kirkstone/layers/)

            ``` cd Graduation_rpi5 ```

            ``` bitbake-layers add-layer ../meta-raspberrypi ```
  
      📝 Edit Graduation-rpi5/conf/local.conf :

           1- specify machine 

            ``` MACHINE ??= "raspberrypi5" ```

          2- YOCTO Optimization

           📌 make downloads and state-cache shared between different images :
 
              ``` DL_DIR ?= "${TOPDIR}/../shared_yocto_space/downloads" ```

              ``` SSTATE_DIR ?= "${TOPDIR}/../shared_yocto_space/state-cache" ```
  
           📌 bitbake use max.4 Cores to run 4 tasks in same time but not related to each other
  
               ``` BB_NUMBER_THREADS="4" ```

           📌 bitbake use 4 cores when compile to speed up compilation process
  
               ```  PARALLEL_MAKE="-j 4" ```

   ## -- ⚙️ Distribution ( Distro layer ) --

    1- Follow structure of distribution layer (meta-grad-distro/conf/distro/grad.conf)

          Configuration File Structure 📃:
  
              - Distribution Information
  
              - SDK Information
  
              - Distribution Featrures :
  
                    DISTRO_DEFAULT_DISTRO_FEATURES = Values ( SW Layers ‘apps’)
  
                    DISTO_FEATURES = ${DISTRO_DEFAULT_DISTRO_FEATURES}
  
              - Preferred for Package version ( Linux Version )
 
   2- Add systemd as init process :

     - Follow structure ( meta-grad-distro/conf/distro/include/systemd.inc )

     - Require file in grad.conf file

   📝 Return back to Edit Graduation-rpi5/conf/local.conf :

     📌 Specifiy distribution of image 

          ``` DISTRO ?= "grad" ```
   3- Add Layer :

       ``` cd ~/poky/Gradution-rpi5 ```

       ``` bitbake-layers add-layer ../meta-grad-distro ```
  
  ## Build Testing Image for raspberry pi 5 :

      ``` bitbake rpi-test-image ```
 
  ## -- ⚙️ Software Packages - Applications  ( SW layer ) --

   - Integration Nano Editor :

      Follow Layer Strucrure ( meta-features/recipes-cmd/nano )

      ``` recipetool create -o nano_1.0.bb https://www.nano-editor.org/dist/v7/nano-7.2.tar.xz ```
     
      ``` bitbake nano ```
     
  - Integration C++ Applications & Open Streat map scripts

      create new layer : ``` mkdir meta-apps ```   in poky

                        ``` bitbake-layers add-layer ../meta-apps ```  in Gradution_rpi

      create recipes :
    
            - Follow recipe structure :

                    # TODO 1: Documentation Varaibles ( SUMMARY - DESCRIPTION - HOME_PAGE )
    
                    # TODO 2: License Varaialbes      ( LICENSE - LIC_FILES_CHKSUM )
    
                    # TODO 3: Source Vraiables        ( SRC_URI - SRCREV - S )
    
                    # TODO 4 : Resolve dependancy     ( DEPENDS )
    
                    # TODO 5: Recipe Tasks


           1- vehicle to cloud Application recipe  (meta-apps/recipes-v2c/vehicleToCloud/vehicleToCloud.0.bb)

           2- vehicle to vehicle Application recipe (meta-apps/recipes-v2v/vehicleToVehicle/vehicleToVehicle_1.0.bb)

           3- Main Application recipe (meta-apps/recipes-main/mainApplication/mainApplication_1.0.bb)

              .
    
              ├── mainApplication
    
              │   └── main.service
    
              └── mainApplication_1.0.bb

             - Service files ( auto-run script after booting ) : main.service


           4- Rasp-to-arduino Application recipe (meta-apps/recipes-arduino/arduino/arduino_1.0.bb)


           5- Open street Map Scripts recipe  (meta-apps/recipes-osm/OpenstreetMap/OpenstreetMap_1.0.bb)

               .
    
               ├── openstreetMap
    
               │   ├── app.py
    
               │   ├── app.service

               │   ├── db.service
    
               │   ├── initialize_db.py
    
               │   ├── request.py
    
               │   └── templates
    
               │       └── map.html
    
               └── openstreetMap_1.0.bb


             - Scripts : app.py - request.py - intialize_db.py
   
             - Service files ( auto-run script after booting ) : db.service - app.service
    
    - Integration AI Model :

       create new layer : ``` mkdir meta-ai ```   in poky

                          ``` bitbake-layers add-layer ../meta-ai ```  in Gradution_rpi
      
       create recipe :

          .
      
          ├── model
      
          │   ├── model.service
      
          │   ├── model_int8_openvino_model_H-20250615T193933Z-1-001.zip
    
          │   └── track.py
       
          └── model_1.0.bb

  ## Create Image Recipe for our Customized image:

      Follow image recipe structure (meta-grad-distro/recipes-core/images/grad-test-image.bb
      
         - Include base image  : ```require recipes-core/images/rpi-test-image.bb ```

         -  Customization Point: IMAGE_INSTALL (supported packages - software applications)

              # Add Aplications
  
              ``` IMAGE_INSTALL += "vehicleToCloud" ```
  
              ``` IMAGE_INSTALL += "vehicleToVehicle" ```
  
              ``` IMAGE_INSTALL += "openstreetMap"  ```
  
              ``` IMAGE_INSTALL += "mainApplication" ```
  
              ``` IMAGE_INSTALL += "model" ```
  
              ``` IMAGE_INSTALL += "arduino" ```

             # Add support package for vehicle to cloud
  
             ``` IMAGE_INSTALL += "libssl" ```

             # Add nano & ssh
  
             ``` IMAGE_INSTALL += "nano" ```
  
             ``` IMAGE_INSTALL += "openssh" ```
  
            # Add support packages for AI model & Openstreat map
  
            ``` IMAGE_INSTALL += "python3 python3-core python3-pip python3-setuptools python3-requests python3-flask" ```
  
            ``` IMAGE_INSTALL += "curl" ```
  
            ``` DEPENDS = "sqlite3" ```

         - Add Image Features  : EXTRA_IMAGE_FEATURES

  ## Add Needed Configuartions For Hardware (Raspberry pi 5) in local.conf

     1- UART ( Enables extra UART interfaces (UART2, UART3, UART4) on the Pi 5.)
  
        ``` RPI_KERNEL_DEVICETREE_OVERLAYS+= "overlays/uart2-pi5.dtbo" ```
  
        ``` RPI_KERNEL_DEVICETREE_OVERLAYS+= "overlays/uart3-pi5.dtbo" ```
        
        ``` RPI_KERNEL_DEVICETREE_OVERLAYS+= "overlays/uart4-pi5.dtbo" ```

     2- USB Camera :

        # GPU memory (minimal for USB cam)
  
       ``` GPU_MEM = "64" ```

       # Auto-load USB camera driver
  
      ``` KERNEL_MODULE_AUTOLOAD += "uvcvideo" ```

      ```` MACHINE_ESSENTIAL_EXTRA_RECOMMENDS += "kernel-module-uvcvideo" ```
  
   ## Add Needed Packages To Use Camera ( USB Camera ) in image recipe

       #Add support packages for Camera
  
       ``` IMAGE_INSTALL += "ffmpeg" ```
  
       ``` IMAGE_INSTALL += "gstreamer1.0 gstreamer1.0-libav gstreamer1.0-plugins-base gstreamer1.0-meta-base gstreamer1.0-plugins-bad gstreamer1.0-plugins-ugly gstreamer1.0-plugins-good" ```
  
       ``` IMAGE_INSTALL += "v4l-utils" ```
  
       ``` IMAGE_INSTALL += "userland" ```

  

  
  
       

          

    
 

     

     

