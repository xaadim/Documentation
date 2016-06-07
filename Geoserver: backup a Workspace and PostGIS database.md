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
