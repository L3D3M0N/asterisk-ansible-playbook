# Ansible : Automatisation Facile pour Serveurs

Ansible est un outil qui vous aide à contrôler plusieurs ordinateurs (serveurs) en même temps, pour faire des choses comme installer des logiciels ou changer des configurations. C'est comme donner des instructions à plusieurs personnes en même temps, de manière organisée.

**Comment ça marche (très simple) :**

1. **Liste des serveurs :** Vous dites à Ansible quels sont les serveurs que vous voulez gérer (leur adresse internet). C'est comme faire une liste d'invités.
2. **Instructions (Playbook) :** Vous écrivez un fichier (appelé "playbook") qui dit étape par étape ce que vous voulez faire sur ces serveurs. C'est comme une recette de cuisine. Ce fichier est facile à lire, comme de l'anglais simple.
3. **Lancement :** Vous dites à Ansible de prendre votre liste de serveurs et d'appliquer les instructions de votre "playbook" sur chacun d'eux.

**Exemple : Lancer Asterisk (un logiciel de téléphonie)**

Imaginez que vous voulez installer et démarrer Asterisk sur un serveur. Voici une idée simple de ce que vous diriez à Ansible dans votre "playbook" :

```yaml
---
- name: Installer et lancer Asterisk
  hosts: votre_serveur  # Le nom de votre serveur dans la liste
  become: yes         # Pour faire des choses qui nécessitent des droits d'administrateur

  tasks:
    - name: Installer le paquet Asterisk
      apt:
        name: asterisk
        state: present

    - name: Démarrer le service Asterisk
      service:
        name: asterisk
        state: started
