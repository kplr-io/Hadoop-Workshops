# Workshop 1 : LE SYSTÈME DE GESTION DE FICHIER HDFS :

**BUT DU TP**
Prendre en main et apprendre à manipuler des fichiers dans l’environnement HDFS. :heavy_check_mark: 

---
- #### Enoncé 1 : MANIPULATION Part I

:information_source: CONSULTER PREALABLEMENT LA REFERENCE DES COMMANDES USUELLES :<br/>
https://www.formation-bigdata.com/les-commandes-hdfs/

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

