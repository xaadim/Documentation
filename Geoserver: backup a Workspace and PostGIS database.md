### Récupérer un Workspace de Geoserver d'un serveur à un autre ainsi que sa base de données PostGIS.
<h4>le Workspace Géoserver</h4>
Nous essayons de récuperer le workspace de SDIS35 dans cet exemple. La première chose à faire est de trouver le répertoire de données de Geoserver dans lequel se trouve le dossier Workspaces. Nous avons deux possibilités:
- en ligne de commande en faisant une recherche du répertoire geoserver:
	<pre class="lang:default decode:true">
		sudo find / -name "geoserver*"
	</pre>
- depuis l'interface d'administration web de Geoserver
![alt tag](https://doc-0o-58-docs.googleusercontent.com/docs/securesc/v559n3rekbtpch85mgddk9ug8mr41ack/edg1vpr1dueqh3uddqr639l18ugg8klq/1465293600000/16812825424592245321/16812825424592245321/0B0wRlQ5u5OCuNjBTcHBld3B6TUk?e=download&nonce=77n87bb7l14n8&user=16812825424592245321&hash=fd3q0ijt3smvsiocpgmpdsksth7rbpo0)- Depuis putty en ligne de commande ou depuis winscp: Récpération du Workspace
		rsync -av /repertoire_du_workspace repertoire_des_backup

- Récuperation de la base de données PostGis:
		creer un user linux systel 
		se connecter avec systel
		creer un repertoire pour les backup avec droit 777
		sudo -su systel
		dump base de donnée dans le repertoire
- Creer un scrip.php pour les sauvegardes en ligne de commande. 


Maintenant récupération des données de la VM vers Windows

- 1# Utilisez Winscp (facile)
- 2# En ligne de commande DOS : set PATH=C\vers_putty_folder
	* un seul fichier: pscp.exe systel@192.168.56.101:/repertoire_du_fichier/fichier.format repertoire_windows
	* dossier (plusieurs données) :  pscp.exe -r  systel@192.168.56.101:/repertoire_du_fichier  repertoire_windows
	* 

<pre class="lang:default decode:true">sudo apt-get install apache2
sudo apt-get install php5

</pre>


