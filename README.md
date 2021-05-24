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
### Creación y configuración Watson Knowledge Studio  :wrench:
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
### Despliegue del modelo Machine Learning  :space_invader:
En la pestaña ***Machine Learning Model*** de click en ***Versions***, luego seleccione la opción ***Create Version***, allí saldrá la acción **Deploy**, seleccione ***Natural Lenguage Understanding***, de click en **Next** y seleccione la región donde se creo el servicio, el grupo de recurso donde se encuentra y el servicio creado de ***Natural Lenguage Understanding***, finalmente de click en **Deploy**.
Una vez se ha desplegado el modelo en el servicio, podrá ver el **Model-ID** el cual deberá copiar y pegar en un bloc de notas para su posterior uso en el paso 3.
## Paso 3
### Cambio de credenciales según el servicio creado  :arrows_counterclockwise:
En Windows PowerShell, se debe ubicar en la carpeta Back del repositorio y modificar el archivo **params.json** con las credenciales de su servicio y modelo:
- Para modificar el archivo, ejecute el comando 
```
nano params.json
```
Guarde los cambios con **Ctrl+s** y salga del editor con **Ctrl+x**
## Paso 4
### Ejecución local y prueba  :computer:
- Ejecutar los comandos ```npm install``` y ```npm start```. Al ejecutar el último comando, se visualiza una dirección de localhost con su puerto correspondiente, en este caso **http://localhost:6001** <p align="center"><img width="800" src="https://github.com/emeloibmco/Watson-NLU-NodeJS-Application/blob/main/Imagenes/Picture1.jpg"></p>
- Probar desde Postman la ruta http://localhost:6001/upload-text definiendo el body de la siguiente manera: <p align="center"><img width="800" src="https://github.com/emeloibmco/Watson-NLU-NodeJS-Application/blob/main/Imagenes/body_postman.jpg"></p>
- Verificar que este seleccionada la opción **POST** al lado ruta que va a probar, de click en **Send** y así se debe obtener el siguiente resultado: <p align="center"><img width="800" src="https://github.com/emeloibmco/Watson-NLU-NodeJS-Application/blob/main/Imagenes/resultado.jpg"></p> Este resultado verifica que funciona la aplicación Backend y puede ser desplegada.
## Paso 5
### Despliegue de aplicación Backend  :rocket:
En este caso se despliega la aplicación en Kubernetes, los pasos se explican a continuación:
1. En el archivo Dockerfile se debe verificar que en la linea 13 del codigo este mencionado el puerto donde se probo la aplicación en el paso 4.
2. En la misma ventana del PowerShell donde estaba corriendo la aplicación Backend, debe para el proceso con **Ctrl+c**.
3. Ejecutar el comando ```docker build -t <nombre-imagen:tag> . ```. Establezca cualquier nombre a la imagen y como tag **v1**, posteriormente en docker se debe verificar que aparezca la imagen creada.
4. En Docker, de click en **Run** a la imagen creada, luego **Optional Settings** y digitar 6001 en localhost. Para verificar el funcionamiento nos dirigimos al navegador y colocamos http://localhost:6001, como resultado se puede observar CANNOT GET / (Este resultado se obtiene porque el Backend recibe los datos del Frontend cuando se despliegue)
5. Ingrese a su cuenta de IBM por medio del PowerShell ejecutando el comando
```
ibmcloud login --sso
```
>**NOTA**: Se debe tener creado en la cuenta el cluster donde se va a desplegar la app.
7. Ejecutar el comando donde se selecciona el grupo de recursos donde esta el cluster 
```
ibmcloud target -g <nombre-recurso>
```
9. Ingresar al container registry ejecutando el comando 
```
ibmcloud cr login
```
10. Añadir un espacio con el comando 
```
ibmcloud cr namespace-add <nombre-espacio>
```
11. Ejecutar el comando que añade la imagen docker en el espacio creado
```
docker tag <nombre-imagen:tag> us.icr.io/<nombre-espacio>/<nombre-imagen:tag>
```
12. Ejecutar el comando
 ```
 docker push us.icr.io/<nombre-espacio>/<nombre-imagen:tag>
 ```
13. Ingresar al cluster donde se va a desplegar la aplicación  
```
ibmcloud ks cluster config --cluster <nombre-cluster>
```
14. Crear el despliegue con el comando 
```
kubectl create deployment <nombre-despliegue> --image=us.icr.io/<nombre-espacio>/<nombre-imagen:tag>
```
15. Exponer el despliegue
```
kubectl expose deployment/<nombre-despliegue> --type=LoadBalancer --name=<nombre-app>  --port=<puerto-especificado-en-dockerfile> --target-port=<puerto-especificado-en-dockerfile>
```
16. Ingresar desde IBM Cloud al panel de kubernetes y buscar el despliegue, verificar que no existan errores.
17. Ir a la pestaña SERVICES y dar click en la URL mostrada en la columna External Points
>**NOTA**: Debe esperar unos minutos mientras se realiza el despliegue, refresque la página y verifique que no salgan errores de carga, debe aparecer nuevamente CANNOT GET /
<p align="center"><img width="800" src="https://github.com/emeloibmco/Watson-NLU-NodeJS-Application/blob/main/Imagenes/Picture2.jpg"></p>

## Paso 6
###  Despliegue de aplicación Frontend  :rocket:
Para el despliegue de la aplicación Frontend se deben ejecutar los mismos pasos realizados en el despliegue de la aplicación Backend exceptuando lo siguiente:
1. Se debe agregar la dirección URL del Back del paso 5 en la linea 15 del archivo **nlu.component.ts** ubicado en **Front>src>app>components>nlu**.
2. En el archivo Dockerfile se debe verificar que en las lineas 8 y 9 del codigo este mencionado el puerto donde se probo la aplicación en el paso 4.
3. Al correr la imagen creada en Docker, digitar el puerto 8080 en localhost y verificar el funcionamiento en el navegador con la direccion http://localhost:8080, allí se puede visualizar el siguiente resultado: <p align="center"><img width="800" src="https://github.com/emeloibmco/Watson-NLU-NodeJS-Application/blob/main/Imagenes/f1.jpg"></p>
4. Finalmente, con la URL dada en Kubernetes se debe verificar y visualizar el mismo resultado dado en el numeral 2. <p align="center"><img width="800" src="https://github.com/emeloibmco/Watson-NLU-NodeJS-Application/blob/main/Imagenes/f2.jpg"></p>

## Referencias
* <a href="https://cloud.ibm.com/docs/watson-knowledge-studio?topic=watson-knowledge-studio-wks_tutintro">IBM Watson Knowledge Studio</a>
* <a href="https://cloud.ibm.com/docs/natural-language-understanding?topic=natural-language-understanding-getting-started#getting-started-tutorial">IBM Watson Natural Lenguage Understanding</a>

## Autores ✒️
* Equipo IBM Cloud Tech sales Colombia.
