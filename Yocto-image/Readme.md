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

