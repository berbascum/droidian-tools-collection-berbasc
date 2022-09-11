# droidian-tools-collection-berbasc
Collection of some open source tools for Android and Droidian.

You can visit the official Droidian website:
https://droidian.org/

Only some tools are writed for me. When not, the author is mentioned.

Tools list:
 - droidian-build-docker-mgr.sh:
   Script writed by me to manage a docker container with the Droidian build environment used in the official porting guide:
   - https://github.com/droidian/porting-guide
   - You can get the script from:
     https://github.com/berbascum/droidian-kernel-build-env-docker-mgr


 - yabit.py:
   A tool writed in python by Eugenio Paolantonio to edit Android boot images.
   Can you access to copiright, license and usage information in his github repository:
   - https://github.com/g7/yabit


 - magiskboot:
   Other powerfull tool to extract boot.img images and more.
   Is the official tool that Magisk root uses to patch images.
   You can find more information in their github repository:
   - https://github.com/topjohnwu/Magisk
   - Notes:
     - Option repack:
       It's a very usefull option. With it you can repack a boot.img image. Example to replace the ramdisk, kernel, or just add a missing kernel_dtb.
       This option have 2 requirements:
       - An input image that just will be used as image template.
       - The files to be added in the new boot.img. Should be in the current directory (relative to the tool execution path)
       SINTAXIS:
       - $ magiskboot repack -n input_image output_image
