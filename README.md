# Devoir-Linux
Installation des paquets Mysql, Apache et PHP a partir des sources sous la distribution Ubuntu de Linux

    I. Installation de Mysql: 
           L’installation de Mysql à partir du code source sous Ubuntu Linux se fait généralement en 5 étapes
           1) Téléchargement du code source: 
                   On peut télécharger MySQL pour Linux à partir du site officiel de MySQL: 
                   https://dev.mysql.com/downloads/mysql/
	    2) Décompression et désarchivage des sources: 
		     _J’ai mis le code source téléchargé sous /home/mit/Devoir
		     _Je me déplace dans le repertoire Devoir:
				$cd devoir
		     _J’ai décompressé et désarchiver en même temps le fichier 
			mysql-8.0.36.tar.qz en executant la commande:
				$tar mysql-8.0.36.tar.gz
                             A l’issue de la décompression, un nouveau dossier “mysql-8.0.36 sous /home/mit/Devoir est crée.
	   
             3) Configuration:
			_Je me deplace dans le repertoire nouvellement crée 
				$cd mysql-8.0.36
			_ Je crée un repertoire build, puis je me déplace dedans
				$mkdir build
				$cd build
			_ J’installe la commande cmake (commande pour 				générer les fichiers de configuration):
				$sudo apt-get install cmake
			_ J’execute la commande cmake
				$cmake ..
			Là, j’ai rencontré une erreur de configuration comme 			suit: “ Cmake Error at cmake/boost.cmake:108 (MESSAGE):....
.......You can download boost manually, from https://boostorg.jfrog.io/artifactory/main/release/1.77.0/source/boost_1_77_0.tar.bz2”
			Le message  d’erreur signifie que je doit installer un boost; alors j’ai télécharger un code source de boost : boost_1_77_0.tar.gz que j’ai mis sous /home/mit/Devoir. Puis j’installe le paquetage.
			_ Je reviens dans le repertoire Devoir: 
				$cd ..
			_ Je décompresse et désarchive ce source puis je me déplace dans le répertoire nouvellement crée.
				$tar -jxvf boost_1_77_0.tar.bz2
				$cd boost_1_77_0
			_ J’execute les commandes de configuration de ce paquet 
				$./bootstrap.sh
				$./b2
			_ Installation du paquetage: 
				$./b2 install
			_ Après l’installation je me déplace dans la répertoire build puis je réexecute la commande cmake.
				$cd mysql-8.0.36/build
				$cmake ..
			La configuration c’est déroulée sans erreur 
	   4) Compilation: 
 		    La compilation se fait dans le même répertoire par la commande make 
				$make
	 5) Installation:
		   L’installation se fait avec la commande: 
				$sudo make install
		  Pour vérifier l’installation, il suffit d”executer la commande suivante: 
			/usr/local/mysql/bin/mysql --version 

II.  Installation de Apache:

	1) Téléchargement du code source:
		Télécharger la source dans le site: 
		https://httpd.apache.org/download.cgi#apache24

	2) Décompression des sources:
	J’ai mis le source sous /tmp/ sous la forme d’un fichier httpd-2.4.59.tar.bz2. J’ai décompressé les sous /usr/local/src.
		Je me connecte en tant que root: 
			$sudo su root
		Je me déplace dans /usr/local/scr
			#cd /usr/local/src
		Je passe à la décompression
			#tar -jxvf /tmp/httpd-2.4.59.tar.bz2
		A l’issue de la décompression, il y a un nouveau dossier httpd-2.4.59 sous /usr/local/src

	3) Configuration de l’environnement
		Allez dans le répertoire nouvellement créé 
			#cd /usr/local/src/httpd-2.4.59
		Lancer la configuration préparatoire à la compilation 
			#./configure –prefix=/usr/local/httpd-2.4.59
		L’éxecution se termine par un message d’erreur: 
		“APR not found. Please read the documentation.”
		J’ai consulté la documentation puis j’ai su que je doit installer deux paquetage: libapr1-dev et libaprutil1-dev.
			#apt-get install libapr1-dev libaprutil1-dev
		Après, j’ai relancé la commande ./configure et la configuration est terminée avec succès
	4) Compilation:
		La script de configuration s’est dérouleé sans incident, et ja passe à la compilation 
			#make
	5)Installation
		Une fois la compilation terminé j’installe le serveur:
		 	#sudo make install
		J’ai ensuite vérifié si la serveur a bien été installé en éxecutant la commande: 
			#/usr/local/httpd-2.4.59/bin/httpd -v
III. Installation de PHP
	1)Téléchargement des sources: 
		Les sources de PHP sont disponibles à l’adresse: 
		http://www.php.net/downloads.php
		J’ai mis les sources sous /tmp/ sous la forme d’un fichier php-8.3.6.tar.bz2.
	
	2)Décompression des sources
		Je me connecte en tant que root puis j’ai décompresser les sources sous usr/local/scr/
			$sudo su root
			#cd /usr/local/scr
			#tar -jxvf /tmp/php-8.3.6.tar.bz2
	A l’issue de la décompression, un nouveau dossier php-8.3.6  été créée sous /usr/local/scr.
	3) Configuration de l’environnement
		Je me déplace dans le répertoire nouvellement créé et taper la commande de configuration 
			#cd php-8.3.6 
			#./configure --prefix=/usr/local/php-8.3.6
		Lors de l’éxecution, la commande s’arrête brutalement avec un message d’erreur lié à l’abscence d’une bibliothèque dans mon environnement de compilation:
		“ configure: error: xml2-config not found.Please check your libxml2 installation”.
		J’ai alors installé le paquetage libxml2-dev et relancé la commande
		#apt-get install libxml2-dev
		#./configure --prefix=/usr/local/php-8.3.6
	Là, il y avait encore une autre erreur: 
		“configure: error: Package requirements (sqlite3 > 3.7.4) were not met: No package ‘sqlite3’ found”. 
	J’ai alors installé le paquetage libsqlite3-dev et relancé la commande.
		#apt-get install libsqlite3-dev
		#./configure –prefix=/usr/local/php-8.3.6
	La configuration s’est déroulée avec succès.
	4) Compilation
		La compilation se fait en éxecutant la commande make
			#make
	5) Installation
		Une fois la compilation terminée il est possible d’installer PHP (dans l’espace défini par l’option --prefix de la commande configure) par la commande: 
			#make install
		Les commandes PHP se trouvent alors dans le dossier bin/ de l’endroit où il a été installé et le mien se trouve donc dans /usr/local/php-8.3.6/bin/.
	6) Test d’installation
  		J’ai fais un test rapide en éxecutant la commande:
			#/usr/local/php-8.0.6/bin/php -v 
		Ce commande permet de vérifier le bon fonctionnement et la version.
