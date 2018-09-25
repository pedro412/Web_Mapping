## ARQUITECTURA DE PROYECTO WEB MAPPING

Estos son los requerimientos mínimos necesarios para montar una infraestructura de web mapping.
	
Se dividirá en dos bloques FRONTEND y BACKEND


BACKEND(servidor)

	- Servidor web: Apache o IIS.
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



### WEB MAP SERVICES
Para entender esto se debe primero entender que son los servicios web, los servicios web son funciones creadas en algún lenguaje de programación que tenga capacidades de interactuar con una base de datos para hacer consultas a la misma, manipular archivos, en otras palabras en un lenguaje del lado del servidor, los lenguajes más comunes para web: PHP, NodeJS, Python, C#(.NET) y Java(no confundir Java con JavaScript ya que son dos cosas diferentes).
Estas funciones realizan tareas específicas, tal como sumar dos números hasta devolver todos los registros de una base de datos.
Se les llama servicios web porque en teoría todo lo que tienes que hacer para invocarlos es usar una URL que se asignó a dicha función o servicio.

Por ejemplo: se requiere consumir un servicio web para sumar dos numeros:

    copias y pegas esto en tu navegador...
    
    http://www.miDominio.com/sumarNumeros?numero1=5&numero2=6 
    
    pasa la magia y esto nos regresa una respuesta en formato XML o JSON, generalmente retornan un JSON.
    
```javascript
    respuesta:[{
	numero1: 5,
	numero2: 6,
	suma: 11 //<-- este es el resultado de la función que se ejecutó en el servidor.
    }]
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

nótese el uso de etiquetas, **div** es el identificador de la etiqueta que definimos, hay varios tipo de etiquetas con sus respectivos nombres *div* es utilizado con frecuencia, las etiquetas siempre abren y se tienen que cerrar, HTML es muy parecido a XML solo que XML es más difícil de leer para los humanos, ya que XML fue creado para comunicación entre software, y HTML fue creado para que los humanos lo puedan leer y entender muy fácil.



**CSS**

Hoja de estilos, tampoco es un lenguaje de programación, es un lenguaje de estilos, usado para definir estilos específicos a las etiquetas HTML usando la etiqueta anterior digamos que queremos cambiar el color de fondo.

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

a diferencia de la primera vez que se declaro, ahora tiene un atributo que se llama "id" y se le dio un valor = cosaUno, y adentro de las etiquetas no hay nada está vacio.

Primero necesitamos agarrar esa etiqueta con JavaScript

```javascript
// javascript

 var cosaUno = document.getElementById('cosaUno');
```

la palabra reservada *var* se usa para declarar variables, todo lo que paso en la instrucción anterior fue que guardamos esa etiqueta HTML en una variable, lista para ser manipulada. *document.getElementById()* es un método de JavaScript para seleccionar etiquetas HTML basado en un id.

después procedemos a cambiar el valor que esa etiqueta tiene, que al momento está vacía.
pero primero necesitamos que el usuario de clic sobre la página.

¿cómo podemos saber cuándo el usuario da clic sobre la página?.

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

ya que la tenemos en memoria, necesitamos agregar un EventListener que rastrea cualquier evento que definamos, en este caso queremos que rastree cuando el usuario da clic sobre la página.

```javascript
//javascript

pagina.addEventListener('click', function(){
	cosaUno.innerHTML = 'Hola';
});
```

entonces cuando se dé clic se tendría lo siguiente:

```html
html

<html id="pagina">
	<div id="cosaUno">Hola<div>
</html>
```

Ahora se debe tener una idea más clara de lo que es una página web, HTML son los huesos con los que se construye, CSS es para darle forma a esa estructura, y JavaScript es para darle funcionalidad a lo que queramos y como lo queramos.



### FRAMEWORKS Y LIBRERIAS DE JAVASCRIPT
Los frameworks  y/o librerías de JavaScript son funciones(echas con JavaScript) gigantes que adentro de ellas vienen muchas funciones pequeñas que sirven para un propósito, en el caso de web mapping, los frameworks tales como Leaflet y OpenLayers son para la manipulación y renderización de mapas y capas en una página web sin tener que partir de cero.

Ejemplo: https://unpkg.com/leaflet@1.3.4/dist/leaflet.js
Todo ese código es la ibrería de Leaflet ahí vienen todas sus funciones que podemos utilizar.



