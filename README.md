## ARQUITECTURA DE PROYECTO WEB MAPPING

Estos son los requerimientos mínimos necesarios para montar una infraestructura de web mapping.
	
Se dividirá en dos bloques FRONTEND y BACKEND


BACKEND(servidor)

	- Servidor web: Apache o IIS.
	- Instalación de base de datos POSTGRESQL con extensión POSTGIS.
	- Servidor de mapas: GeoServer.
	- Restful API'S AKA Web Services para la autenticación y autorización(opcional). (1)
	  Estos API'S se pueden hacer con PHP, Python(Django) o C#(.NET).
	  También pueden servir para manipular desde el cliente alguna capa determinada.

FRONTEND(cliente)

	- QGIS para crear, editar , visualizar, analizar y publicar información Geoespacial.
	- Una aplicación web donde se consumirán los servicios de GeoServer para poder visualizar las capas(y crear un tipo de QGIS personalizado en la web).
	  Esta aplicación debe utilizar algún framework de mapas tal como OpenLayers, Leaflet o Arcgis API.
	  Debe tener una restricción desde el BACKEND para que no cualquiera pueda visualizar el contenido. (1)
	- Utilizar algún framework o librería de JavaScript para crear aplicaciones robustas: ReactJs o Angular.
	
	

-----------------------------------------------------------------------------------------------------------------


### SERVIDOR

En la empresa se cuenta con servidores IIS de Microsoft los cuales son muy ventajosos al momento de montar e instalar
las aplicaciones, o base de datos, ya que todo se hace mediante interfaz gráfica muy parecido a Windows.


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



### WEB MAP SERVICES
Para entender esto se debe primero entender que son los servicios web, los servicios web son funciones creadas en algún lenguaje de programación que tenga capacidades de interactuar con una base de datos para hacer consultas a la misma, manipular archivos, en otras palabras en un lenguaje del lado del servidor, los lenguajes más comunes para web: PHP, NodeJS, Python, C#(.NET) y Java(no confundir Java con JavaScript ya que son dos cosas diferentes).
Estas funciones realizan tareas específicas, tal como sumar dos números hasta devolver todos los registros de una base de datos.
Se les llama servicios web porque en teoría todo lo que tienes que hacer para invocarlos es usar una URL que se asignó a dicha función o servicio.

Por ejemplo: se requiere consumir un servicio web para sumar dos números:

    copias y pegas esto en tu navegador...
    
    http://www.miDominio.com/sumarNumeros?numero1=5&numero2=6 
    
    pasa la magia y esto nos regresa una respuesta en formato XML o JSON, generalmente retornan un JSON.
    
```javascript
// Ejemplo de una respuesta en formato JSON, status 200 quiere decir que la petición fue exitosa

{
    status: 200,
    respuesta: [{
	numero1: 5,
	numero2: 6,
	suma: 11 // <-- este es el resultado de la función que se ejecutó en el servidor.
    }]
}
```

 - **http** es el protocolo por cual se realizara la consulta.

 - **www.miDominio.com** es el ip o dominio(DNS) que se utiliza.

 - **/sumarNumeros** es la función que se ejecutara y a esta se le pasan los parámetros después del signo ? numero1=5&numero2=6
 
 A muy grandes rasgos eso es un servicios web.
 
 Ahora se puede decir que GeoServer entre muchas cosas es también un despachador de servicios web orientado a GIS.
 
 
 
### CLIENTE
Se entiende por cliente cualquier dispositivo capaz de renderizar la vista al usuario, ya sea un dispositivo móvil, una laptop o desktop, un navegador web, es muy común que navegador web se confunda con motor de búsqueda, navegador web es la aplicación como CHROME o SAFARI, motor de búsqueda es Google o Bing. En el caso de web mapping el cliente será una página web, que consiste en 3 cosas fundamentales: HTML, CSS y JavaScript(no es lo mismo que Java).



**HTML**

NO es un lenguaje de programación, es un lenguaje de marcado ósea que para definir algo hay que usar etiquetas ejemplo:

```html
<div>aquí va el contenido</div>
```

