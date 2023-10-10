# PI_DA
PROYECTO INDIVIDUAL Nº2 

# Homicidios por siniestros viales en la Ciudad Autónoma de Buenos Aires, Argentina (CABA)

## Introducción

En este proyecto se simula el rol de un Data Analyst que forma parte del equipo de analistas de datos de una empresa consultora a la cual el **Observatorio de Movilidad y Seguridad Vial (OMSV)**, que es un centro de estudios que se encuentra bajo la órbita de la Secretaría de Transporte del Gobierno de la Ciudad Autónoma de Buenos Aires (CABA), les solicitó la elaboración de un proyecto de análisis de datos. 

El fin de este proyecto es generar información que le permita a las autoridades locales tomar medidas para disminuir la cantidad de víctimas fatales de los siniestros viales ocurridos en CABA. Para ello, se pone a disposición un dataset sobre homicidios en siniestros viales acaecidos en la Ciudad de Buenos Aires durante el periodo 2016-2021.

Se espera como productos finales un reporte de las tareas realizadas, metodologías adoptadas y principales conclusiones y la presentación de un dashboard interactivo que facilite la interpretación de la información y su análisis.

## Contexto

Los siniestros viales, también conocidos como accidentes de tráfico o accidentes de tránsito, son eventos que involucran vehículos en las vías públicas y que pueden tener diversas causas, como colisiones entre automóviles, motocicletas, bicicletas o peatones, atropellos, choques con objetos fijos o caídas de vehículos. Estos incidentes pueden tener consecuencias que van desde daños materiales hasta lesiones graves o fatales para los involucrados.

La Ciudad Autónoma de Buenos Aires, que se ubica en la provincia de Buenos Aires en Argentina, no es la excepción a esta problemática, sino que los siniestros viales son una preocupación importante debido al alto volumen de tráfico y la densidad poblacional. Estos incidentes pueden tener un impacto significativo en la seguridad de los residentes y visitantes de la ciudad, así como en la infraestructura vial y los servicios de emergencia.

