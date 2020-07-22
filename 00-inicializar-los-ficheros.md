## 00. Inicializar los ficheros
* Crear el fichero `helloworld.xml` en `/`, que indica como instalar el componente en Joomla:
````xml
	<?xml version="1.0" encoding="utf-8"?>
	<extension type="component" version="3.0" method="upgrade">

		<name>Hello World!</name>
		<!-- The following elements are optional and free of formatting constraints -->
		<creationDate>January 2018</creationDate>
		<author>John Doe</author>
		<authorEmail>john.doe@example.org</authorEmail>
		<authorUrl>http://www.example.org</authorUrl>
		<copyright>Copyright Info</copyright>
		<license>License Info</license>
		<!-- The version string is recorded in the components table -->
		<version>0.0.1</version>
		<!-- The description is optional and defaults to the name -->
		<description>Description of the Hello World component</description>

		<update> <!-- Runs on update -->
			<schemas>
				<schemapath type="mysql">sql/updates/mysql</schemapath>
			</schemas>
		</update>

		<!-- Site Main File Copy Section -->
		<!-- Note the folder attribute: This attribute describes the folder
			to copy FROM in the package to install therefore files copied
			in this section are copied from /site/ in the package -->
		<files folder="site">
			<filename>index.html</filename>
			<filename>helloworld.php</filename>
		</files>

		<administration>
			<!-- Administration Menu Section -->
			<menu link='index.php?option=com_helloworld'>Hello World!</menu>
			<!-- Administration Main File Copy Section -->
			<!-- Note the folder attribute: This attribute describes the folder
				to copy FROM in the package to install therefore files copied
				in this section are copied from /admin/ in the package -->
			<files folder="admin">
				<!-- Admin Main File Copy Section -->
				<filename>index.html</filename>
				<filename>helloworld.php</filename>
				<!-- SQL files section -->
				<folder>sql</folder>
			</files>
		</administration>

	</extension>
````
* Crear la carpeta `site` en `site/`.
* Crear el fichero `index.html` en `site/index.html`:
````html
	<html><body bgcolor="#ffffff"></body></html>
````
* Crear el fichero `helloworld.php` en `site/helloworld.php`, que indica el punto de entrada del componente en el sitio:
````php
	Hello World
````
* Crear la carpeta `admin` en `admin/`.
* Crear el fichero `index.html` en `admin/index.html`, que evita que se vea el contenido de la carpeta:
````html
	<html><body bgcolor="#ffffff"></body></html>
````
* Crear el fichero `helloworld.php` en `admin/helloworld.php`, que indica el punto de entrada del componente en el administrador:
````php
	Hello World Administration
````
* Crear la carpeta `sql` en `admin/sql/`.
* Crear el fichero `index.html` en `admin/sql/index.html`:
````html
	<html><body bgcolor="#ffffff"></body></html>
````
* Crear la carpeta `updates` en `admin/sql/updates/`.
* Crear el fichero `index.html` en `admin/sql/updates/index.html`:
````html
	<html><body bgcolor="#ffffff"></body></html>
````
* Crear la carpeta `mysql` en `admin/sql/updates/mysql/`.
* Crear el fichero `index.html` en `admin/sql/updates/mysql/index.html`.
````html
	<html><body bgcolor="#ffffff"></body></html>
````
* Crear el fichero `0.0.1.sql` en `admin/sql/updates/mysql/0.0.1.sql`, que permite inicializar el esquema de versiones del componente:
````

````

### Total 9 ficheros:
````
* helloworld.xml
* site/index.html
* site/helloworld.php
* admin/index.html
* admin/helloworld.php
* admin/sql/index.html
* admin/sql/updates/index.html
* admin/sql/updates/mysql/index.html
* admin/sql/updates/mysql/0.0.1.sql
````
