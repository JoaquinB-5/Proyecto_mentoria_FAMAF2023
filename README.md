# Proyecto_mentoria_FAMAF2023
Integrantes:
* Ing. Joaquín Barrionuevo
* Lic. Sabrina Gonzalez del Campo
* Lic. Sebastián Coca

# ***ANÁLISIS Y GESTIÓN DE RECURSOS AEROPORTUARIOS: Aeroparque Jorge Newbery***

## OBJETIVO >>> Explicar los retrasos en vuelos a través de la ciencia de datos <<<

## Descripción
***Decidimos elegir este proyecto porque presenta diferentes desafíos como el cruzamiento con otras bases de datos (clima, aeropuertos, etc.) y la posibilidad de aplicar la ciencia de datos al área de logística, afrontando un problema real y que podría ser de utilidad en la práctica. Por otra parte, nos interesa también conocer más de cerca el aeropuerto Jorge Newbery, uno de los que más flujo de pasajeros presenta en toda la Argentina, y poder presentar propuestas de mejora acerca de la saturación del aeropuerto basándonos en datos. Entender la capacidad del aeropuerto y la gestión de sus recursos será clave para afrontar el proyecto. El período comprendido en nuestra base de datos es desde enero 2019 hasta septiembre 2022 y contiene información a cerca de los arribos al aeropuerto, con datos de fecha, procedencia, aerolínea. Es relevante que contamos con un año completo en la situación pre-pandemia para entender el flujo normal sin restricciones aeroportuarias. El problema se afrontará utilizando Python y una serie de librerías comunes en la Ciencia de Datos, tales como numpy, pandas, sklearn, matplotlib, seaborn, missingo, etc. El objetivo de este proyecto es entender el volumen de arribos: si hay alguna tendencia de horarios, día, mes o época del año donde se presenten picos, el porcentaje de vuelos con retrasos y entender si provienen mayoritariamente de una aerolínea o aeropuerto en particular (o si tienen correlación con alguna otra variable), y finalmente aplicar machine learning a la base de datos limpia para poder predecir algún pico y proponer de ser posible alguna acción que logre evitar la saturación del aeropuerto.***

## Problema Comercial

Se procederá a formatear los datos existentes y proporcionar visualizaciones que respondan las siguientes preguntas:

>Cantidad de arribos por mes

>Cantidad de Pasajeros por mes

>Distribución de arribos por día y frecuencia

>Distribucion de vuelos provenientes de distintos lugares (eg. Brasil)

>¿Es posible predecir demoras por ruta?

>Durante un año, ¿qué cabecera es la que más se utilizó? ¿En qué posición?

>¿Hay zonas geográficas que tienden a tener más demoras que otras?

>¿Cuáles son los horarios picos de pasajeros en la terminal?

>Posibles causas de las demoras

>Se relacionan las demoras al mal clima?

## Base de datos
Para efectuar el análisis se proporciona un archivo CSV que contiene registros de +120000 datos de vuelos entre los años 2019 y septiembre del 2022 inclusive. Este dataset cuenta con informacion de cantidad de pasajeros, horas de arribo y de programación, aerolinea, aeronave, origen, terminal, entre otros. El problema a resolver es poder predecir las demoras en los distintos vuelos para así poder prever de la mejor manera los recursos aeroportuarios para evitar la saturación de los mismos.

Nombre Columna | Descripción | 
|---|---|
| Aero | Aerolínea que opera el vuelo | 
| Vuelo | Codigo de Vuelo | 
| Cshare | Código compartido entre empresas| 
| Origen | Ruta del vuelo | 
| Via | Escala del vuelo | 
| STA | Horario programado de arribo | 
| SUG | Horario sugerido | 
| ETA | Estimated Time Arrival| 
| ATA | Actual Time Arrival | 
| Tipo | Codificación del tipo de vuelo | 
| Pos | Posición asignada al arribo| 
| Ter | Terminal en que opera el arribo | 
| Sec | Sector asociado a la terminal | 
| Rmk | Remark (Estado del vuelo) | 
| Cin | Cinta asignada para retirar equipajes| 
| L&F | Mostrador de reclamos de equipajes asignado al vuelo | 
| Pax | Cantidad de pasajeros | 
| Vip | si tiene o no pasajeros vip ese vuelo | 
| Mat | MAtricula de la aeronave| 
| Acft | Tipo de aeronave | 
| Obs. | Observaciones | 
| Aero.1 | Empresa aerea asociada a la partida | 
| #Rot | Vuelo asociado a la partida| 
| Cabecera | Cabecera de pista donde operó el arribo | 
| año | Año de operación del vuelo | 
| mes | Mes de operación del vuelo | 
| Hora | Hora de operación del vuelo | 

