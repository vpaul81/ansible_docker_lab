# Utilisation d'un rôle Ansible Galaxy (Installation et configuration d'Apache)  


## Installer le rôle depuis Ansible Galaxy
Utilisez la commande suivante :


```
ansible-galaxy install geerlingguy.apache
```

## Créer un playbook pour tester le rôle
Fichier : deploy_ntp.yml

```
---
- name: Installer et configurer Apache
  hosts: all
  become: true
  roles:
    - geerlingguy.apache
  vars:
    apache_listen_port: 8080

```

## Lancer le playbook
```
ansible-playbook -i inventory install_apache.yml
```

## Validation
Vérifiez que le service Apache est bien démarré :
```
sudo systemctl status apache2
```
---


# Créer un rôle Ansible pour installer et démarrer Nginx


## Objectif
Créer un rôle Ansible qui permet d'installer et de démarrer le serveur web **Nginx** sur les nœuds cibles. Le rôle doit être structuré de manière modulaire et réutilisable.

---

## Contexte
Vous êtes administrateur système et devez automatiser l'installation et la configuration de Nginx sur plusieurs serveurs. Pour cela, vous allez créer un rôle Ansible qui :
1. Installe Nginx.
2. Démarre et active le service Nginx.
3. Vérifie que Nginx est bien installé et fonctionnel.

---

## Étapes à suivre

### 1. Créer la structure du rôle
- Utilisez la commande `ansible-galaxy` pour créer la structure de base du rôle.
- Le rôle doit s'appeler `nginx_role`.

### 2. Définir les tâches
- Créez un fichier `tasks/main.yml` pour définir les tâches suivantes :
  - Installer Nginx.
  - Démarrer et activer le service Nginx.
  - Vérifier que Nginx est fonctionnel.

### 3. Tester le rôle
- Créez un playbook pour appliquer le rôle sur les nœuds cibles.
- Exécutez le playbook et vérifiez que Nginx est installé et fonctionnel.

---

## Fichiers à fournir
1. Un rôle Ansible nommé `nginx_role`.
2. Un playbook nommé `deploy_nginx.yml` pour appliquer le rôle.

---

## Validation
Après avoir exécuté le playbook, vérifiez que :
1. Nginx est installé sur les nœuds cibles.
2. Le service Nginx est actif et fonctionnel.
3. Vous pouvez accéder à la page d'accueil par défaut de Nginx via un navigateur ou une commande `curl`.

---

## Conseils
1. **Utilisez `ansible-galaxy`** : Cette commande simplifie la création de la structure d'un rôle.
2. **Testez chaque tâche** : Vérifiez que chaque tâche fonctionne avant de passer à la suivante.
3. **Explorez les modules** : Utilisez `ansible-doc <module>` pour en savoir plus sur les modules utilisés (par exemple, `ansible-doc apt`).


---

## Liens utiles
- [Documentation officielle d'Ansible](https://docs.ansible.com/ansible/latest/index.html)
- [Module `apt`](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/apt_module.html)
- [Module `service`](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/service_module.html)
- [Module `uri`](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/uri_module.html)
