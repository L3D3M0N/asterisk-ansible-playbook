**1. Configuration Initiale et Dépendances :

Objectif : Préparer le serveur en s'assurant qu'il a les outils nécessaires pour compiler et exécuter Asterisk.
Actions :
Mise à jour des paquets : Le playbook commence par mettre à jour la liste des logiciels disponibles sur le serveur. C'est une bonne pratique pour s'assurer d'avoir les dernières informations sur les paquets.
Installation des dépendances : Une longue liste de paquets est installée. Ces paquets sont des bibliothèques et des outils de développement dont Asterisk a besoin pour être compilé (transformé en un programme exécutable) et pour fonctionner correctement. Cela inclut des outils comme des compilateurs, des bibliothèques pour la gestion du son, des protocoles réseau, etc.
**2. Téléchargement et Préparation des Sources d'Asterisk :

Objectif : Obtenir le code source d'Asterisk à partir du site officiel.
Actions :
Création d'un répertoire : Un dossier /usr/src/asterisk est créé sur le serveur. C'est un endroit courant pour stocker le code source des logiciels que l'on compile.
Téléchargement du code source : Le playbook télécharge un fichier compressé (.tar.gz) contenant tout le code source de la dernière version stable d'Asterisk 22 depuis le site web officiel.
Extraction du code source : Le fichier compressé est décompressé dans le répertoire /usr/src/asterisk/. Cela crée un nouveau dossier contenant les fichiers sources d'Asterisk.
**3. Compilation d'Asterisk :

Objectif : Transformer le code source d'Asterisk en un programme exécutable que le serveur peut comprendre et lancer.
Actions :
Compilation ( make -j $(nproc) ) : La commande make est utilisée pour lancer le processus de compilation. L'option -j $(nproc) indique à make d'utiliser tous les processeurs disponibles sur le serveur pour accélérer la compilation, ce qui peut prendre un certain temps.
**4. Installation d'Asterisk :

Objectif : Copier les fichiers compilés d'Asterisk aux bons endroits sur le système afin qu'il puisse être exécuté.
Actions :
Installation ( make install ) : La commande make install copie les fichiers exécutables d'Asterisk, les bibliothèques et d'autres fichiers nécessaires dans les répertoires appropriés du système (comme /usr/local/bin, /usr/local/lib, etc.).
**5. Installation des Configurations et Scripts de Démarrage :

Objectif : Mettre en place les fichiers de configuration de base et les outils pour démarrer et arrêter Asterisk facilement.
Actions :
Installation des exemples de configurations ( make samples ) : Des fichiers de configuration d'exemple sont installés dans le répertoire /etc/asterisk/. Ces fichiers contiennent des exemples de paramètres pour configurer différents aspects d'Asterisk. Vous devrez probablement modifier ces fichiers pour adapter Asterisk à vos besoins spécifiques.
Installation des scripts d'initialisation ( make config ) : Des scripts qui permettent de démarrer, d'arrêter et de gérer le service Asterisk sont installés. Dans ce cas, il s'agit probablement de scripts pour systemd, le système de gestion des services utilisé par de nombreuses distributions Linux modernes.
**6. Démarrage et Activation du Service Asterisk :

Objectif : Lancer Asterisk et s'assurer qu'il démarre automatiquement à chaque redémarrage du serveur.
Actions :
Activation et démarrage du service ( systemd ) : Le module systemd d'Ansible est utilisé pour activer le service asterisk. L'activation signifie que le service démarrera automatiquement lorsque le serveur sera redémarré. L'état started assure que le service est lancé immédiatement après l'installation.
