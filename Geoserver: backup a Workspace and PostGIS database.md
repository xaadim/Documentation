![alt tag](#)
- Depuis putty en ligne de commande ou depuis winscp: Récpération du Workspace
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
	
Dans cet article, je vous montre une installation rapide du Framework Symfony2 sur une distribution Ubuntu. Le même processus d’installation peut être utilisé pour les autres distributions de Linux.

Pour installer Symfony2, il faut d'abord un environnement de travail qui va accueillir l'installation du Framework.
<h4><strong>1- Installation PHP, Apache et MySql/PostgreSQL/PostGis</strong></h4>
Installons d'abord les paquets nécessaires au fonctionnement de l'application. Nous allons utiliser les lignes de commande. Pour la base gestion de la base de données, nous êtes libre de choisir entre MySql ou PostgreSql. Dans cet exemple, nous installons MySql.

Lançons les commandes maintenant avec sudo qui permet d'avoir tous les droits nécessaires pour installer ces paquets:
<pre class="lang:default decode:true">sudo apt-get install apache2
sudo apt-get install php5
sudo apt-get install libapache2-mod-php5
sudo apt-get install mysql-server
sudo apt-get install php5-mysql
sudo apt-get install php-apc
sudo apt-get install php5-intl
</pre>
Une fois les paquets installés, redémarrons le serveur apache.
<pre class="lang:default decode:true">sudo /etc/init.d/apache2 restart
</pre>
Maintenant, il faut vérifier l'installation. Taper 127.0.0.1 en localhost ou l'adresse de votre serveur si vous en utiliser un. Une page vous dira si ça marche ou pas. Si tel n'est pas le cas, vérifier le fichier error.log, pour en connaître la raison, situé dans le répertoire var/log/apache2/.
<h3>2- Pré-requis pour Symfony2</h3>
Avant de passer maintenant à l'installation de notre Framework, nous devons nous assurer que certaines configuration du serveur sont bien définies.

Ces vérifications se font dans le fichier php.ini se trouvant dans /etc/php5/apache2/php.ini. Pour le modifier nous utilisons l'éditeur de texte nano. Tapez la commandes suivantes pour ouvrir le fichier dans l'éditeur:
<pre class="lang:default decode:true">sudo nano /etc/php5/apache2/php.ini</pre>
Dans ce fichier, il est recommandé que ces directives soient à off :
<strong>magic_quotes_gpc</strong>
<strong>register_globals</strong>
<strong>session.auto_start</strong>
<strong>short_open_tag</strong>

Il faut aussi que ajouter une valeur à la directive date.timezone.

Exemple:
<pre class="lang:default decode:true ">date.timezone = Europe/Paris</pre>
Enregistrer les modifications effectuées et redémarrer encore apache.
<pre class="lang:default decode:true ">sudo /etc/init.d/apache2 restart</pre>
<h3>3- Installation de Composer</h3>
Composer permet d'installer nos bibliothèques en ligne de commande. L'installation de curl est obligatoire pour l'installation. Pour vérifier si curl est installé, faites:
<pre class="lang:default decode:true ">dpkg -l | grep -i curl</pre>
Si le paquet est installé vous verrez des informations sinon rien ne s'affiche.

Pour l'installer, faites un
<pre class="lang:default decode:true ">sudo apt-get install curl</pre>
Installons maintenant composer:
<pre class="lang:default decode:true ">curl -sS https://getcomposer.org/installer | php</pre>
Maintenant, créer un répertoire pour votre projet Symfony2 et déplacer composer dans ce répertoire.  Cela permet d'extraire les bibliothèques que télécharge composer dans votre projet.
<h3>4- Installation de Symfony2</h3>
Maintenant que tous les pré-requis configurés, nous pouvons télécharger et installer le Framework:
<pre class="lang:default decode:true">php composer.phar create-project symfony/framework-standard-edition Symfony 2.7</pre>
Vous pouvez regarder la dernière version sur <a href="http://symfony.com/download">http://symfony.com/download</a>

Un dossier Symfony sera créé dans votre répertoire. Vous pouvez le renommer comme vous voulez.  Mettez à jour les dépendances installées, en déplaçant  composer.phar dans le dossier Symfony (ou renommé) créé pendant l'installation de Symfony2:
<pre class="lang:default decode:true ">sudo php composer.phar update</pre>
Pour finir, mettez les droits sur les répertoires cache et logs du répertoire app,  pour éviter les erreurs d'écriture, avec la commande chmod:
<pre class="lang:default decode:true ">sudo chmod -R 777 app/cache app/logs</pre>
Voyons si notre environnement est bien configuré, avec la commande check.php:
<pre class="lang:default decode:true ">php app/check.php</pre>
&nbsp;
http://khadimdev.com/blogdev/2015/10/10/symfony2-installation-sous-linux-ubuntu/

