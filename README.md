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


## SERVIDOR

En la empresa se cuenta con servidores IIS de Windows los cuales son muy ventajosos al momento de montar e instalar
las aplicaciones, o base de datos, ya que todo se hace mediante interfaz gráfica.








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
