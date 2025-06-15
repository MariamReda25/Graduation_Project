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

   
  -- ⚙️ Raspberry Pi Board support (BSP layer) --
  
  ``` cd ~/poky ```
  
  ``` git clone -b kirkstone git://git.yoctoproject.org/meta-raspberrypi ``` (this link from 🔗 https://layers.openembedded.org/layerindex/branch/kirkstone/layers/)
