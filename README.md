# Joomla: Desarrollo de un componente MVC
Basado en https://docs.joomla.org/J3.x:Developing_an_MVC_Component/es

## Menu
[00. Inicializar los ficheros](README.md#00-inicializar-los-ficheros)  
[01. Añadir una vista](README.md#01-añadir-una-vista)  
[02. Añadir un elemento de menu](README.md#02-añadir-un-elemento-de-menu)  
[03. Añadir un modelo](README.md#03-añadir-un-modelo)  
[04. Añadir una variable de peticion en el tipo de menu](README.md#04-añadir-una-variable-de-peticion-en-el-tipo-de-menu)  
[05. Utilizando la base de datos](README.md#05-utilizando-la-base-de-datos)  

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
1. helloworld.xml
2. admin/index.html
3. admin/helloworld.php
4. admin/sql/index.html
5. admin/sql/updates/index.html
6. admin/sql/updates/mysql/index.html
7. admin/sql/updates/mysql/0.0.1.sql
8. site/index.html
9. site/helloworld.php
---
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
1. helloworld.xml
2. admin/index.html
3. admin/helloworld.php
4. admin/sql/index.html
5. admin/sql/updates/index.html
6. admin/sql/updates/mysql/index.html
7. admin/sql/updates/mysql/0.0.1.sql
8. site/index.html
9. ***site/controller.php***
10. site/helloworld.php
11. ***site/views/index.html***
12. ***site/views/helloworld/index.html***
13. ***site/views/helloworld/view.html.php***
14. ***site/views/helloworld/tmpl/index.html***
15. ***site/views/helloworld/tmpl/default.php***
---
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
1. helloworld.xml
2. admin/index.html
3. admin/helloworld.php
4. admin/sql/index.html
5. admin/sql/updates/index.html
6. admin/sql/updates/mysql/index.html
7. admin/sql/updates/mysql/0.0.1.sql
8. site/index.html
9. site/controller.php
10. site/helloworld.php
11. site/views/index.html
12. site/views/helloworld/index.html
13. site/views/helloworld/view.html.php
14. site/views/helloworld/tmpl/index.html
15. site/views/helloworld/tmpl/default.php
16. ***site/views/helloworld/tmpl/default.xml***
---
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
		<description>Description of the Hello World component</description>

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
1. helloworld.xml
2. admin/index.html
3. admin/helloworld.php
4. admin/sql/index.html
5. admin/sql/updates/index.html
6. admin/sql/updates/mysql/index.html
7. admin/sql/updates/mysql/0.0.1.sql
8. site/index.html
9. site/controller.php
10. site/helloworld.php
11. ***site/models/index.html***
12. ***site/models/helloworld.php***
13. site/views/index.html
14. site/views/helloworld/index.html
15. site/views/helloworld/view.html.php
16. site/views/helloworld/tmpl/index.html
17. site/views/helloworld/tmpl/default.php
18. site/views/helloworld/tmpl/default.xml
---
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
````
````xml
	</metadata>
````
* Actualizar el fichero `helloworld.php` en `site/models/helloworld.php`:
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
	 	 * @return  string  The message to be displayed to the user
	 	 */
		public function getMsg()
		{
			if (!isset($this->message))
			{
````
````php
				$jinput = JFactory::getApplication()->input;
				$id     = $jinput->get('id', 1, 'INT');

				switch ($id)
				{
					case 2:
						$this->message = 'Good bye World!';
						break;
					default:
					case 1:
						$this->message = 'Hello World!';
						break;
				}
````
````php
			}
			return $this->message;
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
		<!-- The version string is recorded in the components table -->
````
````xml
		<version>0.0.5</version>
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
			<folder>models</folder>
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
1. helloworld.xml
2. admin/index.html
3. admin/helloworld.php
4. admin/sql/index.html
5. admin/sql/updates/index.html
6. admin/sql/updates/mysql/index.html
7. admin/sql/updates/mysql/0.0.1.sql
8. site/index.html
9. site/controller.php
10. site/helloworld.php
11. site/models/index.html
12. site/models/helloworld.php
13. site/views/index.html
14. site/views/helloworld/index.html
15. site/views/helloworld/view.html.php
16. site/views/helloworld/tmpl/index.html
17. site/views/helloworld/tmpl/default.php
18. site/views/helloworld/tmpl/default.xml
---
## 05. Utilizando la base de datos
* Crear el fichero `install.mysql.utf8.sql` en `admin/sql/install.mysql.utf8.sql`, que se ejecuta cuando se realiza la instalacion del componente `helloworld`:
````sql
	DROP TABLE IF EXISTS `#__helloworld`;

	CREATE TABLE `#__helloworld` (
		`id`		INT(11)		NOT NULL AUTO_INCREMENT,
		`title`		VARCHAR(25)	NOT NULL,
		`published`	TINYINT(4)	NOT NULL DEFAULT '1',
		PRIMARY KEY (`id`)
	) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 DEFAULT COLLATE=utf8mb4_unicode_ci;

	INSERT INTO `#__helloworld` (`greeting`) VALUES ('Hello World!'), ('Good bye World!');
````
* Crear el fichero `0.0.6.sql` en `admin/sql/updates/mysql/0.0.6.sql`, que se ejecuta cuando se realiza la actualizacion del componente `helloworld` con el contenido anterior.
* Crear el archivo `uninstall.mysql.utf8.sql` en `admin/sql/uninstall.mysql.utf8.sql`, que se ejecuta cuando se realiza la desinstalacion del componente `helloworld`:
````sql
	DROP TABLE IF EXISTS `#__helloworld`;
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
		<version>0.0.6</version>
````
````xml
		<!-- The description is optional and defaults to the name -->
		<description>Description of the Hello World component</description>
````
````xml
		<install> <!-- Runs on install -->
			<sql>
				<file driver="mysql" charset="utf8">sql/install.mysql.utf8.sql</file>
			</sql>
		</install>
		<uninstall> <!-- Runs on uninstall -->
			<sql>
				<file driver="mysql" charset="utf8">sql/uninstall.mysql.utf8.sql</file>
			</sql>
		</uninstall>
````
````xml
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
			<folder>models</folder>
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
````
````xml
				<!-- tables files section -->
				<folder>tables</folder>
				<!-- models files section -->
				<folder>models</folder>
````
````xml
			</files>
		</administration>

	</extension>
````
* Actualizar el fichero `default.xml` en `site/views/helloworld/tmpl/default.xml`:
````xml
	<?xml version="1.0" encoding="utf-8"?>
	<metadata>
		<layout title="COM_HELLOWORLD_HELLOWORLD_VIEW_DEFAULT_TITLE">
			<message>COM_HELLOWORLD_HELLOWORLD_VIEW_DEFAULT_DESC</message>
		</layout>
````
````xml
		<fields name="request" addfieldpath="/administrator/components/com_helloworld/models/fields">
			<fieldset name="request">
				<field name="id" type="helloworld" label="COM_HELLOWORLD_HELLOWORLD_FIELD_GREETING_LABEL" description="COM_HELLOWORLD_HELLOWORLD_FIELD_GREETING_DESC" />
			</fieldset>
````			
````xml			
		</fields>
	</metadata>
````
* Crear la carpeta `models` en `admin/models/`y el fichero `index.html` en `admin/models/index.html`, que impide que se vea el contenido de la carpeta `models`:
````html
	<html><body bgcolor='#fff'></body></html>
````
* Crear la carpeta `fields`en `admin/models/fields/` y el fichero `index.html` en `admin/models/fields/index.html`, que impide que se vea la carpeta `fields`:
````html
	<html><body bgcolor='#fff'></body></html>
````
* Crear el fichero `helloworld.php` en `admin/models/fields/helloworld.php`:
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

	JFormHelper::loadFieldClass('list');

	/**
 	 * HelloWorld Form Field class for the HelloWorld component
 	 *
 	 * @since  0.0.1
 	 */
	class JFormFieldHelloWorld extends JFormFieldList
	{
		/**
	 	 * The field type.
	 	 *
	 	 * @var         string
	 	 */
		protected $type = 'HelloWorld';

		/**
	 	 * Method to get a list of options for a list input.
	 	 *
	 	 * @return  array  An array of JHtml options.
	 	 */
		protected function getOptions()
		{
			$db    = JFactory::getDBO();
			$query = $db->getQuery(true);
			$query->select('id,title');
			$query->from('#__helloworld');
			$db->setQuery((string) $query);
			$messages = $db->loadObjectList();
			$options  = array();

			if ($messages)
			{
				foreach ($messages as $message)
				{
					$options[] = JHtml::_('select.option', $message->id, $message->title);
				}
			}

			$options = array_merge(parent::getOptions(), $options);

			return $options;
		}
	}
````
* Actualizar el fichero `helloworld.php` en `site/models/helloworld.php`:
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
````
````php
		/**
	 	 * @var array messages
	 	 */
		protected $messages;

		/**
	 	 * Method to get a table object, load it if necessary.
	 	 *
	 	 * @param   string  $type    The table name. Optional.
	 	 * @param   string  $prefix  The class prefix. Optional.
	 	 * @param   array   $config  Configuration array for model. Optional.
	 	 *
	 	 * @return  JTable  A JTable object
	 	 *
	 	 * @since   1.6
	 	 */
		public function getTable($type = 'HelloWorld', $prefix = 'HelloWorldTable', $config = array())
		{
			return JTable::getInstance($type, $prefix, $config);
		}

		/**
	 	 * Get the message
	 	 *
	 	 * @param   integer  $id  Greeting Id
	 	 *
	 	 * @return  string        Fetched String from Table for relevant Id
	 	 */
		public function getMsg($id = 1)
		{
			if (!is_array($this->messages))
			{
				$this->messages = array();
			}

			if (!isset($this->messages[$id]))
			{
				// Request the selected id
				$jinput = JFactory::getApplication()->input;
				$id     = $jinput->get('id', 1, 'INT');

				// Get a TableHelloWorld instance
				$table = $this->getTable();

				// Load the message
				$table->load($id);

				// Assign the message
				$this->messages[$id] = $table->greeting;
			}

			return $this->messages[$id];
````
````php
		}
	}
````
* Crear la carpeta `tables` en `admin/tables/`y el fichero `index.html` en `admin/tables/index.html`, que impide que se vea el contenido de la carpeta `tables`:
````html
	<html><body bgcolor='#fff'></body></html>
````
* Crear el fichero `helloworld.php` en `admin/tables/helloworld.php`:
````php
	<?php
	/**
 	 * @package     Joomla.Administrator
 	 * @subpackage  com_helloworld
 	 *
 	 * @copyright   Copyright (C) 2005 - 2018 Open Source Matters, Inc. All rights reserved.
 	 * @license     GNU General Public License version 2 or later; see LICENSE.txt
 	 */

	// No direct access
	defined('_JEXEC') or die('Restricted access');

	/**
 	 * Hello Table class
 	 *
 	 * @since  0.0.1
 	 */
	class HelloWorldTableHelloWorld extends JTable
	{
		/**
	 	 * Constructor
	 	 *
	 	 * @param   JDatabaseDriver  &$db  A database connector object
	 	 */
		function __construct(&$db)
		{
			parent::__construct('#__helloworld', 'id', $db);
		}
	}
````
### Total 26 ficheros:
1. helloworld.xml
2. admin/index.html
3. admin/helloworld.php
4. ***admin/models/index.html***
5. ***admin/models/fields/index.html***
6. ***admin/models/fields/helloworld.php***
7. admin/sql/index.html
8. admin/sql/updates/index.html
9. ***admin/sql/install.mysql.utf8.sql***
10. ***admin/sql/uninstall.mysql.utf8.sql***
11. admin/sql/updates/mysql/index.html
12. admin/sql/updates/mysql/0.0.1.sql
13. ***admin/sql/updates/mysql/0.0.6.sql***
14. ***admin/tables/index.html***
15. ***admin/tables/helloworld.php***
16. site/index.html
17. site/controller.php
18. site/helloworld.php
19. site/models/index.html
20. site/models/helloworld.php
21. site/views/index.html
22. site/views/helloworld/index.html
23. site/views/helloworld/view.html.php
24. site/views/helloworld/tmpl/index.html
25. site/views/helloworld/tmpl/default.php
26. site/views/helloworld/tmpl/default.xml
---
## 06.





