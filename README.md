# Joomla: Desarrollo de un componente MVC
Basado en https://docs.joomla.org/J3.x:Developing_an_MVC_Component/es

## 00. Inicializar los ficheros
* Crear el fichero `helloworld.xml`, que indica como instalar el componente `com_helloworld` en Joomla:
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
		<!-- Note the folder attribute: This attribute describes the folder to copy FROM in the package to install therefore files copied in this section are copied from /site/ in the package -->
		<files folder="site">
			<filename>index.html</filename>
			<filename>helloworld.php</filename>
		</files>

		<administration>
			<!-- Administration Menu Section -->
			<menu link='index.php?option=com_helloworld'>Hello World!</menu>
			<!-- Administration Main File Copy Section -->
			<!-- Note the folder attribute: This attribute describes the folder to copy FROM in the package to install therefore files copied in this section are copied from /admin/ in the package -->
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
* Crear la carpeta `site` en `site/` y el fichero `index.html` en `site/index.html`, que impide que se vea el contenido de la carpeta `site`:
````html
	<html><body bgcolor="#ffffff"></body></html>
````
* Crear el fichero `helloworld.php` en `site/helloworld.php`, que indica el punto de entrada del componente `com_helloworld` en el sitio:
````php
	Hello World
````
* Crear la carpeta `admin` en `admin/` y el fichero `index.html` en `admin/index.html`, que impide que se vea el contenido de la carpeta `admin`:
````html
	<html><body bgcolor="#ffffff"></body></html>
````
* Crear el fichero `helloworld.php` en `admin/helloworld.php`, que indica el punto de entrada del componente `com_helloworld` en el administrador:
````php
	Hello World Administration
````
* Crear la carpeta `sql` en `admin/sql/` y el fichero `index.html` en `admin/sql/index.html`, que impide que se vea el contenido de la carpeta `sql`:
````html
	<html><body bgcolor="#ffffff"></body></html>
````
* Crear la carpeta `updates` en `admin/sql/updates/` y el fichero `index.html` en `admin/sql/updates/index.html`, que impide que se vea el contenido de la carpeta `updates`:
````html
	<html><body bgcolor="#ffffff"></body></html>
````
* Crear la carpeta `mysql` en `admin/sql/updates/mysql/` y el fichero `index.html` en `admin/sql/updates/mysql/index.html`, que impide que se vea el contenido de la carpeta `mysql`:
````html
	<html><body bgcolor="#ffffff"></body></html>
````
* Crear el fichero `0.0.1.sql` en `admin/sql/updates/mysql/0.0.1.sql`, que permite inicializar el esquema de versiones del componente `com_helloworld`:
````

````
### Total 9 ficheros:
01. helloworld.xml
02. site/index.html
03. site/helloworld.php
04. admin/index.html
05. admin/helloworld.php
06. admin/sql/index.html
07. admin/sql/updates/index.html
08. admin/sql/updates/mysql/index.html
09. admin/sql/updates/mysql/0.0.1.sql

## 01. Añadir una vista
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
* Crear el fichero `controller.php` en `site/controller.php`, que representa al controlador `HelloWorld`:
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
* Crear la carpeta `views` en `site/views/` y el fichero `index.html` en `site/views/index.html`, que impide que se vea el contenido de la carpeta `views`:
````html
	<html><body bgcolor='#fff'></body></html>
````
* Crear la carpeta `helloworld` en `site/views/helloworld/` y el fichero `index.html` en `site/views/helloworld/index.html`, que impide que se vea el contenido de la carpeta `helloworld`:
````html
	<html><body bgcolor='#fff'></body></html>
````
* Crear el fichero `view.html.php` en `site/views/helloworld/view.html.php`, que representa la vista `HelloWorld`:
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
* Crear la carpeta `tmpl` en `site/views/helloworld/tmpl/` y el fichero `index.html` en `site/views/helloworld/tmpl/index.html`, que impide que se vea el contenido de la carpeta `tmpl`:
````html
	<html><body bgcolor='#fff'></body></html>
````
* Crear el fichero `default.php`en `site/views/helloworld/tmpl/default.php`, que representa la vista predeterminada:
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
		<!-- Note the folder attribute: This attribute describes the folder to copy FROM in the package to install therefore files copied in this section are copied from /site/ in the package -->
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
			<!-- Note the folder attribute: This attribute describes the folder to copy FROM in the package to install therefore files copied in this section are copied from /admin/ in the package -->
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
01. helloworld.xml
02. site/index.html
03. _site/controller.php_   (nuevo)
04. site/helloworld.php
05. _site/views/index.html_   (nuevo)
06. _site/views/helloworld/index.html_   (nuevo)
07. _site/views/helloworld/view.html.php_   (nuevo)
08. _site/views/helloworld/tmpl/index.html_   (nuevo)
09. _site/views/helloworld/tmpl/default.php_   (nuevo)
10. admin/index.html
11. admin/helloworld.php
12. admin/sql/index.html
13. admin/sql/updates/index.html
14. admin/sql/updates/mysql/index.html
15. admin/sql/updates/mysql/0.0.1.sql

