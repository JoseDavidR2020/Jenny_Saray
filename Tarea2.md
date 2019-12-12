# Tarea 02


## ÁREAS DE PRODUCCIÓN DE HIDROCARBUROS EN EL DEPARTAMENTO DE CESAR

Mapa web con la actividad de los bloques de hidrocarburos que desarrollan actividad de producción en el departamento de Cesar


##  Cuál es el problema a tratar?

Conocer la distribución pozos y contratos que se dedican a la explotación hidrocarburos, clasificándolos por medio de las cuencas sedimentarias 


##  Por qué la publicación de servicios OGC puede ayudar a resolverlo?

Porque por medio de capas base se puede generar una o varias capas nuevas que permitan visualizar y analizar la temática 


##  Qué servicios propone para la solución de su problema? WMS? WMTS? WFS? Por qué?
WFS, porque la información está dada en shapefile y es por medio de la cual se pueden obtener las capas que permiten ser editadas. Para este ejercicio era necesario extraer información limitando el área y alimentado de varias capas


## Descripción de los datos seleccionados

### Mapa de tierras
*Origen:* Agencia Nacional de Hidrocarburos – ANH

*Descripción:* Es la representación gráfica en la cual se muestran el estado de los bloques delimitados para la exploración y la explotación de este recurso no renovable

*Características especiales:* Es un mapa que abarca todo el territorio colombiano tanto continental como la del mar territorial

*Atributos:* Estado de los bloques, clasificación, tipo de contrato, operador, yacimiento

*Url para descarga:* http://www.anh.gov.co/hidrocarburos/oportunidades-disponibles/mapa-de-tierras 

### Cuencas Sedimentarias
*Origen:* Agencia Nacional de Hidrocarburos – ANH

*Descripción:* Es la representación del territorio colombiano en el cual cuyos polígonos son la clasificación que se le atribuyen a características del suelo y del subsuelo nacional

*Características especiales:* Es un mapa que abarca todo el territorio colombiano tanto continental como la del mar territorial, por lo cual tiene todo el país clasificado por las características que brinda el suelo y el subsuelo.

*Atributos:* nombre cuenca, área, clasificación

*Url para descarga:* http://www.anh.gov.co/Informacion-Geologica-y-Geofisica/Cuencas-sedimentarias


### Pozos
*Origen:* Servicio Geológico Colombiano

*Descripción:* Es la recopilación de toda la información georreferenciada de la localización de los pozos, suministrados por las operadoras que perforan el territorio colombiano

*Características especiales:* cuenta con los pozos aprobados según formas 4CR y 6CR 

*Atributos:* Identificador único del pozo, nombre del pozo, coordenada x, coordenada y, fecha de descubrimiento

*Url para descarga:* http://srvags.sgc.gov.co/JSViewer/GEOVISOR_BIP/




##  Descripción del procesamiento realizado con POSTGIS
El procesamiento de las capas base tiene como fin obtener una capa con las áreas de producción que se están desarrollando en el departamento del Cesar y adicionar información de las cuencas sedimentarias en las que se encuentras estos bloques

### Instalación de Software
1. Se descargó el programa QGis 
2. Se descargó el programa pgAdmin

### Cargue de capas por medio de QGis

1. Se crea una conexión a postgis
2. Se importan las 4 capas base al servicio creado:

![img1](Imagenes_T2/cap05.PNG)

### Procesamiento de las capas base en pgAdmin

3. Se crea una conexión a postgis y se abre el editor sql:

![img1](Imagenes_T2/cap06.PNG)

4. Dado que el área de interés es el departamento de Cesar, el primer proceso consiste en extraer este departamento:

*Código*

![img1](Imagenes_T2/cap07.PNG)


*Resultado*

![img1](Imagenes_T2/cap08.PNG)


5. Se realiza el cálculo del área a las capas del departamento de Cesar y mapa de tierras:

*Código*

![img1](Imagenes_T2/cap09.PNG)


*Resultado*

![img1](Imagenes_T2/cap10.PNG)


6. Se crear capa de las áreas en producción del departamento de Cesar a partir de intersectar las capas "u8_depto_cesar" y "u8_mtierras" y teniendo como filtro en el mapa de tierras únicamente las áreas cuyo estado sea producción:

*Código*

![img1](Imagenes_T2/cap11.PNG)


*Resultado*

![img1](Imagenes_T2/cap12.PNG)


7. Se crea una columna en donde se almacenará la información de la cuenca sedimentaria sobre la cual se encuentra el bloque: 

*Código*

