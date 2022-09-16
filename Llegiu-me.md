#### droidian-tools-collection-unofficial

Col·lecció d'algunes utilitats de codi obert per a Android i Droidian.

Podeu visitar el lloc web oficial de Droidian https://droidian.org/

Només alguna d'aquestes utilitats ha estat escrita per mi. En cas contrari, menciono el desenvolupador.

Llista d'utilitats:

- droidian-build-docker-mgr.sh: Bash script escrit per un servidor que permet gestionar un contenidor docker amb l'entorn de compilació descrit a la guia oficial de portabilitat de Droidian.
        https://github.com/droidian/porting-guide
        Podeu obtenir l'script a l'enllaç: https://github.com/berbascum/droidian-kernel-build-env-docker-mgr

- yabit.py: Utilitat python escrita per l'Eugenio Paolantonio que permet editar imatges boot.img d'Android. Podeu descarregar-la, o accedir a informació com el seva llicència o sintaxis al seu repositori oficial:
        https://github.com/g7/yabit

- magiskboot: Una altra potent eina per a extreure i editar imatges boot.img d'Android. És l'eina oficial de Magisk root, amb la que modifica les imatges d'inici. Podeu trobar més informació al seu repositori de github:
        https://github.com/topjohnwu/Magisk
        Notes:
            Opció repack: És una opció realment útil. Et permet recompilar una imatge d'inici d'Android amb arxius modificats, com ara la imatge del kernel, l'initram, o afegir un arxiu kernel_dtb. Aquesta funcionalitat té 2 requeriments:
                Una imatge boot.img d'entrada que s'utilitza com a plantilla. D'ella s'extrauràn els paràmetres de la imatge per a la recompilació.
                L'arxiu o arxius modificats que substituiran els de la imatge d'entrada. Aquests arxius hanm d'estar al directori actual al moment d'executarmagiskboot. SINTAXIS:
                $ magiskboot repack -n input_image output_image
