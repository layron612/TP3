pour ajouter des dépots suplémentaire il faut ouvrir le fichier ce trouvant a cette addresse :
---
	/etc/yum.repos.d/opennebula.repo
puis ajouter ces lignes :
---
	[opennebula]
	name=OpenNebula Community Edition
	baseurl=https://downloads.opennebula.io/repo/6.8/RedHat/$releasever/$basearch
	enabled=1
	gpgkey=https://downloads.opennebula.io/repo/repo2.key
	gpgcheck=1
	repo_gpgcheck=1
pour installer le paquet EPEL il faut rentrer cette commande :
---
	sudo dnf install -y epel-release

puis pour vérifier que tout a bien fonctionner il faut utiliser cette commande :
---
	sudo dnf repolist

pour installer le paquet opennebula-node-kvm il faut faire 2 commande :
---
pour faire une mise a jours des paquets :

	sudo dnf update -y 

pour installer le paquet :

	sudo dnf install -y opennebula-node-kvm

pour démarrer le service libvirtd et faire en sorte qu'il se démarre au lancement de la machine:
---
	sudo systemctl start libvirtd
	sudo systemctl enable libvirtd

commande pour les ouvertures de port :
---
```
# Assurez-vous que firewalld est installé et démarré
sudo systemctl start firewalld
sudo systemctl enable firewalld

# Ouvrir le port 22 (TCP) pour SSH
sudo firewall-cmd --permanent --add-port=22/tcp

# Ouvrir le port 8472 (UDP) pour VXLAN
sudo firewall-cmd --permanent --add-port=8472/udp

# Recharger la configuration pour appliquer les modifications
sudo firewall-cmd --reload

# Vérifier que les ports sont ouverts
sudo firewall-cmd --list-all

```
