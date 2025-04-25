### Je créé un fichier chiffré pour ansible
```
ansible-vault create monfichierchiffre.yml 
```
### J’édite un fichier chiffré pour ansible 
```
ansible-vault edit monfichierchiffre.yml 
```
### Je chiffre un fichier ansible anciennement non chiffré 
```
ansible-vault encrypt monfichierexistantnonchiffre.yml 
```
### J’exécute un playbook se basant sur des éléments chiffrés 
```
ansible-playbook monplaybook.yml --ask-vault-pass
```
