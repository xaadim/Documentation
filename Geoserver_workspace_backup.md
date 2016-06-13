### Récupération d'un Workspace de Geoserver. 

<h4>1- Copie du workspace Geoserver</h4>
Nous essayons de récuperer le workspace de eca_vaud dans cet exemple. La première chose à faire est de trouver le 'GEOSERVER_DATA_DIR', c'est-à-dire, le répertoire de données de Geoserver dans lequel se trouve les workspaces. Pour trouver ce répertoire, depuis l'interface d'administration web de Geoserver, cliquer sur 'Etat du service' et vous aurez le chemin du répertoire où se trouve les données de Geoserver. 
![alt tag](http://res.cloudinary.com/systel/image/upload/v1465299032/1_is4rr0.png)

Une fois ce répertoire trouvé (geoserver_data), on récupère le workspace qui nous intéresse (eca_vaud dans cet exemple).
Cependant, avant de commencer la copie, nous allons créer un dossier en local pour nos sauvegardes. Dans cet exemple, nous le créons sous C:/temp/backup_geoserver sous le nom de 'workspaces'.

*Copie des fichiers: 
- en ligne de commande: 
	<pre class="lang:default decode:true">
		scp -rp user@host.com:/geoserver_data/ C:/temp/backup_geoserver/workspaces
	</pre>

- ou depuis WinSCP ou autre protocole SSH...

<h4>2- Récupération de la base de données PostGIS</h4>
Créer un répertoire pour le backup de la base:
<pre class="lang:default decode:true">
	mkdir /home/systel/backup
</pre>
Ajouter le droit d'écriture à ce dossier
<pre class="lang:default decode:true">
	chmod a+w /home/syel/backup
</pre>
* Si c'est une base complète à récupérer:
	<pre class="lang:default decode:true">
		sudo pg_dump -h [SERVEUR] -p [PORT]  -d [nom_de_la_base_de_donnees] > /home/systel/backup/nom_de_la_base_de_donnees.sql
	</pre>
* Si c'est un schèma ou une table précise:
	<pre class="lang:default decode:true">
	 sudo pg_dump -h [SERVEUR] -p [PORT] -d [BDD] -U [USERBDD] --column-inserts -t [SCHEMA].[TABLE] > /home/systel/backup/ma_table.sql
	</pre>
* ou plus simplement:
	<pre class="lang:default decode:true">
		pg_dump -d eca_vaud (qui est le nom de la base de données ici) > /home/systel/backup_geoserver/eca_vaud.sql
	</pre>

<h4>3- Restauration du workspace et de la base de données dans un autre serveur </h4>
a- Créer une base de données PostGIS nommée aussi eca_vaud: 
	- Sois directement via PgAdmin III
	- Sois en ligne de commande avec un utilisateur postgres
<pre class="lang:default decode:true">
	# Entrer dans psql
	sudo -su postgres psql # postgres étant ici l'utilisateur
	CREATE DATABASE eca_vaud; 
	# Se connecter à la base créée pour créér l'extention Postgis
	\connect eca_vaud
	CREATE EXTENSION postgis;
	# CRTL + D pour sortir de psql
</pre>

Maintenant, il faut restaurer la base de données dumpée précédemment dans la nouvelle base:

<pre class="lang:default decode:true">
	# Se connecter avec un utilisateur postgres
	sudo su postgres
	# Restaurer la base
	\connect eca_vaud
	CREATE EXTENSION postgis;
	# CRTL + D pour sortir de psql
</pre>

b- Avec Winscp, copier le repertoire le workspace sauvegardé précédemment dans 'GEOSERVER_DATA_DIR' du nouveau serveur.
Une fois la copie terminée, redémarrer Geoserver et se connecter à l'interface d'administration pour vérifier si la copie du workspace a bien marché. 

Si workspace copié apparait dans la liste de nos workspaces, ça marche, sinon recommencer la copie et redémarrer Geoserver. 

Dans cet exemple, le workspace eca_vaud comporte aussi un entrepôt  PostGIS dans lequel se trouvent des couches utilisés dans les agrégations de couches. Pour les restaurer tous en même temps, il faut modifier manuellement le fichier datastore.xml de l'entrepôt dans lequel Geoserver stocke les informations de connexion à la base de données de PostGIS. Ce fichier se trouve dans /workspaces/eca_vaud/eca_vaud_postgis. 

Le fichier ressemble à ça: 
```sql
<dataStore>
  <id>DataStoreInfoImpl-2624860f:15405489c07:-4592</id>
  <name>eca_vaud_postgis</name>
  <type>PostGIS</type>
  <enabled>true</enabled>
  <workspace>
    <id>WorkspaceInfoImpl-2624860f:15405489c07:-7e10</id>
  </workspace>
  <connectionParameters>
    <entry key="schema">public</entry>
    <entry key="Evictor run periodicity">300</entry>
    <entry key="Max open prepared statements">50</entry>
    <entry key="encode functions">false</entry>
    <entry key="Batch insert size">1</entry>
    <entry key="preparedStatements">false</entry>
    <entry key="database">eca_vaud</entry>
    <entry key="host">192.168.153.150</entry>
    <entry key="Loose bbox">true</entry>
    <entry key="Estimated extends">true</entry>
    <entry key="fetch size">1000</entry>
    <entry key="Expose primary keys">false</entry>
    <entry key="validate connections">true</entry>
    <entry key="Support on the fly geometry simplification">true</entry>
    <entry key="Connection timeout">20</entry>
    <entry key="create database">false</entry>
    <entry key="port">5432</entry>
    <entry key="passwd">crypt1:6s9hvZoyg1Zq0GRrMsiBUp0hpqLUNo6r</entry>
    <entry key="min connections">1</entry>
    <entry key="dbtype">postgis</entry>
    <entry key="namespace">http://systel.fr/geoserver/eca_vaud</entry>
    <entry key="max connections">10</entry>
    <entry key="Evictor tests per run">3</entry>
    <entry key="Test while idle">true</entry>
    <entry key="user">postgres</entry>
    <entry key="Max connection idle time">300</entry>
  </connectionParameters>
  <__default>false</__default>
</dataStore>
```

L'objectif est de garder l'ID du Datastore (DataStoreInfoImpl-2624860f:15405489c07:-4592) qui est déjà utilisé dans les couches qui se trouvent dans le répertoire workspace qu'on a sauvegardé. Nous allons changé donc les entrées qui se trouvent dans <connectionParameters> .... </connectionParameters>.
<br>
* Attention: on peut choisir de modifier ce fichier à la main, mais le problème va être le mot de passe qui est ici crypté. La meilleure des solutions est de tricher un peu en créant un entrepôt PostGIS sous le nom de 'test_postgis' par exemple avec en entrant les paramètres connexion de la base de données souhaitée. Un fichier datastore.xml sera alors généré dans le dossier /workspaces/eca_vaud/test_postgis. Copier les entrées dans <connectionParameters> .... </connectionParameters> pour les coller dans notre datastore.xml qui se trouve dans /workspaces/eca_vaud/eca_vaud_postgis, ainsi nous aurons toutes les paramètres de connexions ainsi que le mot de passe bien crypé. 

Redémarrer Geoserver et tester. 


