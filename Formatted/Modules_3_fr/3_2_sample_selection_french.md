# Sélection de l'échantillon

## 1. Contexte

Dans le tutoriel précédent, nous avons conçu un échantillon en choisissant un protocole de sélection et en déterminant la taille de l'échantillon et la répartition. Dans ce tutoriel, nous allons physiquement prélever dans une zone d'étude l'échantillon que nous avons conçu. Le tirage d'un échantillon implique la création d'une *cadre d'échantillonnage* qui est une liste d'unités de population pouvant être sélectionnées pour être incluses dans un échantillon. Les unités de population de la liste sont appelées unités d'échantillonnage. En d'autres termes, une base de sondage est un dispositif qui permet d'observer la population en associant les unités de population aux unités d'échantillonnage  (Särndal et al., 1992, p. 9)[^fn1]. Dans notre cas, la base de sondage est par exemple une liste de tous les pixels qui composent la zone d'étude. Nous pourrions donc simplement exporter une liste de tous les pixels de la carte avec des identifiants uniques à partir desquels nous sélectionnons aléatoirement *n* unités. Dans le cadre d'un échantillonnage aléatoire stratifié, chaque pixel aurait, en plus de l'identifiant, un code de strate de sorte qu'un échantillon aléatoire soit sélectionné dans chaque strate. Une telle approche peut facilement devenir impraticable car le nombre d'unités de population tend à être important. Au lieu de cela, la sélection d'échantillons est prise en charge par divers outils et logiciels ; ici, nous illustrons comment dessiner un échantillon dans QGIS, Google Earth Engine/AREA2, et un script R.

## 2 Objectifs d'apprentissage

À la fin du tutoriel, les utilisateurs devraient être en mesure d'échantillonner une zone d'étude arbitraire sous SYS, SRS ou STR. L'utilisateur doit être capable de dessiner un échantillon dans QGIS sous SYS ou SRS, et un échantillon dans GEE/AREA2 sous STR.

- Apprendre à échantillonner une zone d'étude arbitraire sous SYS, SRS ou STR.
- Dessiner un échantillon dans QGIS sous SYS ou SRS.
- Prélever un échantillon dans GEE/AREA2 sous STR.

### 2.1 Prérequis pour ce module

- Révision de la terminologie pertinente pour les techniques d'échantillonnage dans le tutoriel 3.1 Terminologie, et compréhension du tutoriel 3.2 Plan d'échantillonnage pour l'estimation de la superficie et la précision des cartes.
- Il est fortement conseillé de comprendre les tutoriels précédents des modules 1 et 2.



## 2. Échantillonnage aléatoire simple et systématique dans QGIS

QGIS prend en charge l'échantillonnage de populations définies par des données vectorielles. Par conséquent, si vous voulez échantillonner dans des strates définies par un raster, vous devrez d'abord vectoriser les données raster. Ceci se fait par Raster > Conversions > Polygoniser (Raster vers Vecteur). La vectorisation pour les rasters de grande taille prend beaucoup de temps et n'est pas recommandée ; utilisez plutôt les alternatives ci-dessous. Pour les zones d'étude plus petites ou pour les plans SYS et SRS, QGIS fonctionne bien. Passons en revue les étapes nécessaires pour tirer deux échantillons sous SRS et SYS du pays de la Colombie.
#### 2.1 Simple random sampling
1. Nous avons d'abord besoin d'un fichier de format vectoriel délimite notre zone d'étude. Téléchargez un shapefile de la zone de délimitation de la Colombie ici : https://drive.google.com/file/d/1tXvczTra_5wrlXBhe00m_oKRpLK0GwwJ/view?usp=sharing
2. Affichez le fichier dans QGIS : Calque > Ajouter un couche > Ajouter une couche vectorielle et sélectionnez le fichier de forme colombiaborder.shp pour le dessiner sur le canevas.  
3. Vectoriel > Outils de recherche > Points aléatoires à l'intérieur des polygones
4. Spécifiez la limite de la Colombie comme couche d'entrée, le nombre de points comme stratégie d'échantillonnage et la taille totale de l'échantillon sous Nombre de points ; laissez la distance minimale " Enregistrer dans un fichier et cliquez sur Exécuter pour obtenir l'échantillon.

[image: SRS_QGIS.png]

