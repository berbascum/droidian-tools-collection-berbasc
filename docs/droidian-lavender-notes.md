# Notes about testing Droidian on xiaomi lavender

BOOKWORM BUGS
- The bookworm rootfs images are booting fine on xiaomi lavender, but screen is not displaying anything.

- By connecting with ssh over RNDIS and issuing next command,  instantly desktop is showed on screer.
     $ sudo echo "2047" > /sys/class/leds/lcd-backlight/brightness
     NOTE: 2047 is the defaut value on the file. So the solution is not the value itself, but the file edition itself with some permited value that modifies the file.
  But this solution is not permanent, and using it causes a one time bootloop in next reboot or poweron.

- Also tried sleeping 5 seconds phosh.service before it starts, but not works. I guess i'ts a very early problem.

- Also tried with kernel rebuild and diff of kernel .config with other working devices.

- The problem did not exist since Droidian bullseye snapshot 22, so i'm currently testing on it.

TESTING IN BUYSELLE
- After flashing Droidian rootfs snapshot 22, device boots fine and image is swhowed on screen.

- After an update and upgrade (not dist-upgrade or full-upgrade) device reboot fine

- In next steep i have updated from bookworm nightly rootfs.img next dirs:
  - "etc/apt": I find it mounting an unflashed rootfs.img
     $ rsync -av --del ./rootfs/etc/apt/  /etc/apt/ 
  - "usr/share/droidian-apt-config"
     $ rsync -av --del usr/share/droidian-apt-config/ /usr/share/droidian-apt-config/
  - "/var/lib/extrepo" (wich have updated keys for mobian and hybris repos)
  - Also needed download last Mobian repo key:
    $ wget -O - https://repo.mobian-project.org/mobian.gpg.key | sudo apt-key add -
  - Apt-get update && apt-get upgrade
    - It upgrades android-system-gsi-28

TO DO:
- Save android-rootfs.img from bullseye to compare size and contents with the bookworm one.
- Compare boot.img from zip with a yet booted one.



ERRORS WHILE UPGRADING BULLSEYE
- NEW VERSION: /etc/default/lxc-net…
  Job for lxc-net.service failed
- keyboard-configuration (1.205)…
  cat: '/sys/bus/usb/devices/*:*/bInterfaceClass': El fitxer o directori no existeix
  cat: '/sys/bus/usb/devices/*:*/bInterfaceSubClass': El fitxer o directori no existeix
  cat: '/sys/bus/usb/devices/*:*/bInterfaceProtocol': El fitxer o directori no existeix
