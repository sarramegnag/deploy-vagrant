# Installation

## Serveur de déploiement

### Création d'un nouvel utilisateur

```
ansible-playbook create-user.yml -i inventories/production -e "ansible_ssh_user=root" --ask-pass
```

### Installation Ansible

#### Debian 9 Stretch

```
# echo "deb http://ppa.launchpad.net/ansible/ansible/ubuntu trusty main" | tee -a /etc/apt/sources.list.d/ansible.list
# apt-get install dirmngr
# apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 93C4A3FD7BB9C367
# apt-get update
# apt-get install ansible
```

#### Ubuntu 18.04

```
# apt install software-properties-common
# apt-add-repository ppa:ansible/ansible
# apt update
# apt install ansible
```

## Serveur d'application

Vérifier que python 2+ est installé
```
$ python -v
```

### Création d'un nouvel utilisateur

```
# adduser deployer
# usermod -aG sudo deployer
# cp /etc/sudoers /root/sudoers.bak
# visudo
```
Ajouter en fin de liste `deployer ALL=(ALL) NOPASSWD:ALL`

### Test du nouvel utilisateur

```
# su - deployer
$ sudo whoami
```

# Exécution

```
$ ansible-playbook <playbook>.yml -i inventories/<environnement> --vault-id ../vault-password-file
```
