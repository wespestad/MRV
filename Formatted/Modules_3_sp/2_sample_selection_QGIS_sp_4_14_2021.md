---
​---
title: Sample selection using QGIS
summary: In sampling design methods for estimation of area and map accuracy, we design a sample by choosing a selection protocol and determining the sample size and allocation. In this tutorial we will physically draw from a study area a sample that was designed based on tutorials here on OpenMRV under process "Sampling design". Here, we illustrate how to draw a sample in QGIS.
author: Pontus Olofsson
creation date: February, 2021
language: English
publisher and license: Copyright 2021, World Bank. This work is licensed under a Creative Commons Attribution 3.0 IGO

tags:
- OpenMRV
- Landsat
- Sentinel 2
- QGIS
- Cloud cover
- Optical sensors
- Remote sensing
- Composite
- Mosaic
- Time series
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
​---
---

# Sample selection using QGIS

## 1. Contexto

En el tutorial anterior, diseñamos una muestra eligiendo un protocolo de selección y determinando el tamaño y la asignación de la muestra. En este tutorial sacaremos físicamente de un área de estudio la muestra que diseñamos. La extracción de una muestra implica la creación de un *marco de muestreo* que es una lista de unidades de población que se pueden seleccionar para su inclusión en una muestra. Las unidades de población de la lista se denominan unidades de muestreo. En otras palabras, un marco es un dispositivo que proporciona acceso de observación a la población al asociar las unidades de población con las unidades de muestreo (Särndal et al., 1992, p. 9) [^ fn1]. En nuestro caso, el marco de muestreo es, por ejemplo, una lista de todos los píxeles que componen el área de estudio. Por lo tanto, podríamos simplemente exportar una lista de todos los píxeles del mapa con identificadores únicos de los que seleccionamos aleatoriamente *n* unidades. En un muestreo aleatorio estratificado, cada píxel, además del identificador, también tendría un código de estrato de modo que se seleccione una muestra aleatoria de cada estrato. Este enfoque puede resultar fácilmente impráctico ya que el número de unidades de población tiende a ser grande. En cambio, la selección de muestras es compatible con varias herramientas y software; aquí, ilustramos cómo dibujar una muestra en Google Earth Engine / AREA2.

## 2 Objetivos de Aprendizaje

- Upon completion of the tutorial, the user should be able to sample an arbitrary study area under either systematic sampling (SYS), or simple random sampling (SRS) using QGIS.
  - Draw a sample in QGIS under SYS or SRS

### 2.1 Prerrequisitos para este módulo

- Relevant terminology for sampling techniques can be found at the end of this document

## 3 Tutorial: Sample selection using QGIS

QGIS proporciona soporte para el muestreo de poblaciones definidas por datos vectoriales. Por lo tanto, si desea muestrear en estratos definidos por un ráster, primero deberá vectorizar los datos ráster. Esto se hace usando la herramienta Raster> Conversions> "Polygonize (Raster to Vector)". La vectorización de rásteres grandes llevará mucho tiempo y no se recomienda; en su lugar, use las alternativas a continuación. Para áreas de estudio más pequeñas o para diseños SYS y SRS, QGIS funciona bien; repasemos los pasos necesarios para extraer dos muestras bajo SRS y SYS del país de Colombia.

### 3.1 Muestreo aleatorio simple

1. Primero necesitamos un shapefile que delinea nuestra área de estudio. Baje el shapefile de la frontera de Colombia aquí: https://drive.google.com/file/d/1tXvczTra_5wrlXBhe00m_oKRpLK0GwwJ/view?usp=sharing
2. Visualice el archivo en QGIS: Layer > Add Layer > "Add Vector Layer" y seleccione colombiaborder.shp para dibujar el shapefile en el lienzo.
3. Vector > Research Tools > "Random Points Inside Polygons"
4. Especifique que la frontera de Colombia es la capa de insumo, seleccione "Points count as sampling strategy and the total sample size under Point count"; deje la distancia mínima automática, y seleccione "Save to a file" y hacer clic en Run para dibujar la muestra.

[image: SRS_QGIS.png]

### 3.2 Muestreo sistemático

Dibujar una muestra bajo SYS en QGIS tiene el inconveniente de que la población tiene que ser rectangular, lo que dificulta dibujar un número exacto de unidades para un área no rectangular. Simplemente podemos recortar las unidades de muestra para la frontera con Colombia, pero eso dará como resultado un tamaño de muestra más pequeño que el especificado. Una solución alternativa es establecer una distancia entre ellos según el tamaño del área de estudio. Por ejemplo, si el área de estudio es *x* km^2^, establecer un espacio entre unidades ax/100 daría como resultado una muestra de 100 unidades.

1. Después de agregar el shapefile en la sección 2.1.2 arriba, vaya a Vector > Research Tools > "Regular Points"
2. Seleccione la frontera de Colombia como la extensión de insumo
3. Especifique el espacio de los puntos (Point spacing) o la cantidad de puntos (Point count) -- si usa el espacio, active la cajilla "Use point spacing"
4. Guarde esto a un archivo y haga clic en Run para visualizar la muestra.

[image: SYS_QGIS.png]

## 4 Preguntas Frecuentes

**¿Debo usar las aplicaciones mencionadas en este tutorial para seleccionar una muestra?**

¡No, en absoluto! Estos son solo algunos ejemplos y hay muchas otras formas de muestrear un área de estudio. Las aplicaciones comunes incluyen R, ENVI y ArcGIS.

**¿Tengo que seleccionar píxeles? ¿Qué pasa si quiero seleccionar segmentos o bloques de píxeles?**