#### Échantillonnage systématique 
Le tracé d'un échantillon sous SYS dans QGIS présente l'inconvénient que la population doit être rectangulaire, ce qui rend plus difficile le tracé d'un nombre exact d'unités pour une zone non rectangulaire. Nous pouvons simplement découper les unités d'échantillonnage pour la frontière de la Colombie, mais cela donnera une taille d'échantillon plus petite que celle spécifiée. Une solution consiste à définir une distance entre les unités en fonction de la taille de la zone d'étude. Par exemple, si la zone d'étude est de *x* km^2^, en fixant l'espacement entre les unités à x/100, on obtient un échantillon de 100 unités. 
1. Après avoir ajouté le fichier de données vectoriel dans le point 2.1.2 ci-dessus, allez dans Vector > Reserach Tools > Regular Points.
2. Sélectionnez comme zone d'entrée, le shapefile  de la Colombie
3. Spécifiez l'espacement des points ou le nombre de points -- si vous utilisez le premier, cochez la case "Utiliser l'espacement des points". 
4. Enregistrez dans un fichier et cliquez sur Exécuter pour dessiner l'échantillon.

[image: SYS_QGIS.png]

## 3. Echantillonnage aléatoire stratifié dans Google Earth Engine/AREA2
Dans le script du plan d'échantillonnage, nous avons estimé la taille de l'échantillon nécessaire pour atteindre une marge d'erreur de 25% de l'estimation de la zone de perturbation de la forêt, et nous avons réparti l'échantillon en strates aux fins de l'estimation de la zone. Cela a donné la taille d'échantillon suivante :

| | A             | B            | C              |D              |E             |F         |
|-|:--------------|:-------------|:---------------|:--------------|:-------------|:---------|
|1| Stratum (*h*) | Forêt (1) | Non-Forêt (2) |For. Dist. (3) |FD buf. (4)   |Total     |
|11| *nh* (final) |275      	|200	      |30	        |30              |535           |

Pour sélectionner cet échantillon, utilisons AREA2 pour sélectionner un échantillon sous échantillonnage aléatoire stratifié :
https://code.earthengine.google.com/?accept_repo=users%2Fopenmrv%2FMRV&scriptPath=projects%2FAREA2%2Fpublic%3A1.%20Sampling%20Design%2FStratified%20Random%20Sampling et spécifions le chemin d'accès à la carte de la Colombie basée sur le CODED  (https://code.earthengine.google.com/?asset=users/olofsson76/Open_MRV/Open_MRV_Col_strat_buffer)  avec un tampon sous "Spécifier la stratification/l'image pour définir la zone d'étude" ; utilisez les autres arguments par défaut ; cliquez sur "Charger l'image", ce qui affichera les zones de strates dans la Console (NOTE : cela prendra un certain temps). Sélectionnez une taille d'échantillon arbitraire sous "Determine sample size", et spécifiez sous "Allocate sample size to strata" : 275, 200, 30, 30. Cliquez sur "Create sample" -- note : ne cliquez qu'une seule fois ; il semble que GEE ne réagisse pas mais il dessine l'échantillon après que vous ayez cliqué. En cliquant sur "Add to map", les unités de l'échantillon s'afficheront sous forme de points rouges dans l'affichage de la carte. La dernière étape consiste à exporter l'échantillon : cliquez sur l'onglet Tâches, puis sur Exporter l'échantillon dans la boîte de dialogue - deux entrées nommées "sample_asset" et "sample_CSV" apparaîtront dans Tâches. Elles sont identiques, mais l'une sert à exporter l'échantillon sous forme de fichier CSV, l'autre à l'enregistrer sous forme de fichier GEE Asset à utiliser dans Google Earth Engine. Cliquez sur le bouton Exécuter juste à côté des entrées et enregistrez en tant que GEE Asset et CSV (ce dernier devrait être enregistré dans votre Google Drive). Utilisez le nom "STR_sample_Col" pour GEE Asset et le fichier CSV. 

[image: STR_AREA2.png]


## 3. Échantillonnage aléatoire stratifié dans R

