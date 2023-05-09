# Comparación de las herramientas de procesamiento de datos Pandas, Koalas y Pyspark

En este proyecto se realizó una comparación básica de la eficiencia de las herramientas para el procesamiento de datos pandas, pyspark y koalas (pyspark.pandas). Para esto se utilizó el dataset Udemy Courses Exploration disponible en https://www.kaggle.com/code/wolfsdata/udemy-courses-exploration 

El dataset tiene un tamaño de 72.6 MB y contiene datos sobre los cursos ofrecidos por Udemy tales como el Id del curso, título, dirección url, nombre del instructor y número de estudiantes suscritos. 

Se realizó el mismo procesamiento de los datos en las tres herramientas con el objetivo de realizar una comparación de los profesores y los cursos más exitosos respecto al género del instructor. Se compararon los tiempos de ejecución, la sintaxis y las funciones disponibles en cada herramienta de procesamiento, con la finalidad de analizar cual es la más conveniente.

## Introducción

Pandas es una de las librerías de Python más importantes para el procesamiento de datos ya que brinda una gran cantidad de funciones para trabajar con dataframes que permiten limpiar y manipular los datos de manera sencilla utilizando la sintaxis intuitiva propia de python, además de que permite utilizar funciones definidas en python para modificar los dataframes. Sin embargo, una de las desventajas que presenta Pandas es que todas las operaciones se realizan en un único nodo, por lo que al trabajar con datasets grandes la ejecución puede ser lenta o imposible si no se cuenta con suficiente memoria.

Una alternativa para trabajar con grandes volúmenes de datos es Apache Spark, se trata de un framework open-source para procesamiento distribuido en clúster que cuenta con una API implementada en python llamada Pyspark. Apache Spark también permite la creación y manipulación de los datos mediante dataframes inspirados en los de Pandas pero con la ventaja de que permite ejecutar operaciones en paralelo utilizando diferentes nodos de un clúster lo que la vuelve más adecuada para procesar grandes volúmenes de datos. La sintaxis de Spark es distinta a la de Pandas y está muy influenciada por la sintaxis de SQL, por lo que puede resultar menos intuitivo para aquellas personas familiarizadas con la sintaxis de python.

Koalas es una API de Pandas en Apache Spark que une la sintaxis intuitiva de Pandas con el procesamiento en paralelo y los dataframes de Spark. Por ello es una herramienta muy util tanto para trabajar con conjuntos de datos pequeños como con datos distribuidos de gran volumen. Koalas fue integrado oficialmente a la distribución de Pyspark a partir de la versión 3.2 como Pandas.pyspark.

## Importar el dataset (formato CSV)

Al momento de importar el dataset y convertirlo en un dataframe para trabajar con el, se registraron los siguientes tiempos de ejecución.

|            | Pyspark | Pandas | Pyspark.pandas |
| :--------: | :-----: | :----: | :------------: |
| Tiempo (s) |  0.327  |  1.230 |     5.909      |

Como se puede ver, Pyspark requirió el menor tiempo para importar los datos en un dataframe, por otro lado, en cuanto a la sintaxis pyspark requiere que varios parámetros sean especificados al leer el archivo csv para poder darle estructura al dataframe; mientras que en Pandas no son necesarios tantos parámetros por lo que resulta más intuitivo. Por otro lado, Pandas.pyspark tomó el mayor tiempo en la lectura de los datos, aunque conservó la familiaridad de la sintaxis de Pandas.

## Manipulación del dataframe

Se realizaron distintas operaciones básicas en el dataframe, como mostrar el curso más antiguo y el más reciente con su fecha de publicación, contar el número de cursos por idioma y ordenar los cursos para mostrar los 10 con más subscriptores, para estas operaciones Pandas es la herramienta que realizó las tareas en el menor tiempo, seguido por Pyspark y siendo Pyspark.pandas la herramienta más lenta.

## Definiendo y usando UDF (User Defined Functions)

Se definió una función en python que permitiera extraer prefijos específicos de los nombres de los instructores. Dado que se trabajó con Pyton en los tres notebooks se definió la misma función; sin embargo, en Pyspark y Pyspark.pandas es necesario transformar la función de python mediante la función udf() de spark para poder usarla en el dataframe, esto no es necesario en Pandas ya que es una librería nativa de Python. Los efectos de esta transformación se reflejan en la eficiencia de la función definida por el usuario.