La unidad espacial de la muestra no tiene que ser un píxel, pero debe tener el mismo tamaño para satisfacer los criterios del muestreo probabilístico. Los píxeles se utilizan como unidades en estos tutoriales en aras de la simplicidad. Para un análisis en profundidad de las unidades espaciales, consulte Stehman y Wickham (2011).

## 5 Terminología relevante para las técnicas de muestreo

Una lista de términos relevantes para las técnicas de muestreo e inferencia esta provista en la documentación de AREA2: https://area2.readthedocs.io/en/latest/definitions.html. Abajo hay algunos términos adicionales que no están incluidos en la documentación.

### 5.1 Diseño de Respuesta

Definido por Stehman and Czaplewski, 1998[^fn1]: “La referencia o clasificación 'verdadera' se obtiene para cada unidad de muestreo en función de la interpretación de fotografías aéreas o videografías, una visita terrestre o una combinación de estas fuentes. Los métodos utilizados para determinar esta clasificación de referencia se denominan "diseño de respuesta". El diseño de respuesta incluye procedimientos para recopilar información relacionada con la determinación de la cobertura terrestre de referencia y reglas para asignar una o más [etiquetas] de referencia a cada unidad de muestreo ". Conocido como "plan de medición" por Särndal et al. (1992)[^fn2].

### 5.2 Muestra

Un subconjunto de unidades de población seleccionadas de la población.

### 5.3 Diseño de Muestra

Sinónimo de diseño de muestreo, que es el término preferido en la literatura fundamental (Cochran, 1977 [^ fn3], Särndal et al., 1992 [^ fn2]). El término aparece en Rice (1995) [^ fn4] que utiliza tanto "diseño de muestreo" como "diseño de muestra".

### 5.4 Diseño de Muestreo

"El diseño de muestreo es el protocolo mediante el cual se seleccionan las unidades de muestra de referencia". (Stehman y Czaplewski, 1998) [^ fn1]. El “diseño de muestreo” también es utilizado por Cochran (1977) [^ fn3] y Särndal et al. (1992) [^ fn2]- el primero también usa "plan de muestreo".

### 5.5 Encuesta

Särndal y col. (1992) [^ fn2] define una encuesta como una “investigación parcial de una población finita”, y además que “los términos 'encuesta' y 'encuesta por muestreo' se utilizan para denotar investigaciones estadísticas con las siguientes características metodológicas: [. ..] plan de medición [...] de muestreo probabilístico [y] estimación."

### 5.6 Diseño de Encuesta

Un "diseño total de la encuesta" define los procedimientos para "obtener la posible precisión en las estimaciones de la encuesta mientras se logra un equilibrio entre los errores de muestreo y los no muestrales [...] El diseño de la encuesta da lugar a operaciones de encuesta" como la selección de la muestra (Särndal et al., 1992) [^ fn2]. Lohr (1999) [^ fn5] describe un diseño de encuesta total como "Una filosofía de diseño de encuesta para minimizar los errores de muestreo y de no muestreo". Además, en Lohr (1999) “diseño de encuestas” es sinónimo de diseño de muestreo.

## Referencias

Cochran, W.G., 1977. Sampling Techniques, John Wiley & Sons, New York, NY.

Lohr, S.L., 1999. Sampling: Design And Analysis, CRC Press.

Rice, J.A., 1995. Mathematical Statistics and Data Analysis (2nd ed.), Duxbury Press, Belmont, CA.

Särndal, C.E., Svensson, B.H., & Wretman, J.H., 1992. Model assisted survey sampling, Springer Science & Business Media, New York, NY.

Stehman, S.V., & Czaplewski, R.L., 1998. Design and analysis for thematic map accuracy assessment: fundamental principles. Remote Sensing of Environment, 64(3), 331-344. https://doi.org/10.1016/S0034-4257(98)00010-8

Stehman, S.V. and Wickham, J.D., 2011. Pixels, blocks of pixels, and polygons: Choosing a spatial unit for thematic accuracy assessment. Remote Sensing of Environment, 115(12), pp.3044-3055. https://doi.org/10.1016/j.rse.2011.06.007



-----

![](figures/cc.png)  

Este trabajo tiene licencia bajo un [Creative Commons Attribution 3.0 IGO](https://creativecommons.org/licenses/by/3.0/igo/)

Copyright 2020, World Bank.

Este trabajo fue desarrollado por Pontus Olofsson bajo contrato del World Bank con GRH Consulting, LLC para el desarrollo de recursos nuevos o existentes relacionadas a la Medida, Reportaje, y Verificación para el apoyo de implementación MRV en varios países.

Material revisado por: Ana Mirian Villalobos, El Salvador, Ministry of Environment and Natural Resources Carole Andrianirina, Madagascar, National Coordination Bureau REDD+ (BNCCREDD) Foster Mensah, Ghana, Center for Remote Sensing and Geographic Information Services (CERGIS) Jennifer Juliana Escamilla Valdez, El Salvador, Ministry of Environment and Natural Resources Paula Andrea Paz, Colombia, International Center for Tropical Agriculture (CIAT) Phoebe Oduor, Kenya, Regional Centre For Mapping Of Resources For Development (RCMRD) Rajesh Bahadur Thapa, Nepal, International Centre for Integrated Mountain Development (ICIMOD) Tatiana Nana, Cameroon, REDD+ Technical Secretariat

Atribución: Olofsson, P. 2021. Sample selection using QGIS. © World Bank. License: [Creative Commons Attribution license (CC BY 3.0 IGO)](http://creativecommons.org/licenses/by/3.0/igo/)

![](figures/wb_fcfc_gfoi.png)