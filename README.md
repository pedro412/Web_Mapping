## ARQUITECTURA DE PROYECTO WEB MAPPING

Estos son los requerimientos mínimos necesarios para montar una infraestructura de web mapping.
	
Se dividirá en dos bloques FRONTEND y BACKEND


BACKEND(servidor)

	- Servidor: Apache o IIS.
	- Instalación de base de datos POSTGRESQL con extensión POSTGIS.
	- Servidor de mapas: GeoServer.
	- Restful API's para autenticación y autorización(opcional).
	  Estos apis se pueden hacer con PHP o .NET (1).

FRONTEND(cliente)

	- QGIS para la interacción de usuario con la base de datos.
	- Una aplicación web donde se consumirán los servicios de GeoServer para poder visualizar las capas.
	  Esta aplicación debe utilizar algún framework de mapas tal como OpenLayers, Leaflet o Arcgis API.
	  Debe tener una restricción desde el BACKEND para que no cualquiera pueda visualizar el contenido.(1)
	- Utilizar algún framework o librería de JavaScript para crear aplicaciones robustas: ReactJs o Angular.
	
	

-----------------------------------------------------------------------------------------------------------------


### SERVIDOR

En la empresa se cuenta con servidores IIS de Windows los cuales son muy ventajosos al momento de montar e instalar
las aplicaciones, o base de datos, ya que todo se hace mediante interfaz gráfica.


Otra opción sería rentar algún VPS o Virtual Private Server, que generalmente usan servidores Apache,
estos vienen con la desventaja de que hay que configurar todo manualmente, a diferencia del IIS,
estos servidores generalmente vienen montados en un sistema operativo Linux, y todo lo que se requiera instalar
debe ser mediante uso de línea de comando, cuando no se tiene un conocimiento avanzado, esto puede demorar mucho tiempo.




### BASE DE DATOS
Aquí no hay mucho tema, todas las interacciones no se hacen directamente, siempre se hacen a través de QGIS o el servidor de mapas.



### SERVIDOR DE MAPAS
El servidor de mapas es una aplicación que se encarga de hacer muchas cosas por nosotros, si este no existiera se tendría que
hacer una aplicación que tuviera todas la funciones que llegásemos a necesitar, lo cual es mucho desarrollo y tiempo.
Algunas de esas cosas que este servidor puede hacer por nosotros es: publicar un servicio web de las capas, listo para 
ser consumido desde cualquier cliente que acepte HTTP, ya sea una aplicación de teléfono o una página web.
También si se quisiera optar por otro tipo de desarrollo digamos usar Python, este servidor nos puede entregar un JSON que 
prácticamente puede ser utilizado y manipulado desde cualquier lenguaje de programación.



### RESTFUL API'S
Para entender esto se debe primero entender que son los servicios web, los servicios web son funciones creadas en algún lenguaje de programación que tenga capacidades de interactuar con una base de datos para hacer consultas a la misma, manipular archivos, en otras palabras en un lenguaje del lado del servidor, los lenguajes más comunes para web: PHP, NodeJS, Python, C#(.NET) y Java(no confundir Java con JavaScript ya que son dos cosas diferentes).
Estas funciones realizan tareas específicas, tal como sumar dos números hasta devolver todos los registros de una base de datos.
Se les llama servicios web porque en teoría todo lo que tienes que hacer para invocarlos es usar una URL que se asignó a dicha función o servicio.

Por ejemplo: se requiere consumir un servicio web para sumar dos cifras:

    copias y pegas esto en tu navegador...
    
    http://www.miDominio.com/sumarNumeros?numero1=5&numero2=6 
    
    pasa la magia y esto nos regresa una respuesta en formato XML o JSON, generalmente retornan un JSON.
    
```javascript
    respuesta:[{
	numero1: 5,
	numero2: 6,
	suma: 11 //<-- este es el resultado de la función que se ejecutó en el servidor.
    }]
````

    	*http* es el protocolo por cual se realizara la consulta.
	*www.miDominio.com* es el ip o dominio(DNS) que se utiliza.
	*/sumarNumeros* es la función que se ejecutara y a esta se le pasan los parámetros después del signo ? numero1=5&numero2=6

   








### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/pedro412/Web_Mapping/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
