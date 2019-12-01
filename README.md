# Tarea 01

## MAPA DE TIERRAS

Mapa web de bloques de Hidrocarburos en Colombia

##  Cuál es el problema a tratar?

Conocer que uso se le está dando al territorio colombiano en cuanto a la explotación de recursos no renovables dentro del sector hidrocarburífero 


##  Por qué un mapa ayuda a resolverlo?

Porque el mapa permite mostrar de manera gráfica la especialización de las áreas y el estado en que se encuentran los bloques de Hidrocarburos. Además, con la opción de los metadatos se puede conocer más información acerca de cada bloque 

## Fuente de datos

DEPARTAMENTOS
https://www.datos.gov.co/Mapas-Nacionales/Departamentos-y-municipios-de-Colombia/xdk5-pm3f

MAPA DE TIERRAS
http://www.anh.gov.co/hidrocarburos/oportunidades-disponibles/mapa-de-tierras


##  Herramientas

- QGIS
- QgisCloud

##  Proceso Realizado

- Se creó cuenta gratuita en QgisCloud https://qgiscloud.com/
- En QGIS se instaló del plugin de qgiscloud


![img1](images/00_qgiscloud.png)


- Se descargó la información en formato .shp
- Se configuró simbología a través de clasificación categórica por atributo único.

![img1](images/00_simbologia.png)

- Mapa resultante:

![img2](images/00_mapa.png)

- Se realizó la publicación del mapa en la web utilizando QgisCloud

![img3](images/00_publicado.png)


##  Urls

- Mapa Web https://qgiscloud.com/dersteppenwolf/qgis_mapa_rutas_2/?bl=&st=&l=rutas-habiles-zonales%20Rutas%20H%C3%A1biles%20Zonales&t=qgis_mapa_rutas_2&e=-74.38875%2C4.48498%2C-73.77022%2C4.79034

- WMS https://qgiscloud.com/dersteppenwolf/qgis_mapa_rutas_2/wms?SERVICE=WMS&REQUEST=GetCapabilities

