---
title: Terminology relevant to the sampling techniques
summary: This tutorial will introduce the terminology relevant to the sampling techniques for estimation of area and map accuracy. More information on terminology can be found in the AREA2 documentation - https://area2.readthedocs.io/en/latest/definitions.html
author: Pontus Olofsson
creation date: February, 2021
language: English
publisher and license: Copyright 2021, World Bank. This work is licensed under a Creative Commons Attribution 3.0 IGO

tags:
- OpenMRV
- Landsat
- Sentinel 2
- Sentinel 1
- GEE
- Cloud cover
- Optical sensors
- Remote sensing
- Composite
- Mosaic
- Time series
- Change detection
- Land cover mapping
- Forest mapping
- Deforestation mapping
- Degradation mapping
- Forest degradation mapping
- Sampling design
- Sample design
- Sample selection
- Sample
- Sampling frame
- Stratified
- Simple Random
- Systematic
- Response design
- Survey
- Survey design
- Accuracy
- Accuracy assessment
- Area Estimation
- Reference data
- Reference classification
- Reference observations
- Colombia
- Mozambique
- Cambodia

group:
- category: Stratified
  stage: Sampling
- category: Simple Random
  stage: Sampling
- category: Cluster
  stage: Sampling
- category: Systematic
  stage: Sampling
- category: Stratified
  stage: Area Estimation/Accuracy assessment
- category: Expansion
  stage: Area Estimation/Accuracy assessment
- category: Model-assisted
  stage: Area Estimation/Accuracy assessment
- category: Ratio
  stage: Area Estimation/Accuracy assessment
---

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
Ce travail est sous licence  [Creative Commons Attribution 3.0 IGO](https://creativecommons.org/licenses/by/3.0/igo/) 

Copyright 2020, Banque mondiale. Ce travail a été développé par Pontus Olofsson dans le cadre d'un contrat de la Banque mondiale avec GRH Consulting, LLC pour le développement de nouvelles ressources - et la collecte de ressources existantes - liées à la mesure, la notification et la vérification pour soutenir la mise en œuvre du MRV dans les pays. 

Attribution: Olofsson, P. (2021). *Open MRV: Terminology relevant to the sampling techniques*. World Bank. License: Creative Commons Attribution license (CC BY 3.0 IGO)

## References
[^fn1]: Stehman, S. V., & Czaplewski, R. L. (1998). Design and analysis for thematic map accuracy assessment: fundamental principles. *Remote Sensing of Environment*, 64(3), 331-344.

[^fn2]: Särndal, C. E., Svensson, B. H., & Wretman, J. H. (1992). *Model assisted survey sampling.* New York, NY: Springer.

[^fn3]: Cochran, W. G. (1977). *Sampling Techniques*. New York, NY: Wiley.

[^fn4]: Rice, J. A. (1995). *Mathematical Statistics and Data Analysis* (2nd ed.). Belmont, CA: Duxbury Press.

[^fn5]: Lohr, S. L. (1999). *Sampling: Design And Analysis.* CRC Press.