## 02. Añadir un elemento de menu
* Crear el fichero `default.xml` en `site/views/helloworld/tmpl/default.xml`, que añade el elemento de menu predeterminado:  
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
		<!-- Note the folder attribute: This attribute describes the folder to copy FROM in the package to install therefore files copied in this section are copied from /site/ in the package -->
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
			<!-- Note the folder attribute: This attribute describes the folder to copy FROM in the package to install therefore files copied in this section are copied from /admin/ in the package -->
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
01. helloworld.xml
02. site/index.html
03. site/controller.php
04. site/helloworld.php
05. site/views/index.html
06. site/views/helloworld/index.html
07. site/views/helloworld/view.html.php
08. site/views/helloworld/tmpl/index.html
09. site/views/helloworld/tmpl/default.php
10. _site/views/helloworld/tmpl/default.xml_   (nuevo)
11. admin/index.html
12. admin/helloworld.php
13. admin/sql/index.html
14. admin/sql/updates/index.html
15. admin/sql/updates/mysql/index.html
16. admin/sql/updates/mysql/0.0.1.sql

## 03. Añadir un modelo
* Crear la carpeta `models` en `site/models/` y el fichero `index.html` en `site/models/index.html`, que impide que se vea el contenido de la carpeta `models`:
````html
	<html><body bgcolor='#fff'></body></html>
````
* Crear el fichero `helloworld.php` en `site/models/helloworld.php`, que representa el modelo `HelloWorld`:
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
 	 * HelloWorld Model
 	 *
 	 * @since  0.0.1
 	 */
	class HelloWorldModelHelloWorld extends JModelItem
	{
		/**
	 	 * @var string message
	 	 */
		protected $message;

		/**
	 	 * Get the message
		 *
	 	 * @return  string  The message to be displayed to the user
	 	 */
		public function getMsg()
		{
			if (!isset($this->message))
			{
				$this->message = 'Hello World!';
			}

			return $this->message;
		}
	}
````
* Actualizar el fichero `view.html.php` en `site/views/helloworld/view.html.php`:
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
````
````php
			$this->msg = $this->get('Msg');

			// Check for errors.
			if (count($errors = $this->get('Errors')))
			{
				JLog::add(implode('<br />', $errors), JLog::WARNING, 'jerror');

				return false;
			}
````
````php
			// Display the view
			parent::display($tpl);
		}
	}
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
		<!--  The version string is recorded in the components table -->
````
````xml
		<version>0.0.4</version>
````
````xml
		<!-- The description is optional and defaults to the name -->
		<description>Description of the Hello World component ...</description>

		<update> <!-- Runs on update; New since J2.5 -->
			<schemas>
				<schemapath type="mysql">sql/updates/mysql</schemapath>
			</schemas>
		</update>

		<!-- Site Main File Copy Section -->
		<!-- Note the folder attribute: This attribute describes the folder to copy FROM in the package to install therefore files copied in this section are copied from /site/ in the package -->
		<files folder="site">
			<filename>index.html</filename>
			<filename>helloworld.php</filename>
			<filename>controller.php</filename>
			<folder>views</folder>
````
````xml
			<folder>models</folder>
````
````xml
		</files>

		<administration>
			<!-- Administration Menu Section -->
			<menu link='index.php?option=com_helloworld'>Hello World!</menu>
			<!-- Administration Main File Copy Section -->
			<!-- Note the folder attribute: This attribute describes the folder to copy FROM in the package to install therefore files copied in this section are copied from /admin/ in the package -->
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
### Total 18 ficheros:
01. helloworld.xml
02. site/index.html
03. site/controller.php
04. site/helloworld.php
05. _site/models/index.html_   (nuevo)
06. _site/models/helloworld.php_   (nuevo)
07. site/views/index.html
08. site/views/helloworld/index.html
09. site/views/helloworld/view.html.php
10. site/views/helloworld/tmpl/index.html
11. site/views/helloworld/tmpl/default.php
12. site/views/helloworld/tmpl/default.xml
13. admin/index.html
14. admin/helloworld.php
15. admin/sql/index.html
16. admin/sql/updates/index.html
17. admin/sql/updates/mysql/index.html
18. admin/sql/updates/mysql/0.0.1.sql

## 04. Añadir una variable de peticion en el tipo de menu
* Actualizar el fichero `default.xml` en `site/views/helloworld/tmpl/default.xml`:
````xml
	<?xml version="1.0" encoding="utf-8"?>
	<metadata>
		<layout title="COM_HELLOWORLD_HELLOWORLD_VIEW_DEFAULT_TITLE">
			<message>COM_HELLOWORLD_HELLOWORLD_VIEW_DEFAULT_DESC</message>
		</layout>
````
````xml
		<fields name="request">
			<fieldset name="request">
				<field name="id" type="list" label="COM_HELLOWORLD_HELLOWORLD_FIELD_GREETING_LABEL" description="COM_HELLOWORLD_HELLOWORLD_FIELD_GREETING_DESC" default="1">
					<option value="1">Hello World!</option>
                    <option value="2">Good bye World!</option>
				</field>
			</fieldset>
		</fields>
	</metadata>
````




