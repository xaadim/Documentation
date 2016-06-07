### Récupérer un Workspace de Geoserver d'un serveur à un autre ainsi que sa base de données PostGIS.
<h4>1- Le Workspace Géoserver</h4>
Nous essayons de récuperer le workspace de SDIS35 dans cet exemple. La première chose à faire est de trouver le répertoire de données de Geoserver dans lequel se trouve le dossier Workspaces. Nous avons deux possibilités:
- en ligne de commande en effectuant une recherche du répertoire geoserver:
	<pre class="lang:default decode:true">
		sudo find / -name "geoserver*"
	</pre>
- depuis l'interface d'administration web de Geoserver, cliquer sur 'Etat du service' et vous aurez le chemin du répertoire où se trouve les données de Geoserver. 
![alt tag](http://res.cloudinary.com/systel/image/upload/v1465299032/1_is4rr0.png)

Une fois le répertoire trouvé, on récupère le workspace qui nous intéresse (SDIS35 dans cet exemple):
- en ligne de commande: 
	<pre class="lang:default decode:true">
		# créer un répertoire pour les sauvegardes (backup) pour assurer la copie des fichiers
		sudo mkdir /home/systel/backup
		# lui attribuer tous les droits 
		sudo chmod -R 777 /home/systel/backup
		# maintenant copier le workspace SDIS35 dans notre repertoire backup
		sudo rsync -av /mnt/shared/geoserver_data /home/systel/backup
	</pre>

- ou depuis WinSCP (dans cet exemple) ou autre protocole SSH

<h4>2-Récuperation de la base de données PostGIS</h4>
- Si c'est une base complète à récupérer:
	<pre class="lang:default decode:true">
		sudo pg_dump -h [SERVEUR] -p [PORT]  -d [base_de_donnees] > /home/systel/backup/mabase.sql
	</pre>
- Si c'est un schèma ou une table précise:
	<pre class="lang:default decode:true">
	 sudo pg_dump -h [SERVEUR] -p [PORT] -d [BDD] -U [USERBDD] --column-inserts -t [SCHEMA].[TABLE] > //home/systel/backup/ma_table.sql
	</pre>


<h4> Extraction des données de la machine virtuelle (VM) vers une machine physique (Windows dans cet exemple) </h4>

- sur Winscp, copier le repertoire backup depuis serveur de la VM vers un repertoire de sauvegarde sur Windows.
- en ligne de commande DOS :
	<pre class="lang:default decode:true">
		set PATH=C\vers_putty_folder
		#copie d'un seul fichier: 
		pscp [USER]@[SERVEUR]:/repertoire_du_fichier/fichier.format repertoire_windows
		#copie d'un dossier entier : 
		pscp -r  [USER]@[SERVEUR]:/repertoire  repertoire_windows
	</pre>
	
