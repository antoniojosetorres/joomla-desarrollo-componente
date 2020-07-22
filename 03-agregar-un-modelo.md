## 03. Añadir un modelo a Hello World
* Crear la carpeta `models` en `site/models/`.
* Crear el fichero `index.html` en `site/models/index.html`:
````html
	<html><body bgcolor='#fff'></body></html>
````
* Crear el fichero `helloworld.php` en `site/models/helloworld.php`:
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
		<!-- Note the folder attribute: This attribute describes the folder
			to copy FROM in the package to install therefore files copied
			in this section are copied from /site/ in the package -->
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

### Total 18 ficheros:
````
* helloworld.xml
* site/index.html
* site/controller.php
* site/helloworld.php
* site/models/index.html   (nuevo)
* site/models/helloworld.php   (nuevo)
* site/views/index.html
* site/views/helloworld/index.html
* site/views/helloworld/view.html.php
* site/views/helloworld/tmpl/index.html
* site/views/helloworld/tmpl/default.php
* site/views/helloworld/tmpl/default.xml
* admin/index.html
* admin/helloworld.php
* admin/sql/index.html
* admin/sql/updates/index.html
* admin/sql/updates/mysql/index.html
* admin/sql/updates/mysql/0.0.1.sql
````
