Installer un serveur MySQL
---
installer le rpm de mysql : 

```
	wget https://dev.mysql.com/get/mysql80-community-release-el9-5.noarch.rpm
```

installer localement le rpm : 
	
```
	sudo rpm -ivh mysql80-community-release-el9-5.noarch.rpm
```
vérifier les paquets disponibles : 
	
```
	sudo dnf search mysql
```

installer mysql comunity serveur : 
	
```
	sudo dnf install mysql-community-server 
```

activer mysqld : 
	
```
	sudo systemctl start mysqld
```

le rendre actif au démarage : 
	
```
	sudo systemctl enable mysqld
```
vérifier que tout fonctionne : 
	
```
	sudo systemctl status mysqld
```

commande pour trouver le mot de passe temporaire : 
	
```
	sudo grep 'temporary password' /var/log/mysqld.log
```

commande pour se connecter a mysql : 
---
```
	sudo mysql -u root -p
```
commande pour setup mysql :

```
	ALTER USER 'root'@'localhost' IDENTIFIED BY 'Passw0rd?';
```
```
	CREATE USER 'oneadmin' IDENTIFIED BY 'Passw0rd?';
```
```
	CREATE DATABASE opennebula;
```
```
	GRANT ALL PRIVILEGES ON opennebula.* TO 'oneadmin';
```
```
	SET GLOBAL TRANSACTION ISOLATION LEVEL READ COMMITTED;
```



commande pour ouvrir le repo de opennebula

```
	sudo nano /etc/yum.repos.d/opennebula.repo
```

information a remplir dans le repo
---
```
	[opennebula]
	name=OpenNebula Community Edition
	baseurl=https://downloads.opennebula.io/repo/6.8/RedHat/$releasever/$basearch
	enabled=1
	gpgkey=https://downloads.opennebula.io/repo/repo2.key
	gpgcheck=1
	repo_gpgcheck=1
```


pour mettre a jour le cache des paquets

```
	sudo dnf makecache -y
```


installation de opennebula
---
installer opennebula :

```
	sudo dnf install opennebula
```
```
	sudo dnf install opennebula-sunstone
```
```
	sudo dnf install opennebula-fireedge
```

ajout dans le fichier de conf se trouvant a /etc/one/oned.conf :

```
	DB = [ BACKEND = "mysql",
       SERVER  = "localhost",
       PORT    = 0,
       USER    = "oneadmin",
       PASSWD  = "also_here_define_another_strong_password",
       DB_NAME = "opennebula",
       CONNECTIONS = 25,
       COMPARE_BINARY = "no" ]
```

modification du mot de passe oneadmin 
---
il faut aller a l'addresse suivant avec les acces root : 
	
```
	/var/lib/one/.one/one_auth
```
puis modifier le mot de passe

démarage des services opennebula et opennebula-sunstone :
---
```
	sudo systemctl start opennebula
	sudo systemctl start opennebula-sunstone
```

commande pour les activer au démarage
---
```
	sudo systemctl enable opennebula
	sudo systemctl enable opennebula-sunstone
```

ouverture des ports :
---
```
	sudo firewall-cmd --zone=public --add-port=9869/tcp --permanent
```
```
	sudo firewall-cmd --zone=public --add-port=22/tcp --permanent
```
```
	sudo firewall-cmd --zone=public --add-port=2633/tcp --permanent
```
```
	sudo firewall-cmd --zone=public --add-port=4124/tcp --permanent
```
```
	sudo firewall-cmd --zone=public --add-port=4124/udp --permanent
```
```
	sudo firewall-cmd --zone=public --add-port=29876/tcp --permanent
```
```
	sudo firewall-cmd --reload
```
```
	sudo firewall-cmd --zone=public --list-ports
```



