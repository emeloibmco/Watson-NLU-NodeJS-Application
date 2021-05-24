# Watson-NLU-NodeJS-Application :speech_balloon:
IBM Watson™ Natural Lenguage Understanding es un servicio que ayuda a analizar varias características de contenido de texto a escala. Con IBM Watson™ Natural Language Understanding, los desarrolladores pueden analizar las características semánticas de la entrada de texto, incluidas categorías, conceptos, emociones, entidades, palabras clave, metadatos, relaciones, roles semánticos y sentimientos.

## Indice  :book:
1. [Pre-Requisitos](#Pre-Requisitos)
2. [Paso 1. Creación y configuración Watson Knowledge Studio](#Paso-1)
3. [Paso 2. Despliegue del modelo machine learning](#Paso-2)
4. [Paso 3. Cambio de credenciales según el servicio creado](#Paso-3)
5. [Paso 4. Ejecución local y prueba](#Paso-4)
6. [Paso 5. Despliegue de aplicación Backend](#Paso-5)
7. [Paso 6. Despliegue de aplicación Frontend](#Paso-6)

## Pre-Requisitos
+ Tener una cuenta en IBM Cloud
+ Tener creado el servicio Watson Knowledge Studio
+ Tener creado el servicio Watson Natural Lenguage Understanding

## Paso 1
### Creación y configuración Watson Knowledge Studio
1. Crear un espacio de trabajo y especificar los detalles, para este caso lo más importante que se debe especificar es el nombre y el lenguaje de los documentos que la herramienta debe analizar (Español).
2. Descargar el archivo <a href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/knowledge-studio/en-klue2-types.json">en-klue2-types.json</a> el cual contiene el sistema de tipos necesarios.
3. Crear un sistema de tipos en el espacio de trabajo:
- De click en ***Assets*** y luego en la pestaña ***Entity Types***, una vez haya ingresado, de click en ***Upload***, seleccione el archivo que descargo en su computador **en-klue-types.json** y de click en ***Upload***. Podrá visualizar la lista de tipos de entidades ingresadas como se muestra en la siguiente imagen: <p align="center"><img width="800" src="https://github.com/emeloibmco/Watson-NLU-NodeJS-Application/blob/main/Imagenes/Entity_types.jpg"></p>
4. Crear un diccionario y añadirlo en el espacio de trabajo
- De click en ***Assets*** y luego en la pestaña ***Dictionaries***, una vez haya ingresado, de click en ***Create Dictionary***, en el campo **Name**, digite ***Diccionario de accidentes*** y de click en guardar (El nuevo diccionario es creado y abierto automáticamente para editar).
- En el panel del diccionario, de click en ***Upload***, allí debe añadir el archivo **dictionary-items-cars.csv*** que se encuentra en la carpeta ***Archivos*** de este repositorio. Nota: Si desea añadir otra palabra o conjuntos de palabras al diccionario, se puede agregar dando click en ***Add Entry*** en el panel del diccionario, o modificar el archivo desde su ordenador.
5. Crear un modelo de aprendizaje automático
- De click en ***Assets*** y luego en la pestaña ***Documents***, en la pagina de documentos, de click en ***Upload Documents Sets***, allí debe añadir el archivo **documents-new-copy.csv*** que se encuentra en la carpeta ***Archivos*** de este repositorio. Este archivo contiene los relatos de los accidentes mencionados por las personas, si desea modificar los relatos debe hacerlo directamente en el archivo.
- En la pestaña donde se encuentra el diccionario, debe seleccionar el tipo de entidad ***EVENT_DISASTER*** para comenzar a entrenar el modelo de aprendizaje automático.
7.  
