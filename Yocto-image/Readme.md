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
  
           📌 bitbake use max.4 Cores to make 2 tasks in same time but not related to each other
  
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

  ## Create Image Recipe for our Customized image:

      Follow image recipe structure (meta-grad-distro/recipes-core/images/grad-test-image.bb)

         - Include base image : ```require recipes-core/images/rpi-test-image.bb ```

         - # Customization Point: IMAGE_INSTALL

 
 ## -- ⚙️ Software Packages - Applications  ( SW layer ) --

   - Integration Nano Editor :

      Follow Layer Strucrure ( meta-features/recipes-cmd/nano )

      ``` recipetool create -o nano_1.0.bb https://www.nano-editor.org/dist/v7/nano-7.2.tar.xz ```
     
      ``` bitbake nano ```
     
  - Integration C++ Applications & Open Streat map scripts

      create new layer : ``` mkdir meta-apps ```   in poky

                        ``` bitbake-layers add-layer ../meta-apps ```  in Gradution_rpi

      create recipes :

     Upstreams :
    
     1- AWS Application recipe  (meta-apps/recipes-aws/aws/aws_1.0.bb)

     2- uart Application recipe (meta-apps/recipes-uart/uart/uart_1.0.bb)

     3- Main Application recipe (meta-apps/recipes-main/main/main_1.0.bb)

     ![Screenshot from 2025-06-15 23-16-57](https://github.com/user-attachments/assets/ca807044-36a8-4746-841a-f1e394fbb2f6)
    

     - Service files ( auto-run script after booting ) : main.service


      - Follow recipe structure :

                   # TODO 1: Documentation Varaibles ( SUMMARY - DESCRIPTION - HOME_PAGE )
    
                   # TODO 2: License Varaialbes      ( LICENSE - LIC_FILES_CHKSUM )
    
                   # TODO 3: Source Vraiables        ( SRC_URI - SRCREV - S )
    
                   # TODO 4 : Resolve dependancy     ( DEPENDS )
    
                   # TODO 5: Recipe Tasks


     4- OSM Scripts recipe  (meta-apps/recipes-osm/osm/osm_1.0.bb)

      ![Screenshot from 2025-06-15 23-05-39](https://github.com/user-attachments/assets/e684ed67-6c12-4ab2-a720-66d4e79b3247)


       - Scripts : app.py - request.py - intialize_db.py
   
       - Service files ( auto-run script after booting ) : db.service - app.service
   
    
 

     

     

