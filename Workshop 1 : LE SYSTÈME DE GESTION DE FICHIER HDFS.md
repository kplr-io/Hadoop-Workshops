# Workshop 1 : LE SYSTÈME DE GESTION DE FICHIER HDFS :

**BUT DU TP**
Prendre en main et apprendre à manipuler des fichiers dans l’environnement HDFS. :heavy_check_mark: 

---
- #### Enoncé 1 : MANIPULATION Part I

:information_source: CONSULTER PREALABLEMENT LA REFERENCE DES COMMANDES USUELLES :<br/>
https://cdiese.fr/commandes-shell-courantes-pour-hdfs/

0-Accéder au container de hadoop namenode :
```console
docker exec -it namenode /bin/bash
```
  ![image](https://github.com/zineb-kplr/Hadoop-Workshops/assets/123749462/22d43971-f5e4-41de-96a6-055036d8d01a)
- Accéder au conteneur Hadoop Namenode vous permet d'interagir directement avec le système de fichiers distribué Hadoop (HDFS).
- Le Namenode est un composant essentiel de Hadoop, chargé de gérer l'espace de noms du système de fichiers et de coordonner le stockage des données dans le cluster.

1 - Télécharger le fichier suivant dans le Système linux via la commande WGET :<br/>
https://www.gutenberg.org/files/40086/40086-0.txt
```console
curl -O https://www.gutenberg.org/files/40086/40086-0.txt
```

![image](https://github.com/zineb-kplr/Hadoop-Workshops/assets/123749462/2e249879-1045-467b-aee9-989957886cf2)

2 - Renomer le fichier 40086-0.txt en moliere.txt
```console
touch doc.txt
mv 40086-0.txt doc.txt
```

![image](https://github.com/zineb-kplr/Hadoop-Workshops/assets/123749462/84c8da2a-7577-4c25-ac37-7721e52cca73)

3 - Créer un répertoire sous HDFS.

```console
hdfs dfs -mkdir /user/votre-prenom
```
- La commande hdfs dfs -mkdir /user/votre-prenom permet de créer un répertoire dans le système de fichiers distribué Hadoop (HDFS) avec le chemin /user/votre-prenom.
- Vous devez remplacer votre-prenom par votre propre prénom pour créer le répertoire correspondant.

  ![image](https://github.com/zineb-kplr/Hadoop-Workshops/assets/123749462/d51cffbe-dab3-4e75-9213-afc6978bcf78)

4 - Insérer le fichier dans ce répertoire HDFS via la commande PUT dans votre répertoire user.

```console
hdfs dfs -put /doc.txt /user/votre-prenom
```
  ![image](https://github.com/zineb-kplr/Hadoop-Workshops/assets/123749462/aedadcdb-417b-45ef-a093-088a3c4075c4)


5 - Vérifier la présence de ce fichier dans votre répertoire hdfs user via la commande LS (hdfs).

```console
hdfs dfs -ls /user/votre_prenom
```
   ![image](https://github.com/zineb-kplr/Hadoop-Workshops/assets/123749462/919d9dd3-8a20-4891-8ec5-50d8df695e3b)
---
- #### Enoncé 2 : MANIPULATION Part II

1 - Créer un répertoire hdfs “data” dans votre répertoire “user/mon_prenom”.
```console
hdfs dfs -mkdir /user/votre_prenom/data
```
 ![image](https://github.com/zineb-kplr/Hadoop-Workshops/assets/123749462/55fa9a4b-f98f-499d-82bc-afd0270fbf0c)

 2 - Déplacer le fichier doc.txt depuis hdfs dans ce répertoire data.
```console
 hdfs dfs -mv /user/votre_prenom/doc.txt /user/votre_prenom/data
```
  ![image](https://github.com/zineb-kplr/Hadoop-Workshops/assets/123749462/f0effd6a-c0bd-4cc2-b068-270d96204814)


3 - Modifier les droits hdfs de ce fichier pour le rendre accessible uniquement à vous.
```console
hdfs dfs -chmod 700 /user/votre_prenom/data
 ```
  ![image](https://github.com/zineb-kplr/Hadoop-Workshops/assets/123749462/27c9e8d9-6db9-43f0-ab21-10b00a8e3c78)

:information_source: Consulter la doc pour les commandes :  mkdir / mv / chmod / etc.)

---
- #### Enconcé 3 : EXPLORATION DES METADATA
Explorer le mapping réel des fichiers HDFS dans EXT4.
Localiser les données relatives au fichier chargé dans HDFS lors de la première partie.
* Blocs du fichier
* Mapping du fichier et des blocs
* Mapping des blocs vers les serveurs

Infos des blocs de fichiers :
```console  
hdfs fsck /user/votre_prenom/data/doc.txt -files -blocks -locations 
```  
![image](https://github.com/zineb-kplr/Hadoop-Workshops/assets/123749462/c6baf732-622c-4900-8fc5-538ea56c7170)
