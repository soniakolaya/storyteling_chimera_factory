
 # Titulo Proyecto🎞️

A continuación encontraras la documentación del modelo de datos para los conjunto de datos `Movie and TV Shows`de las plataformas [Netflix](https://www.kaggle.com/datasets/shivamb/netflix-shows ), [Disney +](https://www.kaggle.com/datasets/shivamb/disney-movies-and-tv-shows) y [Prime Video](https://www.kaggle.com/datasets/shivamb/amazon-prime-movies-and-tv-shows ). 
La base total contiene 19.925 registros, donde un 49% es de Prime, un 44% de Netflix, y un 7% de Disney +. Este compuesto por diferentes columnas las cuales contienen detalle del elenco, directores, calificaciones, año de lanzamiento, país de producción y duración de la película. 

## Documentación modelado
A. Descripción del metadatos de las variables originales.


| Variable            | Descripción                                                                                                           | Tipo de Dato   |
|---------------------|-----------------------------------------------------------------------------------------------------------------------|----------------|
| **show_id**          | Identificador alfanumérico único de la película o serie en la plataforma.                                                       | `text`     |
| **type**          | Descripción o tipo de cotenido (categorias: movie, tv show)..                                                       | `text`     |
| **title**          | Titulo de la película o serie..                                                       | `text`     |
| **director**          | Nombre del director de la película o serie.                                                       | `text`     |
| **cast**          | Nombres de los actores que participaron.                                                       | `text`     |
| **country**          | País(es) donde está disponible.                                                       | `text`     |
| **date_added**          | Fecha en que se agregó a la plataforma.                                                       | `datetime`     |
| **release_year**          | Fecha en que se lanzó al público.                                                       | `datetime`     |
| **rating**          | Clasificación del contenido.                                                       | `text`     |
| **duration**          | Duración en minutos (películas) o en temporadas (series).                                                       | `text`     |
| **listed_in**          | Categoría interna de la plataforma.                                                     | `text`     |
| **description**          | Descripción corta de la película o serie.                                                     | `text`     |

B. Paso a paso del modelado realizado.

En el [Notebook Modelamiento](https://github.com/soniakolaya/storyteling_chimera_factory/blob/master/Modelamiento.ipynb) se encuentra el código en Python del proceso que se va a detallar a continuación:

1. **Concatencación de los conjuntos de datos:** Se realiza una concatencación de todos los datos para cada plataforma, dado que son conjunto de datos separados.

2. **Creación de campos:** Creación de nuevo IDs para el nuevo conjunto de datos. Se renombra el campo `show_id`como `sub_show_id` y se crea un nuevo campo `show_id` con un índice consecutivo. Adicional, se crea el campo `streaming`, que indica la plataforma en donde esta disponible la película o serie.

3. **Eliminación de columnas**: Se eliminan las columnas que por tener un porcentaje alto de columnas con valores NaN (mayor del 90%), no se puede imputar. Se elimino la columna `director`.

4. **Eliminación de valores nulos**: Se eliminan los registros que tengan valores nulos en algunos de sus campos. Inicialmente se tenian 10.257 registros, luego de la eliminación de nulos se obtuvieron 9.207 registros.

5. **Mapeo de variables**: La variable `rating`contiene códigos alfanumérico que por estándar internacional tiene una descripción asociada. Se crea el campo `rating_description`que contiene  la descripción asociada a cada tipo de `rating`.

6. **Estandarización variables:**: Se estandarizó el campo `duration` que contenia en el mismo campo la duración en minutos de peliculas y temporadas de las series. Se creó tres campos nuevos: 
- `duration_num`: extracción de la parte numérica del campo `duration`.
- `duration_type`:  extracción del texto del campo `duration`.
- `standard_duration`: estandarización del tiempo en minutos (se toma en promedio 600 minutos para una temporada de serie).
Se estandarizó el campo `date_added` cambiando de formato "month day, year" a "dd/mm/yyyy".

7. **Separación de campos multivalor:** Para los campos que contiene categorias separadas por coma, se crea un registro nuevo por cada categoría. Esto se realiza sobre los campos `country`y `listed_in`.


8. **Guardar el nuevo conjunto de datos:** Se guarda el conjunto de datos en los formatos .csv y .parquet (extensión necesaria para cargue de datos en Big Query en Looker Studio).


C. Descripción del metadatos de las variables finales.


| Variable            | Descripción                                                                                                           | Tipo de Dato   |
|---------------------|-----------------------------------------------------------------------------------------------------------------------|----------------|
| **show_id**          | Identificador único de la película o serie.                                                       | `numeric`     |
| **sub_show_id**          | Identificador alfanumérico único de la película o serie en la plataforma.                                                       | `numeric`     |
| **type**          | Descripción o tipo de cotenido (categorias: movie, tv show).                                                       | `text`     |
| **title**          | Titulo del *show id*.                                                       | `text`     |
| **cast**          | Nombres de los actores que participaron en el *show id*.                                                       | `text`     |
| **country**          | País donde está disponible el *show id*.                                                       | `text`     |
| **date_added**          | Fecha en que se agregó el *show id*.                                                       | `datetime`     |
| **release_year**          | Fecha en que se lanzó al público el *show id*.                                                       | `datetime`     |
| **rating**          | Clasificación del contenido.                                                       | `text`     |
| **rating_description**          | Descripción de la clasificación del contenido del *show id*.                                                       | `text`     |
| **duration**          | Duración en minutos (películas) o en temporadas (series).                                                       | `text`     |
| **duration_num**          | Valor numérico de la duración del *show id*.                                                       | `numeric`     |
| **duration_type**          | Tipo de duración del *show id*.                                                       | `text`     |
| **standard_duration**          | Tiempo en minutos de la duración del *show id*.                                                       | `numeric`     |
| **listed_in**          | Categoría interna de la plataforma.                                                     | `text`     |
| **description**          | Descripción corta de la película o serie.                                                     | `text`     |






## Autores 

- Daniel Montero: [de.montero@uniandes.edu.co](de.montero@uniandes.edu.co)
- Juan Mejía: [jc.mejiam1@uniandes.edu.co](jc.mejiam1@uniandes.edu.co)
- Carlos Camacho: [ce.camachoc1@uniandes.edu.co](ce.camachoc1@uniandes.edu.co)
- Sonia Olaya: [sk.olaya@uniandes.edu.co](sk.olaya@uniandes.edu.co)