Nótese el uso de etiquetas, **div** es el identificador de la etiqueta que definimos, hay varios tipo de etiquetas con sus respectivos nombres *div* es utilizado con frecuencia, las etiquetas siempre abren y se tienen que cerrar, HTML es muy parecido a XML solo que XML es más difícil de leer para los humanos, ya que XML fue creado para comunicación entre software, y HTML fue creado para que los humanos lo puedan leer y entender muy fácil.



**CSS**

Hoja de estilos, tampoco es un lenguaje de programación, es un lenguaje de estilos, usado para definir estilos específicos a las etiquetas HTML.
Usando la etiqueta anterior digamos que queremos cambiar el color de fondo.

```html
html

<div>aquí va el contenido</div>
```

```css
css

div {
 background-color: blue;
}
```



**JAVASCRIPT**

Por última vez, no confundir con Java ya que son dos lenguajes de programación distintos, la similitud del nombre fue gracias a los de marketing ya que cuando se lanzó JavaScript, Java era el lenguaje más popular del momento.
JavaScript si es un lenguaje de programación, con el cual, podemos declarar variables, crear condiciones y ciclos, declarar funciones que ejecuten determinada tarea.
JavaScript es un lenguaje que se ejecuta en el cliente ósea en tu navegador, con JavaScript podemos manipular casi cualquier cosa en una página.

Ejemplo, se requiere hacer que cuando el usuario de clic sobre la página el contenido de la etiqueta que definimos anteriormente sea 'Hola';

```html
html

<div id="cosaUno"></div>
```

A diferencia de la primera vez que se declaro, ahora tiene un atributo que se llama "id" y se le dio un valor = cosaUno, y adentro de las etiquetas no hay nada está vacio.

Primero necesitamos agarrar esa etiqueta con JavaScript

```javascript
// javascript

 var cosaUno = document.getElementById('cosaUno');
```

La palabra reservada *var* se usa para declarar variables, todo lo que paso en la instrucción anterior fue que guardamos esa etiqueta HTML en una variable, lista para ser manipulada. *document.getElementById()* es un método de JavaScript para seleccionar etiquetas HTML basado en un id.

Después procedemos a cambiar el valor que esa etiqueta tiene, que al momento está vacía.
pero primero necesitamos que el usuario de clic sobre la página.

¿Cómo podemos saber cuándo el usuario da clic sobre la página?.

Necesitamos esperar un evento, y para ello antes necesitamos una función que siempre este pendiente de cuando se da clic.

En el ejercicio dice que cuando el usuario de clic sobre la página, en cualquier parte.

Entonces necesitamos agarrar la etiqueta que define la página y esa etiqueta se llama HTML,

```html
html

<html id="pagina">
   <div id="cosaUno"><div>
</html>
```

```javascript
//javascript

var pagina = document.getElementById('pagina');
```

Ya que la tenemos en memoria, necesitamos agregar un EventListener que rastrea cualquier evento que definamos, en este caso queremos que rastree cuando el usuario da clic sobre la página.

```javascript
//javascript

pagina.addEventListener('click', function(){
	cosaUno.innerHTML = 'Hola';
});
```

Entonces cuando se dé clic se tendría lo siguiente:

```html
html

<html id="pagina">
   <div id="cosaUno">Hola<div>
</html>
```

Ahora se debe tener una idea más clara de lo que es una página web, HTML son los huesos con los que se construye, CSS es para darle forma a esa estructura, y JavaScript es para darle funcionalidad a lo que queramos y como lo queramos.



### FRAMEWORKS Y LIBRERÍAS DE JAVASCRIPT
Los frameworks  y/o librerías de JavaScript son funciones(echas con JavaScript) que adentro de ellas vienen muchas funciones pequeñas que sirven para un propósito, en el caso de web mapping, los frameworks tales como Leaflet y OpenLayers son para la manipulación y renderización de mapas y capas en una página web sin tener que partir de cero.

Ejemplo: https://unpkg.com/leaflet@1.3.4/dist/leaflet.js
Todo ese código es la ibrería de Leaflet ahí vienen todas las funciones que podemos utilizar.



### ROLES DE TRABAJO

**Desarrollador Front End**

