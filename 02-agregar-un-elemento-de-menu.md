## 02. Añadir un elemento de menu a Hello World
* Crear el fichero `default.xml` en `site/views/helloworld/tmpl/default.xml`:  
````xml
	<?xml version="1.0" encoding="utf-8"?>
	<metadata>
		<layout title="COM_HELLOWORLD_HELLOWORLD_VIEW_DEFAULT_TITLE">
			<message>COM_HELLOWORLD_HELLOWORLD_VIEW_DEFAULT_DESC</message>
		</layout>
	</metadata>
````
* Actualizar el fichero `helloworld.xml`:  
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
````
````xml
		<version>0.0.3</version>
````
````xml
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
			<filename>controller.php</filename>
			<folder>views</folder>
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

### Total 16 ficheros:
````
* helloworld.xml
* site/index.html
* site/controller.php
* site/helloworld.php
* site/views/index.html
* site/views/helloworld/index.html
* site/views/helloworld/view.html.php
* site/views/helloworld/tmpl/index.html
* site/views/helloworld/tmpl/default.php
* site/views/helloworld/tmpl/default.xml   (nuevo)
* admin/index.html
* admin/helloworld.php
* admin/sql/index.html
* admin/sql/updates/index.html
* admin/sql/updates/mysql/index.html
* admin/sql/updates/mysql/0.0.1.sql
````
