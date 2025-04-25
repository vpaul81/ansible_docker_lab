# Créer un module personnalisé Ansible  

## Créer un module personnalisé 

### Préparation de l'Environnement

- Assurez-vous qu'Ansible est installé sur votre machine.

- Créez un répertoire library/ dans votre répertoire de projet Ansible pour stocker votre module personnalisé.

### Création du Module 
- Créez un fichier Python pour votre module, par exemple greet.py, dans le répertoire library/.

- Le module doit accepter un paramètre name qui représente le nom de la personne à saluer.

- Le module doit retourner un JSON avec un message de salutation.

```
#!/usr/bin/python
# -*- coding: utf-8 -*-

from ansible.module_utils.basic import AnsibleModule

def main():
    # Définir les arguments du module
    module_args = dict(
        name=dict(type='str', required=True)
    )

    # Initialiser le module Ansible
    module = AnsibleModule(
        argument_spec=module_args,
        supports_check_mode=True
    )

    # Récupérer le paramètre 'name'
    name = module.params['name']

    # Construire le message de salutation
    message = f"Bonjour, {name} !"

    # Retourner le résultat au format JSON
    module.exit_json(changed=False, message=message)

if __name__ == '__main__':
    main()

```


### Créer le playbook pour tester le module
Fichier : test_greet.yml

```
---
- hosts: localhost
  tasks:
    - name: Saluer l'utilisateur
      greet:
        name: "Brahim"
      register: greeting

    - name: Afficher le message de salutation
      debug:
        var: greeting

```

### Lancer le playbook

Exécutez le playbook avec la commande suivante :

```
ansible-playbook -i inventory test_greet.yml
```

### Validation
Le playbook doit afficher un résultat similaire à ceci :

```
{
    "message": "Bonjour, Brahim !",
    "changed": false
}