Se encarga principalmente de trabajar del lado del cliente, debe tener un nivel avanzado en HTML, CSS y JavaScript.
Es muy común que siempre estén trabajando con frameworks y librerías de JS(JavaScript).
También existen frameworks de CSS para hacer prototipos de diseño en tiempo reducido.

Debe optimizar todo tipo de recurso que se entregue al usuario por ejemplo, una foto que pese 1MB es mucho para una página web, entonces se debe usar una herramienta como PhotoShop para reducir su peso a unos 100KB aproximadamente por decir algo. 

El UI/UX juega un rol importante para estos desarrolladores, no deben ser expertos pero si tener conocimientos intermedios.

En el caso de web mapping el desarrollador front end debe ser proficiente en algún framework de JS como OpenLayers para poder crear aplicaciones complejas, para esto debe tener conocimientos sólidos en JS tal como para usar algún Transpilador como TypeScript o por lo menos dominar un framework o librería como Angular o ReactJS.



**Desarrollador Back End**

Este es responsable de todas las tecnologías del lado del servidor tal como base de datos y aplicaciones creadas con PHP o C#(.NET).
Aquí el diseño no es prioridad, lo que es prioridad es la seguridad, siempre la deben tener muy presente.
También deben escribir código de manera astuta para optimizar tiempos en respuesta, por ejemplo ellos crean los web services, pero los deben de hacer tal forma que te puedan entregar un registro de millones de una base de datos en tiempo record o al menos a eso le apuntan.

La herramientas con las que trabajan dependerán del ambiente en el cual se les pida por ejemplo, aquí en la empresa se usa ambiente Windows por lo cual tienen que trabajar con las herramientas adecuadas: SQL server para base de datos, algún framework como .NET que usa el lenguaje C#.

También deben ser capaces de configurar cualquier herramienta que se requiera.

En el caso de web mapping tendrá que instalar la base POSTGRESQL con su extensión POSTGIS, tendrá que hacer las respectivas configuraciones para enlazarlo con el servidor de mapas GeoServer, tendrá que configurar de igual forma el GeoServer y también se tendría que encargar de que los servicios de GeoServer salgan por un canal seguro y solo se les pueda servir a ciertos usuarios.



**Especialista en SIG**

Bueno aquí ustedes ya sabrán todo lo que implica, deben ser capaces de realizar consultas complejas en el lenguaje SQL para datos espaciales, tienen que tener conocimientos en un alto nivel de todo lo que es el web mapping.
Supongo que deben saber interpretar los datos para determinar ciertas situaciones.

Dominar algún software como QGIS o ArcMap?? y lo más importante para mí, hacer capas que realmente muestren algo valioso para el usuario o aquel que analizara que hacer con esa información.




------------------------------------------------------------------------------------------------------


### COSITAS

**Ejemplo del código HTML de la pagina más simple posible:**


```html
<html>

  <head>
    <title>Título de la página</title>
  </head>

  <body>
    Este es el cuerpo de la página, aquí iría todo el contenido que se desea mostrar.
  </body>

</html>
```

Para ver esto es un navegador es tan fácil como, copiar el código, abrir Bloc de notas, pegarlo en un documento en blanco, guardarlo y poner un nombre como : ejemplo.html

Al abrir este nuevo archivo con doble clic, se abrirá en tu navegador web por defecto.


**JSON**

JavaScript Object Notation por sus siglas en inglés, es un tipo de formato para el intercambio de datos entre cliente-servidor.

https://www.w3schools.com/Js/js_json_intro.asp



**Rest API'S**

![Apis!](http://media2.govtech.com/images/940*603/api_infographic_smartfile_crop.jpg)

[Más...](http://www.govtech.com/applications/Whats-an-API-and-Why-Do-You-Need-One.html)



### ¿Y el XAMPP y el Tomcat? :'(

El XAMPP solo era para montar un entorno de desarrollo Apache en su computadora sin la necesidad de un servidor.
Tomcat es un servidor de aplicaciones basadas en Java, en el montamos GeoServer para emular que está instalado en un servidor web, en la práctica todo eso se configura de manera diferente.



## Parte 2

...


