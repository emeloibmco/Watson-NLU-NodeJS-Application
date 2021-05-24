# Watson-NLU-NodeJS-Application :speech_balloon:
IBM Watson™ Natural Lenguage Understanding es un servicio que ayuda a analizar varias características de contenido de texto a escala. Con IBM Watson™ Natural Language Understanding, los desarrolladores pueden analizar las características semánticas de la entrada de texto, incluidas categorías, conceptos, emociones, entidades, palabras clave, metadatos, relaciones, roles semánticos y sentimientos.

## Indice  :book:
1. [Pre-Requisitos](#Pre-Requisitos)
2. [Paso 1. Creación y configuración Watson Knowledge Studio](#Paso-1)
3. [Paso 2. Despliegue del modelo Machine Learning](#Paso-2)
4. [Paso 3. Cambio de credenciales según el servicio creado](#Paso-3)
5. [Paso 4. Ejecución local y prueba](#Paso-4)
6. [Paso 5. Despliegue de aplicación Backend](#Paso-5)
7. [Paso 6. Despliegue de aplicación Frontend](#Paso-6)

## Pre-Requisitos
+ Clonar el repositorio en su máquina
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
- En el panel del diccionario, de click en ***Upload***, allí debe añadir el archivo **dictionary-items-cars.csv*** que se encuentra en la carpeta ***Archivos*** de este repositorio. 
>**NOTA**: Si desea añadir otra palabra o conjuntos de palabras al diccionario, se puede agregar dando click en ***Add Entry*** en el panel del diccionario, o modificar el archivo desde su ordenador.
5. Crear un modelo Machine Learning
- De click en ***Assets*** y luego en la pestaña ***Documents***, en la pagina de documentos, de click en ***Upload Documents Sets***, allí debe añadir el archivo **documents-new-copy.csv** que se encuentra en la carpeta ***Archivos*** de este repositorio. Este archivo contiene los relatos de los accidentes mencionados por las personas, si desea modificar los relatos debe hacerlo directamente en el archivo.
- En la pestaña donde se encuentra el diccionario, debe seleccionar el tipo de entidad ***EVENT_DISASTER*** para comenzar a entrenar el modelo de aprendizaje automático.
<p align="center"><img width="800" src="https://github.com/emeloibmco/Watson-NLU-NodeJS-Application/blob/main/Imagenes/Diccionario.jpg"></p>

- En la pestaña ***Machine Learning Model***, de click en ***Pre-annotation*** y luego en ***Run Pre-annotators***, seleccione **Dictionary** y luego de click en **Next**, seleccione el documento **documents-new-copy.csv** y de click en **Run**.
- Dirijase a la pestaña ***Annotations***, allí seleccione **Annotation Tasks** y luego de click en **Add task**, especifique los detalles de la tarea (Ej: En el campo **Task name** ingrese "Relatos" y en el campo **Deadline** seleccione una fecha en el futuro)
- De click en ***Create Annotation Sets*** donde en el campo ***Annotator*** selecciona su usuario y en ***Set name*** le otorga un nombre al conjunto (Ej: Set1), finalmente de click en ***Generate*** y luego en ***Save***.
- Una vez creado el conjunto de tareas, en la parte derecha, de click en ***Annotate***, allí verá la lista de relatos, seleccione el relato llamado "Accidente - mazda" y asigne manualmente las relaciones y menciones que hay en el relato. <p align="center"><img width="800" src="https://github.com/emeloibmco/Watson-NLU-NodeJS-Application/blob/main/Imagenes/r1.jpg"></p><p align="center"><img width="800" src="https://github.com/emeloibmco/Watson-NLU-NodeJS-Application/blob/main/Imagenes/r2.jpg"></p>
En el menú de estado, seleccione ***Completed*** y luego de click en el botón **Save**
>**NOTA**: Este proceso se debe hacer por cada relato para entrenar el modelo.
- Para finalizar con la creación y entrenamiento del modelo, dirijase a la pestaña ***Performance***, allí debe dar click en **Train & Evaluate**.
>**NOTA**: El proceso puede tardar más de 10 minutos o incluso horas dependiendo del número de anotaciones y palabras en los documentos.
## Paso 2
### Despliegue del modelo Machine Learning
En la pestaña ***Machine Learning Model*** de click en ***Versions***, luego seleccione la opción ***Create Version***, allí saldrá la acción **Deploy**, seleccione ***Natural Lenguage Understanding***, de click en **Next** y seleccione la región donde se creo el servicio, el grupo de recurso donde se encuentra y el servicio creado de ***Natural Lenguage Understanding***, finalmente de click en **Deploy**.
Una vez se ha desplegado el modelo en el servicio, podrá ver el **Model-ID** el cual deberá copiar y pegar en un bloc de notas para su posterior uso en el paso 3.
## Paso 3
### Cambio de credenciales según el servicio creado
En windows PowerShell, se debe ubicar en la carpeta Back del repositorio y modificar el archivo **params.json** con las credenciales de su servicio y modelo:
- Para modificar el archivo, ejecute el comando 
```
nano params.json
```
Guarde los cambios con **Ctrl+s** y salga del editor con **Ctrl+x**
## Paso 4
### Ejecución local y prueba
- Ejecutar los comandos ```npm install``` y ```npm start```. Al ejecutar el ultimo comando, se visualiza una direccion de localhost con su puerto correspondiente


