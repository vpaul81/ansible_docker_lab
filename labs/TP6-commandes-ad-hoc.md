# Tester des commandes ad hoc Ansible

---

## Objectif
Cet exercice consiste à tester plusieurs commandes ad hoc Ansible pour interagir avec des nœuds distants. Vous allez utiliser des commandes pour récupérer des informations système, installer et redémarrer un service, gérer des fichiers, et bien plus encore.

---

## Prérequis
1. Un fichier d'inventaire Ansible (`inventory`) configuré avec les nœuds cibles.
2. Un accès SSH aux nœuds cibles.
3. Ansible installé sur votre machine locale.

## Commandes à tester
### Récupérer la version du noyau Linux
Exécutez la commande suivante pour afficher la version du noyau sur tous les nœuds :

```
ansible all -i inventory -m command -a "uname -r"
```
### Afficher l'utilisation de la mémoire
Utilisez cette commande pour afficher l'utilisation de la mémoire sur tous les nœuds :

```
ansible all -i inventory -m command -a "free -m"
```

### Installer Nginx
Installez le paquet nginx sur tous les nœuds :

```
ansible all -i inventory -b -m apt -a "name=nginx state=present"
```

### Redémarrer Nginx
Redémarrez le service nginx sur tous les nœuds :

```
ansible all -i inventory -b -m service -a "name=nginx state=restarted"
```

### Créer un fichier sur les nœuds cibles
Créez un fichier nommé /tmp/testfile.txt sur tous les nœuds :

```
ansible all -i inventory -m file -a "path=/tmp/testfile.txt state=touch"
```

### Modifier les permissions d'un fichier
Modifiez les permissions du fichier /tmp/testfile.txt pour le rendre accessible en lecture et écriture à tous les utilisateurs :

```
ansible all -i inventory -m file -a "path=/tmp/testfile.txt mode='0666'"
```

### Afficher l'espace disque disponible
Affichez l'espace disque disponible sur tous les nœuds :

```
ansible all -i inventory -m command -a "df -h"
```

### Afficher la mémoire disponible
Affichez la mémoire disponible sur tous les nœuds :

```
ansible all -i inventory -m command -a "free -m"
```

### Afficher la charge système
Affichez la charge système sur tous les nœuds :

```
ansible all -i inventory -m command -a "uptime"
```

### Copier un fichier local vers les nœuds distants
Copiez un fichier local nommé config.conf vers le répertoire /etc/myapp/ sur tous les nœuds :

```
ansible all -i inventory -m copy -a "src=./config.conf dest=/home/ansible_user/config.conf"
```

### Supprimer un fichier ou un répertoire
Supprimez le fichier /tmp/testfile.txt sur tous les nœuds :

```
ansible all -i inventory -m file -a "path=/tmp/testfile.txt state=absent"
