### Pré-requis:
<h6>* Une distribution Linux (Ubuntu 16.6 dans cet exemple)</h6> http://www.ubuntu.com/download/desktop
<h6>* Un environnement Java installé</h6> http://openjdk.java.net/
<h6>* Geoserver</h6> http://geoserver.org/release/stable/
<h6>* Si vous êtes sur Windows, nous allon installer Ubuntu via Virtualbox</h6> https://www.virtualbox.org/


Pour installer Geoserver assurez-vous que l'environnement Java est d'abord installé. L'Oracle JRE est préférable, mais OpenJDK marche très bien et il est très simple à installer..

<h4><strong>1- Installation de Ubuntu 16.6 sur une machine virtuelle</strong></h4>
- Télécharger et installer VirtualBox (https://www.virtualbox.org/)
- Télécharger la version Ubuntu de votre choix (ici Ubuntu 16.6 86bits)
- Créer une machine virtuelle
- Avant de démarrer la machine, aller dans Configuration et dans Stockage, charger l'image de votre Ubuntu téléchargée
- Démarrer la machine virtuelle pour installer Ubuntu.

Vous pouvez aussi à partir des outils disponibles, créer une clé usb de démarrage pour installer Ubuntu à côté de votre Windows, voir (http://www.linuxliveusb.com/fr/home).

<h4><strong>2- Installation de OpenJDK</strong></h4>
Ouvrez votre terminal dans Ubuntu et lancez la commande suivante pour installer l'environnement Java OpenJDK:
<pre class="lang:default decode:true">
sudo apt-get install openjdk-8-jre
</pre>

<h4><strong>3- Installation de Geoserver</strong></h4>
Maintenant, vous pouvez installer Geoserver. 
- Sélectionnez la version de GeoServer que vous souhaitez télécharger. Si vous n'êtes pas sûr, sélectionnez Stable http://geoserver.org/release/stable/.
- Sélectionnez .. Platform Independent Binary ​​ sur la page de téléchargement.
- Téléchargez l'archive et décompressez dans le répertoire où vous souhaitez que le programme soit situé. Alors de préférence, il faut déplacer le dossier dans /usr/share/geoserver.
- Pour se faire, utilisez la commande <pre class="lang:default decode:true">
sudo mv /repertoire-avant/geoserver-xx /usr/share/geoserver 
</pre>