Actualmente, según el censo poblacional realizado en el año 2022, la población de CABA es de 3,120,612 habitantes en una superficie de 200 $km^2$, lo que implica una densidad de aproximadamente 15,603 $hab/km^2$ ([Fuente](https://www.argentina.gob.ar/caba#:~:text=Poblaci%C3%B3n%3A%203.120.612%20habitantes%20(Censo%202022).)). Por lo que la prevención de siniestros viales y la implementación de políticas efectivas son esenciales para abordar este problema de manera adecuada.

## Datos

Para este proyecto se trabajó con la **Bases de Víctimas Fatales en Siniestros Viales** que se encuentra en formato de Excel y contiene dos pestañas de datos:

* **HECHOS**: que contiene una fila de hecho con id único y las variables temporales, espaciales y participantes asociadas al mismo.  

* **VICTIMAS**: contiene una fila por cada víctima de los hechos y las variables edad, sexo y modo de desplazamiento asociadas a cada víctima. Se vincula a los HECHOS mediante el id del hecho.

En este [documento](Data/NOTAS_HOMICIDIOS_SINIESTRO_VIAL.pdf) se detallan todas las definiciones manejadas en los datos y en el desarrollo de este proyecto. Por otra parte, en este [link](https://data.buenosaires.gob.ar/dataset/victimas-siniestros-viales) se encuentran los datos utilizados en el análisis.

## Tecnologías utilizadas

Para la elaboración de este proyecto se utilizó Python y Pandas para los procesos de extracción, transformación y carga de los datos, como así también para el análisis exploratorio de los datos. En el siguiente apartado se describen los resultados del análisis.

## ETL y EDA

Se realizó un proceso de extracción, transformación y carga de los datos (ETL) y un análisis exploratorio exahustivo (EDA), primero para los datos de "HECHOS" y luego para los de "VÍCTIMAS", donde se estandarizaron nombres de las variables, se analizaron nulos y duplicados de los registros, se eliminaron columnas redundantes o con muchos valores faltantes, entre otras tareas. Una vez finalizado este proceso para los dos conjuntos de datos de "Homicidios" se generaro dos dataframes 'df_hechos' y 'df_victimas', que fueron luego exportados en formato excel para analizar la información y realizar los dashboards y KPI´S en Power BI.

Todos los detalles de este análisis se encuentran [en este documento](Jupyter_Notebooks/EDA.ipynb).

El primer paso fue analizar la variable **N_VICTIMAS:**
- Donde la estadística descriptiva revela que, en promedio, cada incidente involucra alrededor de 1.03 víctimas. Esto indica que la mayoría de los eventos tienden a tener una sola víctima, aunque ocasionalmente puede haber más de una. La baja desviación estándar de aproximadamente 0.18 sugiere que la cantidad de víctimas tiende a variar muy poco alrededor de esta media.  

- El valor mínimo en la columna es 1, lo que indica que en todos los incidentes, al menos una persona se ha visto afectada. Los percentiles, que representan la distribución de los datos, también revelan que el 25% de los eventos involucra a una sola víctima, al igual que el 50% (mediana) y el 75%. Esto respalda la idea de que la mayoría de los incidentes tienen una sola víctima.  

- Sin embargo, el valor máximo en la columna es 3, lo que sugiere que en algunos casos excepcionales, se han registrado hasta tres víctimas en un solo incidente. Aunque estos casos son menos comunes, aportan una dimensión adicional a la variabilidad en la cantidad de víctimas.

Luego se analizó la variable **FECHA:**
- Donde se aprecia claramente que desde el 2018 donde se registraron 143 siniestros, los mismos han bajado considerablemente, registrando el número más bajo de 78 en 2020.  

- Luego de investigar, encuentro en internet el siguiente artículo https://webpicking.com/baja-la-cantidad-de-victimas-fatales-en-siniestros-viales-en-caba/ donde puede explicarse la baja que registrada desde 2018 tras la implementación del primer "Plan de Seguridad Vial de la Ciudad de Buenos Aires" que guió las políticas de movilidad segura durante el período 2016-2019, donde se propuso la meta de disminuir 30% las víctimas fatales causadas por incidentes viales para el año 2019.  

- Se observa también que el pico más bajo se registró en 2020, el cuál es explicado claramente por la coyuntura de pandemia que dsminuyó considerablemente el tráfico de vehículos.  

Siguiendo con la variable **HH (información de la hora de los incidentes pero en números enteros):**
- se observa, que  el mayor pico de registros, se da entre las 6 y 7 AM, que podría explicarse por el tráfico a la hora de movilizarse al trabajo y a llevar a los niños a los colegios. Los registros más bajos son en la madrugada (2 AM) que puede explicarse ya que la mayoría se encuentra descansando.  

Al analizar la variable **TIPO DE CALLE:**
- podemos observar que el 60% de los registros se dan en avenidas y como vimos anteriormente, en horarios diurnos que es cuando las personas circulan con mayor frecuencia por estas vías, puede explicarse por excesos de velocidad en estas vías, falta de controles en intersecciones peligrosas que veriricaremos cuando analicemos la información de "Intersecciones", alta circulación de todo tipo de vehículos incluyendo bicicletas y peatones. Por otra parte, la poca circulación de peatones y biciclestas puede explicar la baja tasa registraza en Gral Paz. Sobre esta vía, nos surgió una duda respecto a la razón por la cuál se encontraba discriminada como una categoría más y no dentro de "Avenidas", por lo que vía mail se consultó al gobierno. A continuación detallo la respuesta textual que recibimos:  
        "Buenas tardes, como estás Gastón?
 
        Enviamos tu consulta al AREA responsable del Dataset y te pasamos la respuesta correspondiente:
 
        En términos estrictos la Av. General Paz tiene características de autopista, es decir una vía segregada sin semáforos ni cruces a nivel. (Art 5to de la Ley nacional de transito 
        Autopista: una vía multicarril sin cruces a nivel con otra calle o ferrocarril, con calzadas separadas físicamente y con limitación de ingreso directo desde los predios frentistas lindantes)
 
        Sin embargo por cuestiones jurisdiccionales, si bien es parte del territorio de la ciudad en toda su extension, al no estar bajo la administración de la Ciudad como las autopistas de AUSA (la Av General Paz se encuentra administrada por Autopistas del Sol, concesionario que también administra la Panamericana), la tenemos clasificada aparte.
 
        Quienes usen la base pueden realizar la reclasificación que consideren pertinente para su análisis.
 
        Desde ya Muchas Gracias!
        Saludos".  

Por esta razón, decido mantener sin cambios esta categoría.  

Al analizar la variable **COMUNA:**
- detectamos que la Comuna 1 destaca con 90 incidentes, representando el 12.93% del total, mientras que las Comunas 4, 9 y 8 también registran un alto número de incidentes. Por otro lado, las Comunas 2, 5, 6 tienen la menor cantidad de incidentes. Estos hallazgos resaltan la variabilidad en la seguridad entre las comunas y proporcionan información valiosa para la asignación de recursos y la toma de decisiones en materia de seguridad pública.  

    Como información adicional, decido armar un dataframe a partir de un excel que armé con los barrios por comuna como para identificar los siniestros en el contexto de los barrios de CABA. Para esto lo cruzo luego con la info de siniestros por comuna y agrego a los barrios como labels en eje "y" luego de realizar un gráfico de barras horizontales por el largo de las etiquetas. Luego de observar esta información, parece coherente que los barrios con más movimiento como ser Retiro y Puerto Madero, registren un mayor número de incidentes.  

Decido utilizar la información de la variable **DIRECCIÓN NORMALIZADA:**
- ya que tiene la info de las 2 calles en caso de intersecciones y utilizarla para analizar las intersecciones con más registros. Por esta misma razón, elimino del dataset la variable CRUCE. El análisis EDA revela información interesante sobre los cruces de calles más frecuentes en relación con la cantidad de incidentes registrados. En el conjunto de datos, se observa que el cruce "27 DE FEBRERO AV. y ESCALADA AV." es el más recurrente, con un total de 5 incidentes registrados en ese lugar. Le siguen de cerca otros cruces destacados como "PAZ, GRAL. AV. y BALBIN, RICARDO, DR. AV." y "PAZ, GRAL. AV. y DEL LIBERTADOR AV." con 4 incidentes cada uno. Además, varios cruces comparten una frecuencia de 3 incidentes, lo que sugiere áreas de interés adicional para analizar.  

Al realizar un análisis de distribución de la variable **PARTICIPANTES:**
- se destaca que la categoría 'Peatón-Pasajeros', con el formato (Víctima/Acusado), muestra la mayor cantidad de registros. Sin embargo, es importante señalar que este patrón podría deberse a una posible interpretación errónea en la clasificación de los involucrados. Según el diccionario de datos, un 'pasajero' se define como 'personas lesionadas que se encuentran dentro, descendiendo o ascendiendo de las unidades de autotransporte público de pasajeros/as y ómnibus de larga distancia'. Por lo tanto, es probable que en algunos casos se haya intentado representar la situación en la que la víctima es un peatón y el acusado sea, por ejemplo, un conductor de un vehículo de transporte público. Esta observación resalta la importancia de una revisión más detallada de la clasificación de los involucrados para garantizar la precisión de los datos y su interpretación adecuada en futuros análisis y decisiones relacionadas con la seguridad vial. Desido tomar como que es un íncidente en el que participa un peatón como víctima y un transporte de pasajeros como acusado.  

Cuando analizamos la información de manera separada, enfocándonos en **'Víctimas' y 'Acusados'**
- se revelan patrones interesantes en relación con los tipos de vehículos involucrados en los incidentes. En el caso de las 'Víctimas', se destaca que las motocicletas son las que registran la mayor cantidad de incidentes. Esta tendencia puede explicarse por la vulnerabilidad inherente de las motocicletas en las vías de alto tráfico, así como la urgencia en los servicios de entrega que involucran este tipo de vehículos. Además, algunos incidentes pueden estar relacionados con conductores que no respetan las normas de tráfico o que participan en carreras en las vías.

    Por otro lado, al analizar los 'Acusados', tiene sentido que los automóviles representen la mayoría de los registros. Esto se ajusta a la información adicional sobre las horas de mayor incidencia, que confirma que son los automóviles los que más circulan por las diversas vías, especialmente durante las 'horas pico'. Esta mayor presencia de automóviles en las carreteras durante períodos de tráfico intenso está en línea con la mayor cantidad de incidentes en los que están involucrados como acusados. Este análisis resalta la importancia de considerar tanto la cantidad de vehículos en las vías como sus comportamientos al evaluar la seguridad vial y las estrategias para reducir los incidentes.  


Al consumir la hoja "Victimas", decido quedarme solamente con las columnas "ID_hecho", "ROL", "VICTIMA", "SEXO", "EDAD", "FECHA_FALLECIMIENTO" ya que son las que contienen información adicional referente a las víctimas, que no tenía el anterior Dataset.  

Variable **Roles:**
- Al observar los datos en términos de roles desempeñados en los incidentes, se destaca una distribución interesante. Los conductores representan el mayor porcentaje de casos, con un 46% del total. Esto sugiere que la mayoría de los incidentes involucran a conductores como actores principales en los eventos.  

    Los peatones también tienen una presencia significativa, abarcando el 37,2% de los casos. Este alto porcentaje refleja la vulnerabilidad de los peatones en las vías y la importancia de las medidas de seguridad para proteger a este grupo.  

    Los pasajeros o acompañantes, con un 11.2%, constituyen otro grupo significativo en los incidentes. Este porcentaje puede relacionarse con situaciones en las que los pasajeros también se ven afectados por la conducción de terceros.  

    Los ciclistas, con un 4.18%, representan una proporción menor, pero aún así significativa, de los incidentes. La presencia de ciclistas en las vías también requiere consideración especial en términos de seguridad vial.  

    Finalmente, la categoría 'SD' (sin datos) representa un pequeño porcentaje del total de casos, con un 1.59%. Estos casos pueden requerir una revisión adicional para garantizar que no haya información faltante o incorrecta.  

    Este análisis porcentual resalta la diversidad de roles involucrados en los incidentes, subrayando la importancia de enfoques de seguridad vial adaptados a las necesidades específicas de cada grupo, desde conductores hasta peatones y ciclistas, para reducir los incidentes y mejorar la seguridad en las vías.  

Cuando examinamos la distribución de roles en términos de **víctimas en los incidentes:**
- se revela una diversidad de situaciones.  
    Las motocicletas son las víctimas más frecuentes, representando el 42,30% de los casos. Esta alta proporción puede explicarse por la vulnerabilidad de las motocicletas en las vías de tráfico intenso, así como por la prevalencia de servicios de entrega que involucran este tipo de vehículos.

    Los peatones también tienen una presencia significativa como víctimas, constituyendo el 37,2% de los incidentes. Esto destaca la importancia de medidas de seguridad para proteger a los peatones en las vías y reducir los incidentes en los que se ven involucrados.

    Los automóviles representan un 13,1% de las víctimas en los incidentes, lo que puede estar relacionado con choques entre vehículos o incidentes en los que los automóviles son golpeados por otros actores en la vía.

    Los ciclistas, con un 4%, constituyen un grupo menos frecuente de víctimas, pero aún significativo. Esto enfatiza la necesidad de promover la seguridad de los ciclistas en las carreteras.

    Las categorías 'SD' (sin datos), 'CARGAS', 'PASAJEROS' y 'MOVIL' tienen una presencia más limitada como víctimas, representando un pequeño porcentaje del total de casos. Estos casos menos frecuentes pueden requerir una revisión adicional para garantizar la integridad de los datos.  

Cuando analizamos la distribución de **género** en los datos:
- observamos que los individuos de género masculino representan el 76% de los casos, mientras que las personas de género femenino constituyen el 23%. Esta diferencia en la distribución de género refleja una prevalencia significativa de individuos de género masculino en los incidentes registrados.

    Es importante tener en cuenta que, aunque la mayoría de los registros corresponden a individuos de género masculino, esto no implica necesariamente que sean responsables de los incidentes. La información adicional y un análisis más detallado pueden ayudar a comprender mejor las circunstancias de los incidentes y los roles desempeñados por individuos de diferentes géneros.

    Buscando información adicional que ayude a explicar esta brecha tan grande, encontramos un estudio realizado en 2021 por Caja Seguros y curado por socióloga y especialista en movilidad urbana Leda Pereyra acerca de los hábitos y las costumbres en el escenario vial que revela lo siguiente:

        "La muestra estuvo compuesta de 400 casos, de los cuales la mitad fueron mujeres y la mitad, hombres de entre 18 y 60 años. El 50% reside el Área Metropolitana de Buenos Aires (AMBA), un 15% de Mendoza, otro 15% de Córdoba, un 10% de Tucumán y otro 10% de Río Negro.

        Algunos de sus resultados indican que, la edad promedio en que empiezan a conducir es más alta que la de los varones. No obstante, aunque entre 7 y 8 de cada 10 mujeres no cuentan con licencias de conducir, la cantidad de conductoras aumentó en los últimos años.
    
        También los resultados indican que en los autos, el 18,6% es conducido por mujeres y el 81,4 por hombres. En cuanto a motos los porcentajes son de 21,3 y 78,7% para mujeres y hombres respectivamente"

    Esto explica claramente la diferencia en cuanto a la tasa de víctimas hombres respecto a mujeres.

    También se observa un pequeño porcentaje de registros con la categoría 'SD' (sin datos), que representa el 1.0%. Estos casos pueden requerir una revisión adicional para garantizar la integridad de la información.  

Análisis de la columna **EDAD**
- en los datos revela una diversidad de edades en los incidentes registrados. En primer lugar, se destaca que un número significativo de registros, específicamente 53, presenta la categoría 'SD', que indica datos sin especificar o ausentes en relación con la edad de los involucrados en los incidentes.

    Excluyendo los registros con datos faltantes, se observa una variedad de edades que van desde los 1 hasta los 88 años. El conjunto de datos contiene un total de 86 valores únicos de edad. La edad más frecuente entre los registros es 'SD', lo que sugiere que la información sobre la edad de los involucrados en los incidentes no está completa en una proporción significativa de los casos.

    Es importante destacar que, aunque la categoría 'SD' predomina en términos de frecuencia, esto no necesariamente refleja la distribución real de edades en los incidentes. La falta de información sobre la edad en algunos registros puede dificultar la evaluación precisa de la distribución de edades en el conjunto de datos.

    En resumen, el análisis de la columna 'EDAD' destaca la necesidad de una recopilación más completa y precisa de datos sobre la edad de los involucrados en los incidentes para facilitar una comprensión más profunda de la distribución de edades y su relevancia en la seguridad vial. Dado este escenario, realizamos más análisis, aplicando un histograma y un diagrama de caja:  

    El histograma de edades muestra la distribución de edades de las víctimas en el conjunto de datos. En el eje horizontal, tenemos la edad, y en el eje vertical, tenemos la frecuencia (es decir, cuántas víctimas tienen cada edad). Algunas observaciones:

    La mayoría de las víctimas parecen estar en el rango de edades más jóvenes, con un pico en la frecuencia alrededor de los 30 años.
    La media de edad es de aproximadamente 42.17 años, lo que significa que, en promedio, las víctimas tienen alrededor de 42 años.
    La mediana, que es el valor que divide el conjunto de datos en dos mitades iguales, es de 37.0 años. Esto indica que el 50% de las víctimas tiene 37 años o menos, y el otro 50% tiene más de 37 años.
    La desviación estándar de 19.79 nos indica la dispersión de las edades alrededor de la media. En este caso, la desviación estándar relativamente alta indica que las edades están bastante dispersas y no están muy centradas alrededor de la media.
    El mínimo valor de edad en el conjunto de datos es 1 año, lo que sugiere que hay víctimas muy jóvenes.
    El primer cuartil (25%) de las edades está en 27 años, lo que significa que el 25% más joven de las víctimas tiene 27 años o menos.
    El tercer cuartil (75%) de las edades está en 56.25 años, lo que indica que el 25% más viejo de las víctimas tiene 56.25 años o más.
    El máximo valor de edad en el conjunto de datos es de 95 años, lo que indica que hay víctimas de edades avanzadas.  

    El diagrama de caja muestra la distribución de edades de manera gráfica y nos proporciona una representación visual de los datos.
    La línea en el medio de la caja representa la mediana, que es de 37.0 años, lo que concuerda con la mediana calculada anteriormente.
    La caja representa el rango intercuartil (IQR) y abarca desde el primer cuartil (25%) hasta el tercer cuartil (75%). El IQR es una medida de la dispersión en el centro de los datos.
    Los "bigotes" se extienden desde la caja y representan la dispersión de los datos fuera del IQR. Cualquier punto fuera de los bigotes se considera un valor atípico.
    En este caso, parece que hay valores atípicos (puntos individuales) hacia las edades más avanzadas, lo que concuerda con el valor máximo de 95 años.
    La longitud de la caja y la posición de la mediana nos dan una idea de la simetría o asimetría de la distribución. En este caso, la caja es más corta en la parte inferior, lo que sugiere una asimetría hacia edades más jóvenes.  

Decido armar otro excel con la información de población por comuna donde presento 2 columnas, COMUNA que es el ID por el cual luego voy a enlazar la información y el número de habitantes por comuna. Para obtener esta información, consulto el Censo Nacional de Población, Hogares y Viviendas 2022 disponibe en el siguiente enlance [link](https://www.indec.gob.ar/ftp/cuadros/poblacion/cnphv2022_resultados_provisionales.pdf).  

## KPI

En función de lo analizado en el punto anterior, se plantearon tres objetivos en relación a la disminución de la cantidad de víctimas fatales de los siniestros viales, desde los cuales se proponen tres indicadores de rendimiento clave o KPI.

1. Reducir en un 10% la tasa de homicidios en siniestros viales de los últimos seis meses, en CABA, en comparación con la tasa de homicidios en siniestros viales del semestre anterior*

    Las tasas de mortalidad relacionadas con siniestros viales suelen ser un indicador crítico de la seguridad vial en una región. Se define como **Tasa de homicidios en siniestros viales** al número de víctimas fatales en accidentes de tránsito por cada 100,000 habitantes en un área geográfica durante un período de tiempo específico, en este caso se toman 6 meses. Su fórmula es:

    $\text{Tasa de homicidios en siniestros viales} = \frac{\text{Número de homicidios en siniestros viales}}{\text{Población total}}·100,000$

    Como *Población Total* se calculó la población para el año 2021 a partir de los censos poblacionales del año 2010 y 2022.

    En este caso, para el año 2021, la *Tasa de homicidios en siniestros viales* fue de 1.77 lo que significa que, durante los primeros 6 meses del año 2021, hubo aproximadamente 1.77 homicidios en accidentes de tránsito por cada 100,000 habitantes. Ahora, el objetivo planteado es reducir esta tasa para el siguiente semestre de 2021 en un 10%, esto es **1.60**. Cuando se calcula el KPI para este período se obtiene que la *Tasa de homicidios en siniestros viales* fue de **1.35**, lo que significa que para el segundo semestre de 2021 se cumple con el objetivo propuesto.  


  

2. Reducir en un 7% la cantidad de accidentes mortales de motociclistas en el último año, en CABA, respecto al año anterior*

    Como se vio en el análisis exploratorio, el 42% de las víctimas mortales se transportaban en moto al momento del hecho. Por lo que se consideró importante proponer el monitoreo de la cantidad de accidentes mortales en este tipo de conductor. Para ello se define a la **Cantidad de accidentes mortales de motociclistas** como el número absoluto de accidentes fatales en los que estuvieron involucradas víctimas que viajaban en moto en un determinado periodo temporal. La fórmula para medir la evolución de los accidentes mortales con víctimas en moto es:  
    
    $\text{Cantidad de accidentes mortales de motociclistas} = -\frac{\text{Víctimas moto año anterior - Víctimas moto año actual}}{\text{Víctimas moto año anterior}}·100$

    Donde:
    - $\text{Víctimas moto año anterior}$: Número de accidentes mortales con víctimas en moto en el año anterior
    - $\text{Víctimas moto año actual}$: Número de accidentes mortales con víctimas en moto en el año actual 

    Para este caso, se toma como año actual al año 2021 y como año anterior al año 2020. En primer lugar, se calculó la *Cantidad de accidentes mortales de motociclistas* para el año 2020, el cual resultó de 27, de esta manera el objetivo a cumplir es de **25** (es decir, la reducción del 7% de la cantidad de accidentes para 2021). El calcular la *Cantidad de accidentes mortales de motociclistas* para el año 2021 resultó de **46** lo que significa que aumentó un 70% la cantidad de muertes de conductores de motociclistas respecto del 2021.  


  
  
3. Reducir en un 30% la tasa de homicidios de peatones en 2021, en CABA, respecto al año 2016.

    Basándome en el objetivo del Plan de Seguridad Vial trabajado, que era reducir en un 30% los homicidios a causa de sinientros viales, decido llevar este objetivo pero trabajarlo para los peatones con el rango de fechas disponible en el dataset, por esta razón comparo los valores entre diciembre 2021 y diciembre 2016. Su fórmula es:  
    
    $\text{Reducción Tasa Mortalidad Peatones 2016-2021} = \frac{\text{Tasa Mortalidad Peatones 2016 - Tasa Mortalidad Peatones 2021}}{\text{Tasa Mortalidad Peatones 2016}}$

En la siguiente imagen se aprecian los rendimientos de los tres KPI propuestos.

![KPI](Images/KPI%C2%B4S.png)
