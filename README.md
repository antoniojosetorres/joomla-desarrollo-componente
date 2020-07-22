# Joomla: Desarrollo de un componente MVC
Basado en https://docs.joomla.org/J3.x:Developing_an_MVC_Component/es

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
* Crear la carpeta `site` en `site/` y el fichero `index.html` en `site/index.html`, que evita que se vea el contenido de la carpeta:
````html
	<html><body bgcolor="#ffffff"></body></html>
````
* Crear el fichero `helloworld.php` en `site/helloworld.php`, que indica el punto de entrada del componente en el sitio:
````php
	Hello World
````
* Crear la carpeta `admin` en `admin/` y el fichero `index.html` en `admin/index.html`:
````html
	<html><body bgcolor="#ffffff"></body></html>
````
* Crear el fichero `helloworld.php` en `admin/helloworld.php`, que indica el punto de entrada del componente en el administrador:
````php
	Hello World Administration
````
* Crear la carpeta `sql` en `admin/sql/` y el fichero `index.html` en `admin/sql/index.html`:
````html
	<html><body bgcolor="#ffffff"></body></html>
````
* Crear la carpeta `updates` en `admin/sql/updates/` y el fichero `index.html` en `admin/sql/updates/index.html`:
````html
	<html><body bgcolor="#ffffff"></body></html>
````
* Crear la carpeta `mysql` en `admin/sql/updates/mysql/` y el fichero `index.html` en `admin/sql/updates/mysql/index.html`.
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

## 01. Añadir una vista a Hello World
* Actualizar el fichero `helloworld.php` en `site/helloworld.php`:  
````php
	<?php
	/**
 	 * @package     Joomla.Administrator
 	 * @subpackage  com_helloworld
 	 *
 	 * @copyright   Copyright (C) 2005 - 2018 Open Source Matters, Inc. All rights reserved.
 	 * @license     GNU General Public License version 2 or later; see LICENSE.txt
 	 */

	// No direct access to this file
	defined('_JEXEC') or die('Restricted access');

	// Get an instance of the controller prefixed by HelloWorld
	$controller = JControllerLegacy::getInstance('HelloWorld');

	// Perform the Request task
	$input = JFactory::getApplication()->input;
	$controller->execute($input->getCmd('task'));

	// Redirect if set by the controller
	$controller->redirect();
````
* Crear el fichero `controller.php` en `site/controller.php`:
````php
	<?php
	/**
 	 * @package     Joomla.Administrator
 	 * @subpackage  com_helloworld
 	 *
 	 * @copyright   Copyright (C) 2005 - 2018 Open Source Matters, Inc. All rights reserved.
 	 * @license     GNU General Public License version 2 or later; see LICENSE.txt
 	 */

	// No direct access to this file
	defined('_JEXEC') or die('Restricted access');

	/**
 	 * Hello World Component Controller
 	 *
 	 * @since  0.0.1
 	 */
	class HelloWorldController extends JControllerLegacy
	{
	}
````
* Crear la carpeta `views` en `site/views/` y el fichero `index.html` en `site/views/index.html`:
````html
	<html><body bgcolor='#fff'></body></html>
````
* Crear la carpeta `helloworld` en `site/views/helloworld/` y el fichero `index.html` en `site/views/helloworld/index.html`:
````html
	<html><body bgcolor='#fff'></body></html>
````
* Crear el fichero `view.html.php` en `site/views/helloworld/view.html.php`:
````php
	<?php
	/**
 	 * @package     Joomla.Administrator
 	 * @subpackage  com_helloworld
 	 *
 	 * @copyright   Copyright (C) 2005 - 2018 Open Source Matters, Inc. All rights reserved.
 	 * @license     GNU General Public License version 2 or later; see LICENSE.txt
 	 */

	// No direct access to this file
	defined('_JEXEC') or die('Restricted access');

	/**
 	 * HTML View class for the HelloWorld Component
 	 *
 	 * @since  0.0.1
 	 */
	class HelloWorldViewHelloWorld extends JViewLegacy
	{
		/**
	 	 * Display the Hello World view
	 	 *
	 	 * @param   string  $tpl  The name of the template file to parse; automatically searches through the template paths.
	 	 *
	 	 * @return  void
	 	 */
		function display($tpl = null)
		{
			// Assign data to the view
			$this->msg = 'Hello World';

			// Display the view
			parent::display($tpl);
		}
	}
````
* Crear la carpeta `tmpl` en `site/views/helloworld/tmpl/` y el fichero `index.html` en `site/views/helloworld/tmpl/index.html`:
````html
	<html><body bgcolor='#fff'></body></html>
````
* Crear el fichero `default.php`en `site/views/helloworld/tmpl/default.php`:
````php
	<?php
	/**
 	 * @package     Joomla.Administrator
 	 * @subpackage  com_helloworld
 	 *
 	 * @copyright   Copyright (C) 2005 - 2018 Open Source Matters, Inc. All rights reserved.
 	 * @license     GNU General Public License version 2 or later; see LICENSE.txt
 	 */
 
	// No direct access to this file
	defined('_JEXEC') or die('Restricted access');
	?>

	<h1><?php echo $this->msg; ?></h1>
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
		<version>0.0.2</version>
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
````
````xml
			<filename>controller.php</filename>
			<folder>views</folder>
````
````xml
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

### Total 15 ficheros:
````
* helloworld.xml
* site/index.html
* site/controller.php   (nuevo)
* site/helloworld.php
* site/views/index.html   (nuevo)
* site/views/helloworld/index.html   (nuevo)
* site/views/helloworld/view.html.php   (nuevo)
* site/views/helloworld/tmpl/index.html   (nuevo)
* site/views/helloworld/tmpl/default.php   (nuevo)
* admin/index.html
* admin/helloworld.php
* admin/sql/index.html
* admin/sql/updates/index.html
* admin/sql/updates/mysql/index.html
* admin/sql/updates/mysql/0.0.1.sql
````