## Limpieza y curación

Se realizo un investigación a partir de las matriculas de las aeronaves para filtrar aquellas instancias que no eran parte de vuelos comerciales regulares, como las aeronaves del estado, militares, helicopteros o aeronaves pequeñas privadas.
Se detectaron columnas con muy pocos datos, otras con datos faltantes a las cuales se realizaron imputaciones, correcciones, valores númericos negativos o nulos y otros casos particulares que se analizaron y solucionaron puntualmente.

## Análisis exploratorio

La exploración sobre la base de datos se realizó pensando en las preguntas que debiamos responder para abordar el problema comercial y se obtuvieron algunas conclusiones, pero se detectó que la correlación entre las caracteristicas y la variable objetivo era muy baja. Por lo tanto en este punto se incoporaron otras variables como el clima, datos de la aeronave, también se realizó un poco de ingeniería de varibles buscando que podamos explicar mejor las demoras en los vuelos. 
A partir de esto se seleccionaron los factores mas determinantes para utilizar en el proximo paso del proyecto.

## Modelación 

Con el objetivo de que a la hora de aplicar los modelos de aprendizaje automático, las variables de entrada tengan propiedades deseables y permitan obtener mejores rendimientos y eficiencias en los modelos,
se realizaron transfomaciones tales como la Normalización y Estandarización sobre las variables númericas, y el Encoding para las categoricas.

Se aplicó una estrategía de clasificación - predicción como se muestra en la figura siguiente:

<div align="center">

<p align="center">
  <img src= "https://github.com/JoaquinB-5/Proyecto_mentoria_FAMAF2023/assets/103613228/c513e3cc-8ce7-4329-b261-fd7b5eefc01e" width="500" height="300">
</p>
</div>

donde primero realizamos una clasificación binaria, es decir vuelo retrasado o no, y a partir de los obtenidos como positivos se realizó una predicción para intentar determinar un valor de retraso en minutos.

Se utilizaron modelos de aprendizaje automatico supervizado, donde primero elegimos el modelo de regresión logística como base y a partir de allí se fueron evaluando modelos más específicos.
Como métricas para determinar el rendimiento usamos el f1-score, recall que fueron las mas aproiadas para nuestros datos
Además también tuvimos que aplicar técnicas de submuestreo y sobremuestreo para intentar resolver el problema de desbalance de clases.

## Conclusiones

En base a los desarrollado anteriormente, es necesario reconocer las limitaciones del proyecto y realizar una comunicación de las 
conclusiones de forma transparente, en resumen pudimos observar.

* Calidad de los datos: a pesar de haber realizado una exaustiva investigación de estos, limpieza profunda, ingeniería de datos, pruebas con distintos modelos e
hiperparámetros no se obtuvieron mejoras significativas en los modelos de clasificación;

* datos desbalanceados: otro de los problemas fue el gran desequilibrio de clases a la hora de querer aplicar los algoritmos de clasificación, se probaron distintas técnicas
para abordar este problema, y se obtuvieron limitadas mejoras;

* generalización deficiente: también logramos observar en varios modelos que estos presentaban sobreajuste en los datos de entrenamientos y 
que arrojaban metricas pobres a la hora de testearlos; y

* tendecias preliminares: en análisis previos se observaba que las caracteristicas no tenian una buena correlacion con nuestra variable
objetivo, en esta última etapa pudimos confirmar esta tendecia.

Trabajos futuros: entonces en funcion a estas conclusiones se recomiendan acciones para una posible segunda etapa del proyecto

* ampliación de la base de datos: creemos que es necesario incluir otras caracteristicas que expliquen de mejor manera los retrasos
como por ejemplo datos relacionados al origen, como el despegue. Como asi mismo, ampliar la cantidad de datos y en lo posible eliminar el intervalo de pandemia;

* ingenería de variables: profundizar en tecnicas de ingeniería de variables para de esta a forma utilizar las caracateristicas que ya se tienen
de una forma mas conveniente; y

* Probar otras técnicas de IA.
