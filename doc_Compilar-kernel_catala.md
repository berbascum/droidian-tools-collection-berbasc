## 2022 ##

## Compilació kernel lavender amb halium  amb el mètode de Droidian.

- Es pot compilar amb clang (kernels nous) o amb gcc-4.9 (kernels legacy, com l de lavender?)
- El kernel source que descarrego de:
  https://github.com/droidian-lavender/kernel-xiaomi-lavender/
  està configurat per a compilar-se amb gcc-4.9 de Droidian

## Compilació amb DOCKER ##
## Preparar un debian Bookworm amd64
apt-get install build-essential docker.io
- Droidian fa servir docker per a compilar el kernel
- Seguint la porting guide, es configura automàticament tot l'entorn i dependències
## BAIXAR KERNEL SOURCE
   ## Clonació kernel lavender halium configured
   cd /media/homeper/Droidian/kernel/
   git clone https://github.com/droidian-lavender/kernel-xiaomi-lavender
## Si es vol carregar un .config anterior funcionant:
   - Copiar el .config a l'arrel del kernel sources
   - make olddefconfig # Accepta per defecte noves confs.
   - make oldconfig    # Pegunta cada nova conf trobada.
## Crear dir on es guardarà el kernel compilat
   - mkdir /media/homeper/Droidian/kernel/compilat

## Configuracions PATHS adicionals I SELECT BRANCA:
   (host)$ KERNEL_DIR="/media/homeper/Droidian/kernel/kernel-xiaomi-lavender"
   (host)$ PACKAGES_DIR="/media/homeper/Droidian/kernel/compilat"
   (host)$ mkdir -p $PACKAGES_DIR
   (host)$ cd $KERNEL_DIR
   (host)$ git checkout -b bookworm

## INICIAR DOCKER instal·lant el build-essential de droidian:
   - (host)$ docker run --rm -v $PACKAGES_DIR:/buildd -v $KERNEL_DIR:/buildd/sources -it quay.io/droidian/build-essential:bookworm-amd64 bash

## Install dins de docker
   - (docker)# apt-get install linux-packaging-snippets vim
   - Al Droidian Porting Guide s coniguren uns arxius que el kernel que utilitzo ja té creat i configurats
, per tant les següents comandes no cal executar-les:
     - (docker)# cd /buildd/sources
     - (docker)# mkdir -p debian/source
     - (docker)# cp -v /usr/share/linux-packaging-snippets/kernel-info.mk.example debian/kernel-info.mk
     - (docker)# echo 13 > debian/compat
     - (docker)# echo "3.0 (native)" > debian/source/format
     - (docker)# cat > debian/rules <<EOF
     - #!/usr/bin/make -f
     - include /usr/share/linux-packaging-snippets/kernel-snippet.mk
     - %:
     - dh \$@
     - EOF
     - (docker)# chmod +x debian/rules
## permisos a debian rules
 chmod +x debian/rules

## RECREAR DEBIAN/CONTROL:
   - cd /buildd/sources
   - rm -f debian/control
   - debian/rules debian/control

## Iniciar compilació baixant entorn si no hi és:
   ## INSTALA ELS COMPILADORS NECESSARIS DE DROIDIAN.
   (docker)# RELENG_HOST_ARCH="arm64" releng-build-package



## FINAL COMPILACIÓ
- S'HAURAN GENERAT VARIS .deb
- Descomprimir el deb del bootimg:
  - dpkg-deb --extract arxiu.debv ./
- Flashejar imatges dbto boot vbmeta

## PROBLEMES DETECTATS
- La imatge boot.img generada no conté el kernel_dtb, per tant els sistema no arrenca.
- Possible limitació de l'eina mkbootimg?
- Solució temporal:
  - Obtenir l'arxiu kernel_dtb:
    cp ./out/KERNEL_OBJ/target-dtb kernel_dtb
  - Amb l'eina yabit afegir l'arxiu kernel_dtb a la imatge
    # Baixar yabit: https://github.com/g7/yabit




## OBSOLET: INSTAL DEPENDÈNCIES MANUAL ##
## Creació base dir compiladors
mkdir /media/homeper/Droidian/kernel/compilers -p
cd /media/homeper/Droidian/kernel/compilers
## Clonació repos compiladors
   ## Clona clang-android-6.0-4691093 de Droidian per a kernel Android 9
   git clone https://github.com/droidian/android-platform-prebuilts-clang-host-linux-x86-28
   ## Clona gcc de Droidian per a kernel Android 9
   git clone  https://github.com/droidian/android-platform-prebuilts-gcc-aarch64-linux-android-4.9
## Clonació kernel lavender halium configured
cd /media/homeper/Droidian/kernel/
   git clone https://github.com/droidian-lavender/kernel-xiaomi-lavender
## Configurar VARS paths
   - export ANDROID_GCC_PATH='/media/homeper/Droidian/kernel/compilers/android-platform-prebuilts-gcc-aarch64-linux-android-4.9/bin'
   - export PATH="$ANDROID_GCC_PATH:$PATH"
   - export ARCH='arm64' # Ja està configurada a l'arxiu de config del kernel del dir debian/kernel-info.mk
   - #export CROSS_COMPILE=aarch64-linux-android-
  - Creo un script setbuildenv.sh que les defineix
## Configurar debian/kernel-info.mk
   BUILD_PATH = /media/homeper/Droidian/kernel/compilers/android-platform-prebuilts-clang-host-linux-x86-28/clang-4691093/bin/


