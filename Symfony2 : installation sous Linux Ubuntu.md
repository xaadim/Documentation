Dans cet article, je vous montre une installation rapide du Framework Symfony2 sur une distribution Ubuntu. Le même processus d’installation peut être utilisé pour les autres distributions de Linux.

Pour installer Symfony2, il faut d’abord un environnement de travail qui va accueillir l’installation du Framework.

1- Installation PHP, Apache et MySql/PostgreSQL/PostGis

Installons d’abord les paquets nécessaires au fonctionnement de l’application. Nous allons utiliser les lignes de commande. Pour la base gestion de la base de données, nous êtes libre de choisir entre MySql ou PostgreSql. Dans cet exemple, nous installons MySql.

Lançons les commandes maintenant avec sudo qui permet d’avoir tous les droits nécessaires pour installer ces paquets:


sudo apt-get install apache2
sudo apt-get install php5
sudo apt-get install libapache2-mod-php5
sudo apt-get install mysql-server
sudo apt-get install php5-mysql
sudo apt-get install php-apc
sudo apt-get install php5-intl
1
2
3
4
5
6
7
sudo apt-get install apache2
sudo apt-get install php5
sudo apt-get install libapache2-mod-php5
sudo apt-get install mysql-server
sudo apt-get install php5-mysql
sudo apt-get install php-apc
sudo apt-get install php5-intl
Une fois les paquets installés, redémarrons le serveur apache.


sudo /etc/init.d/apache2 restart
1
sudo /etc/init.d/apache2 restart
Maintenant, il faut vérifier l’installation. Taper 127.0.0.1 en localhost ou l’adresse de votre serveur si vous en utiliser un. Une page vous dira si ça marche ou pas. Si tel n’est pas le cas, vérifier le fichier error.log, pour en connaître la raison, situé dans le répertoire var/log/apache2/.

2- Pré-requis pour Symfony2

Avant de passer maintenant à l’installation de notre Framework, nous devons nous assurer que certaines configuration du serveur sont bien définies.

Ces vérifications se font dans le fichier php.ini se trouvant dans /etc/php5/apache2/php.ini. Pour le modifier nous utilisons l’éditeur de texte nano. Tapez la commandes suivantes pour ouvrir le fichier dans l’éditeur:


sudo nano /etc/php5/apache2/php.ini
1
sudo nano /etc/php5/apache2/php.ini
Dans ce fichier, il est recommandé que ces directives soient à off :
magic_quotes_gpc
register_globals
session.auto_start
short_open_tag

Il faut aussi que ajouter une valeur à la directive date.timezone.

Exemple:


date.timezone = Europe/Paris
1
date.timezone = Europe/Paris
Enregistrer les modifications effectuées et redémarrer encore apache.


sudo /etc/init.d/apache2 restart
1
sudo /etc/init.d/apache2 restart
3- Installation de Composer

Composer permet d’installer nos bibliothèques en ligne de commande. L’installation de curl est obligatoire pour l’installation. Pour vérifier si curl est installé, faites:


dpkg -l | grep -i curl
1
dpkg -l | grep -i curl
Si le paquet est installé vous verrez des informations sinon rien ne s’affiche.

Pour l’installer, faites un


sudo apt-get install curl
1
sudo apt-get install curl
Installons maintenant composer:


curl -sS https://getcomposer.org/installer | php
1
curl -sS https://getcomposer.org/installer | php
Maintenant, créer un répertoire pour votre projet Symfony2 et déplacer composer dans ce répertoire.  Cela permet d’extraire les bibliothèques que télécharge composer dans votre projet.

4- Installation de Symfony2

Maintenant que tous les pré-requis configurés, nous pouvons télécharger et installer le Framework:


php composer.phar create-project symfony/framework-standard-edition Symfony 2.7
1
php composer.phar create-project symfony/framework-standard-edition Symfony 2.7
Vous pouvez regarder la dernière version sur http://symfony.com/download

Un dossier Symfony sera créé dans votre répertoire. Vous pouvez le renommer comme vous voulez.  Mettez à jour les dépendances installées, en déplaçant  composer.phar dans le dossier Symfony (ou renommé) créé pendant l’installation de Symfony2:


sudo php composer.phar update
1
sudo php composer.phar update
Pour finir, mettez les droits sur les répertoires cache et logs du répertoire app,  pour éviter les erreurs d’écriture, avec la commande chmod:


sudo chmod -R 777 app/cache app/logs
1
sudo chmod -R 777 app/cache app/logs
Voyons si notre environnement est bien configuré, avec la commande check.php:


php app/check.php
1
php app/check.php