La Banque Mondiale a implémenté les scripts suivants dans R qui permettent à un utilisateur de sélectionner un échantillon sous STR en utilisant une stratification au format raster. Les commentaires du code sont uniquement en français mais les instructions pour exécuter les scripts sont fournies ci-dessous [Le premier script calcule les poids des strates et peut être téléchargé ici.](https://drive.google.com/file/d/1b5kZD_Eb73MwKvWPpGIqokyJpQJZ0rZ1/view?usp=sharing): 
Il y a quelques éléments que nous devons spécifier avant de pouvoir exécuter le script. Si vous utilisez RStudio, vous devrez installer les paquets suivants : rgdal, raster et stringr.  Ensuite, après avoir ouvert le script dans RStudio, vous devez définir le répertoire de travail. Ci-dessous, le répertoire de travail est défini comme étant C:/Users/olofsson/Desktop/STR_example/ dans un système d'exploitation Windows -- changez-le pour le répertoire qui héberge votre stratification. Notez que vous devez utiliser une barre oblique "/" même lorsque vous spécifiez un répertoire Windows.

```R
###################DEFINIR DES ENTREES###############################################
#set working directory. Il faut definir ici le directoire. Il faut mettre / au lieu de \
wd <- "C:/Users/olofsson/Desktop/STR_example/"
setwd(wd)
```
Ensuite, spécifiez le nom de la stratification au format raster, la résolution spatiale de la stratification, et le nom du fichier CSV de sortie :

```R
#  lire un raster, GeoTiff ou autre. 
Raster <- raster('Col_strat_buffer_subset.tif')
 
##Resolution de la carte utilisée
Res <- 30
 
##Fichier avec les superficies par estrate
Output <- "Col_Strat_buffer_subset_Wh.csv"
```
Cela donnera les poids des strates qui peuvent maintenant être utilisés pour concevoir l'effort d'échantillonnage. (Notez qu'il existe de nombreuses autres façons de calculer les surfaces des strates, y compris la commande "GDALINFO -hist"). Maintenant, nous pouvons sélectionner l'échantillon en utilisant le deuxième script qui est accessible ici :[Maintenant, nous pouvons sélectionner l'échantillon en utilisant le deuxième script qui est accessible ici :](https://drive.google.com/file/d/1NbfEUBzwsAToxAkFFho2ltowb3Par8iE/view?usp=sharing)


Encore une fois, il y a quelques arguments dans le code que nous devons spécifier. Tout d'abord, vous devez créer un fichier CSV avec deux colonnes, une colonne appelée "map_value" avec la valeur de chaque strate et une autre colonne appelée "final" avec le nombre d'échantillons dans chaque strate. Vous devez placer ce fichier dans le répertoire de travail. Ensuite, sur  
Ligne 12 : définissez le répertoire de travail
Ligne 19 : pointez sur le fichier contenant la stratification 
Ligne 22 : spécifier la résolution
Ligne 26 : pointer vers le fichier CSV contenant la taille de l'échantillon
Ligne 29 : spécifier le nom du CSV de sortie à utiliser dans Collect Earth
Ligne 35 : spécifier le nom du fichier shapefile de sortie contenant l'échantillon.



## 4 Foire aux questions (FAQs)

**Dois-je utiliser les applications mentionnées dans ce tutoriel pour sélectionner un échantillon?**

Non, pas du tout ! Ce ne sont que quelques exemples et il existe de nombreuses autres façons d'échantillonner une zone d'étude. Les applications courantes comprennent R, ENVI et ArcGIS.

**Dois-je sélectionner des pixels ? Et si je veux sélectionner des segments ou des blocs de pixels?**

L'unité spatiale de l'échantillon ne doit pas nécessairement être un pixel, mais doit être de taille égale pour satisfaire aux critères de l'échantillonnage probabiliste. Les pixels sont utilisés comme unités dans ces tutoriels pour des raisons de simplicité. Pour une discussion approfondie des unités spatiales, voir Stehman et Wickham (2011).

# Terminologie relative aux techniques d'échantillonnage

Une liste de termes relatifs aux techniques d'échantillonnage et d'inférence est fournie dans la documentation d'AREA2 : https://area2.readthedocs.io/en/latest/definitions.html Vous trouverez ci-dessous quelques termes supplémentaires qui ne figurent pas dans la documentation d'AREA2.  

#### Plan de réponse

Défini par (Stehman and Czaplewski, 1998)[^fn1]:  “La référence ou classe réelle est obtenue pour chaque unité d'échantillonnage sur la base de l'interprétation de photographies aériennes ou de vidéographies, d'une observation au sol ou d'une combinaison de ces sources. Les méthodes utilisées pour déterminer cette référence de classification sont appelées "plan de réponse". Le plan d'intervention comprend les procédures de collecte des informations relatives à la détermination de la occupation du sol de référence, et les règles d'attribution d'une ou plusieurs [labels] de référence à chaque unité d'échantillonnage.” Connu sous le nom de “plan de mesure” par Särndal et al. (1992)[^fn2].

#### Echantillon

Un sous-ensemble de la population sélectionné parmi les unités de la population.

#### Plan d'échantillonnage

Synonyme de plan d'échantillonnage (Sampling Design), qui est le terme préféré dans la littérature de référence (Cochran, 1977[^fn3], Särndal et al., 1992[^fn2]).  Le terme apparaît chez  Rice (1995)[^fn4] ui utilise à la fois “sampling design, **_plan d'echantillonnage_**” et “sample design, **_plan d'echantillon_**”. 

#### Plan d'échantillonnage

“Le concept de plan d'échantillonnage (sampling design ) est le protocole par lequel les unités de référence de l'échantillon sont sélectionnées” (Stehman and Czaplewski, 1998)[^fn1]. Le terme “Sampling design” est également utilisé par Cochran (1977)[^fn3] and Särndal et al. (1992)[^fn2] -- Le premier utilise également “sampling plan”. 

#### Sondage/Enquêtee

Särndal et al. (1992)[^fn2] définissent une enquête comme une “investigation partielle d'une population finie”, et précisent que  “les concepts d ‘enquête’ et ‘enquête par sondage’ sont utilisés pour désigner des enquêtes statistiques présentant les caractéristiques méthodologiques suivantes: [...]  échantillonnage aléatoire [...] plan de mesure [et] estimation”. de facon plus precise une enquete par sondage ou un sondage est une  enquête effectuee  sur une partie de la population. Cette fraction de la population constitue l'échantillon et les méthodes qui permettent de construire cet echantillon s'appellent méthode d'échantillonnage.


#### Plan d'enquête

UN “plan de sondage total” définit les procédures pour “obtenir la plus grande précision possible dans les estimations de l'enquête tout en trouvant un équilibre entre les erreurs d'échantillonnage et les erreurs non dues à l'échantillonnage [...] Le plan de sondage donne lieu à des opérations d'enquête” sélection de l'échantillon  (Särndal et al., 1992)[^fn2]. Lohr (1999)[^fn5] décrit un plan de sondage total comme “Une philosophie de conception d'enquête visant à minimiser les erreurs de non-échantillonnage ainsi que les erreurs d'échantillonnage..” De plus, dans Lohr (1999) “plan  d'enquête” est synonyme de plan d'échantillonnage.   

## License

Ce travail est autorisé sous une licence   [Creative Commons Attribution 3.0 IGO](https://creativecommons.org/licenses/by/3.0/igo/) 

Copyright 2020, Banque Mondiale. Ce travail a été développé par Pontus Olofsson dans le cadre d'un contrat de la Banque mondiale avec GRH Consulting, LLC pour le développement de nouvelles ressources - et la collecte de ressources existantes - liées à la mesure, la communication et la vérification pour soutenir la mise en œuvre du MRV dans les pays. 

Matériel révisé par :
Ana Mirian Villalobos, El Salvador, Ministry of Environment and Natural Resources
Carole Andrianirina, Madagascar, National Coordination Bureau REDD+ (BNCCREDD)
Foster Mensah, Ghana, Center for Remote Sensing and Geographic Information Services (CERGIS)
Jennifer Juliana Escamilla Valdez, El Salvador, Ministry of Environment and Natural Resources Phoebe Oduor, Kenya, Regional Centre For Mapping Of Resources For Development (RCMRD)
Rajesh Bahadur Thapa, Nepal, International Centre for Integrated Mountain Development (ICIMOD)
Tatiana Nana, Cameroon, REDD+ Technical Secretariat

Attribution: Olofsson, P. (2021). *Open MRV: Sample Selection*. World Bank. License: Creative Commons Attribution license (CC BY 3.0 IGO)

## References
[^fn1]: Särndal, C. E., Svensson, B. H., & Wretman, J. H. (1992). *Model assisted survey sampling*. New York, NY: Springer

[^fn1]: Stehman, S. V., & Czaplewski, R. L. (1998). Design and analysis for thematic map accuracy assessment: fundamental principles. *Remote Sensing of Environment*, 64(3), 331-344.

[^fn2]: Särndal, C. E., Svensson, B. H., & Wretman, J. H. (1992). *Model assisted survey sampling.* New York, NY: Springer.

[^fn3]: Cochran, W. G. (1977). *Sampling Techniques*. New York, NY: Wiley.

[^fn4]: Rice, J. A. (1995). *Mathematical Statistics and Data Analysis* (2nd ed.). Belmont, CA: Duxbury Press.

[^fn5]: Lohr, S. L. (1999). *Sampling: Design And Analysis.* CRC Press.