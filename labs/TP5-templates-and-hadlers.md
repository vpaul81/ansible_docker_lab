# Déploiement d'un serveur web avec Handlers

## Objectif 
- Installer Nginx sur un serveur Ubuntu.
- Tester un handler qui redémarre Nginx uniquement si le fichier de configuration a été modifié.

## Instructions
### 1- Playbook nginx.yml

```
---
- name: Exercice Handlers - Configuration de Nginx sur Ubuntu
  hosts: node
  become: yes

  tasks:
    - name: Installer Nginx
      ansible.builtin.apt:
        name: nginx
        state: present
        update_cache: yes

    - name: Créer un fichier de configuration personnalisé
      ansible.builtin.copy:
        src: templates/nginx.conf.j2
        dest: /etc/nginx/nginx.conf
        owner: root
        group: root
        mode: '0644'
      notify: Redémarrer Nginx

    - name: Démarrer Nginx
      ansible.builtin.service:
        name: nginx
        state: started

  handlers:
    - name: Redémarrer Nginx
      ansible.builtin.service:
        name: nginx
        state: restarted
```

### 2- Template templates/nginx.conf.j2

```
user www-data;
worker_processes auto;
pid /run/nginx.pid;

events {
    worker_connections 768;
    # multi_accept on;
}

http {
    sendfile on;
    tcp_nopush on;
    tcp_nodelay on;
    keepalive_timeout 65;
    types_hash_max_size 2048;

    include /etc/nginx/mime.types;
    default_type application/octet-stream;

    server {
        listen 80 default_server;
        listen [::]:80 default_server;

        server_name _;

        location / {
            return 200 'Hello from Ansible Handlers on Ubuntu!';
        }
    }
}

```
###  3. Exécution

Installer CURL

```
apt install curl
```

Exécutez le playbook :

```
ansible-playbook -i inventory nginx.yml
```

Vérifiez que Nginx fonctionne :

```
curl http://ansible_node1
curl http://ansible_node2
```

Modifiez le template nginx.conf.j2, par exemple en changeant le message de retour :

```
return 200 'Handler triggered successfully!';
```
Rejouez le playbook :
Vérifiez que le handler a été exécuté et que la configuration est mise à jour.

## 🔥 Challenge supplémentaire : Amélioration du Playbook

Améliorez votre solution actuelle en remplaçant l'utilisation du module `copy` par le module `template` :

- Utilisez le module **`ansible.builtin.template`** pour déployer un fichier de configuration dynamique.
- Déplacez le fichier `nginx.conf` existant dans un nouveau fichier de template : `templates/nginx.conf.j2`.
- Rendez ce fichier **dynamique** en utilisant **au moins deux variables** :
  - `nginx_listen_port` : pour définir le **port d'écoute** du serveur Nginx.
  - `nginx_server_message` : pour définir le **message retourné** par le serveur web.

Le fichier `/etc/nginx/nginx.conf` généré doit s'adapter automatiquement aux valeurs des variables.

> **Objectif** :  
> - Faciliter les changements futurs de port et de message sans modifier le template.
> - Rendre votre playbook plus flexible et maintenable.

✅ Pensez à rejouer votre playbook pour vérifier que :
