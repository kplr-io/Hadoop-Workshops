# INGESTION ANALYSE ET TRAITEMENT DE DONNEES

-Accédez au container de hive. . :
```console
docker exec -it hive-server /bin/bash
```
- Chercher un fichier CSV Open Data de taille moyenne ici
- Utiliser la commande wget DANS VOTRE REPERTOIRE LOCAL (/home/hadoop/):

```console
curl -O https://raw.githubusercontent.com/hortonworks/data-tutorials/master/tutorials/hdp/how-to-process-data-with-apache-hive/assets/driver_data.zip
```

- Unzipper le fichier :

```console
 jar xf driver_data.zip
```

- se rendre dans le repertoire :

```console
cd driver_data
```

- lister pour voir les fihiers csv existants :

```console
ls
```

- Ouvrir le fichier : head drivers.csv :

```console
head drivers.csv
```
- Lancer le shell Hive :

```console
hive
```

- Afficher les bases existantes :

```console
show databases;
```
- Construire la requête de création et de remplissage d'un tableau dans la base de donnée à partir su fichier .csv sauvegardé :
  - Définir la table associée au fichier csv dans Hive (Create Table) en respectant le schéma noté précédemment, par ewemple:
```console
  create table driver_table(
     driverId int,
     name varchar(20),
     ssn int,
     location varchar(20),
     certified char(1),
     wage_plan varchar(20)
  )
```
  - enregistrer le fichier dans votre repertoire
```console
  row format 
  delimited fields terminated by ',' 
  stored as textfile   
  location '/hive/data/votre_prenom_rep'
```
  - supprimer l'entête :
```console
  TBLPROPERTIES('skip.header.line.count'='1');
```
- La commande doit donc ressembler à (Attention à la syntaxe) :
```console
create table driver_table(
driverId int,
name varchar(20),
ssn int,
location varchar(20),
certified char(1),
wage_plan varchar(20)
)
row format 
delimited fields terminated by ',' 
stored as textfile   
location '/hive/data/votre_prenom_rep'
TBLPROPERTIES('skip.header.line.count'='1');
```
- ou bien :

```console
CREATE TABLE driver_table (driverId STRING,name STRING,ssn STRING,location STRING,certified STRING,wageplan STRING) ROW FORMAT DELIMITED FIELDS TERMINATED BY ‘,’ STORED AS TEXTFILE tblproperties(“skip.header.line.count”=“1”);
```
- SQL n'est pas sensible à la case