![img1](Imagenes_T2/cap13.PNG)

*Resultado*

![img1](Imagenes_T2/cap14.PNG)



##  Procedimiento de cargue de capa en Geoserver

8. El proceso consiste en adicionar las capas que se desean genearr en el mapa. Para esto, sobre la pestaña “Capas” se selecciona “Agregar nuevo recurso”
![img1](Imagenes_T2/cap15.PNG)


9. En la ventana emergente se adiciona una a una las capas deseadas seleccionando la pestaña Publicación
![img1](Imagenes_T2/cap16.PNG)


9. Se ingresan los parámetros solicitados de la siguiente manera:
![img1](Imagenes_T2/cap17.PNG)


10. Finalmente se pueden observar las Capas en la pestaña “Previsualización de capas” :
![img1](Imagenes_T2/cap18.PNG)


10. Se realiza una agrupación de las capas anteriormente adicionadas por medio de la opción “Grupos de Capas – Agregar nuevo grupo de capas” :
![img1](Imagenes_T2/cap19.PNG)



11. En la ventana emergente se ingresan los datos solicitados y en la parte inferior se adicionan una a una las capas del grupo:
![img1](Imagenes_T2/cap20.PNG)
![img1](Imagenes_T2/cap21.PNG)



##  Descripción de la forma en que creó la simbología
#### Generación de Estilos SLD
12. En la herramienta Qgis se genera la simbología deseada y se guarda como archivo SLD:
![img1](Imagenes_T2/cap22.PNG)

13. En GeoServer se genera el estilo seleccionando la pestaña “Estilos” y luego “Nuevo Estilo” y se ingresan el nombre y parámetros deseados:
![img1](Imagenes_T2/cap23.PNG)

En la parte inferior se adiciona el archivo SLD creado en Qgis:
![img1](Imagenes_T2/cap24.PNG)


Este procedimiento se realiza para las capas:
-	u8_cuencas_sed
-	u8_mtierras
-	u8_depto_cesar
13. Ahora es posible asignar los estilos creados a las capas previamente adicionadas, esto se realiza ingresando a cada estilo en la pestaña “Publishing” y seleccionando la capa a asignar:

![img1](Imagenes_T2/cap25.PNG)

*PREVISUALIZACION DE LA CAPA CUENCAS SEDIMENTARIAS*

![img1](Imagenes_T2/cap26.PNG)


*PREVISUALIZACION DE LA CAPA DEPARATAMENTO CESAR*

![img1](Imagenes_T2/cap27.PNG)


*PREVISUALIZACION DE LA CAPA MAPA DE TIERRAS*

![img1](Imagenes_T2/cap28.PNG)



#### Generación de Estilos CSS
14. Se genera el estilo seleccionando la pestaña “Estilos” y luego “Nuevo Estilo” y se ingresan el nombre y parámetros deseados, esta vez se selecciona CSS en Formato:
![img1](Imagenes_T2/cap29.PNG)

Este proceso se realiza para las capas pozos y producción cesar

![img1](Imagenes_T2/cap30.PNG)
![img1](Imagenes_T2/cap31.PNG)


15. La visualización se realiza en el grupo de capas creado:
![img1](Imagenes_T2/cap32.PNG)


## Nombres de las tablas creadas en postgis
-	u8_depto_cesar
-	u8_produccion_cesar

## Nombres de las capas y estilos publicadas en geoserver
#### Capas
-	u8_cuencas_sed
-	u8_mtierras
-	u8_pozos_cesar
-	u8_depto_cesar
-	u8_produccion_cesar
#### Estilos
-	u8_style_cuencas_sed
-	u8_style_mt
-	u8_style_cesar
-	u8_style_pozo
-	u8_style_produccion_cesar


## Url de la previsualización del grupo de capas en Geoserver
http://34.83.176.208:18080/geoserver/clase/wms?service=WMS&version=1.1.0&request=GetMap&layers=clase%3AU8_Tarea_02&bbox=-224808.546875%2C22962.0%2C1806815.875%2C2287798.0&width=688&height=768&srs=EPSG%3A3116&format=application/openlayers#toggle

## Ventajas / desventajas / dificultades encontradas durante el proceso

-	No logre tener un mapa con el cual me sienta satisfecha, si bien es una herramienta útil y de acceso dinámico no me gusta la visualización de los colores, cambian bastante con respecto Qgis y no logre generar la transparencia a las capas.
-	La herramienta QGis es bastante lenta en los procesos gráficos y varios procesos se repitieron por las fallas que este genera


![img1](Imagenes_T2/cap33.PNG)
