-------------------------------
QGIS Plugins
-------------------------------
.. _`plugins`:
:index:`plugins`

QGIS has been designed with a plugin architecture.
This allows many new features/functions to be easily added to the application.
Many of the features in QGIS are actually implemented as either **core**
or **external plugins**.

:index:`plugins!types`

*  **Core Plugins** are maintained by the QGIS Development
Team and are automatically part of every QGIS distribution.
They are written in one of two languages: C++ or Python.
More information about core plugins are provided in Section :ref:`core_plugins`

*  **External Plugins** are currently all written in Python.
They are stored in external repositories and maintained by the individual authors.
They can be added to QGIS using the :file:`Python Plugin Installer`.
More information about external plugins are provided in Section :ref:`load_external_plugin`.


Managing Plugins
================

.. _`managing_plugins`:
:index:`plugins!managing`

Managing plugins in general means loading or unloading them using
the :file:`Plugin Manager`. External plugins can be installed and
directly activated or uninstalled using the :file:`Python Plugin Installer`.
To deactivate and reactivate external plugins, the :file:`Plugin Manager` is used again.

Loading a QGIS Core Plugin
***************************
.. _`load_core_plugin`:


Loading a QGIS Core Plugin is done from the main menu :menuselection:`Plugins --> Manage Plugins`

:index:`plugins!manager`

.. figure::img/en/plugins/pluginmanager.png
   :align: center
   :width: 12em


The :file:`Plugin Manager` lists all the available plugins and their
status (loaded or unloaded), including all core plugins and all external
plugins that have been installed and automatically activated using the
:file:`Python Plugin Installer` (see Section :ref:`external_plugins`).
Those plugins that are already loaded have a check mark to the left of
their name. Figure `pluginmanager`_ shows the Plugin Manager dialog.

To enable a particular plugin, click on the checkbox to the left of the
plugin name, and click :guilabel:`OK`. When you exit the application, a list
of loaded plugins is retained, and the next time you run QGIS these
plugins are automatically loaded.

:index:`crashes`

.. note:: 
	**Crashing Plugins**
	
	If you find that QGIS crashes on startup, a plugin may be at fault.
	You can stop all plugins from loading by editing your stored settings file (see :ref:`gui_options` for location). Locate the plugins settings and change all the plugin values to false to prevent them from loading.
	|nix| For example, to prevent the Delimited text plugin from loading, the entry in \$HOME/.config/QuantumGIS/qgis.conf on Linux should look like this: ``Add Delimited Text Layer=false``. 
	
	Do this for each plugin in the [Plugins] section. You can then start QGIS and add the plugins one at a time from the :file:`Plugin Manager to determine which plugin is causing the problem.


Loading an external QGIS Plugin
*******************************
.. _`load_external_plugin`:


External QGIS plugins are written in Python. They are by default stored in either 
the 'Official' or 'User contributed' QGIS Repositories, or in various other external
repositories maintained by individual authors. These lists are available 
automatically from the :file:`Python Plugin installer` via :menuselection:`Fetch Python Plugins`.

Detailed documentation about the usage, minimum QGIS version, homepage, authors,
and other important information are provided with the external plugins themselves
and is not included in this manual [1]_ [2]_. 

Currently (at the time of testing version 1.8 of QGIS) there are over 90 external 
plugins available from thirteen listed repositories. Some of these plugins offer
functionality that will be required by many users (for example : providing the user 
with the ability to view and edit Open Street Map data, or to add Google Map layers)
while others offer very specialised functions (for example : Calculate economic pipe diameters
for water supply networks).

It is, however, quite straightforward to search through all the available external plugins
by providing keywords, choosing a named repository and/or filtering on the status of plugins 
(currently installed or uninstalled in your system). Searching and filtering is done from the 
QGIS Plugin Manager (see Figure `plugininstaller`_).

.. note:: 
	**Add more repositories**
	
	To add the 'User contributed' repository and/or several external author repositories, open the
	Plugin Installer (:menuselection:`Plugins --> Fetch Python Plugins`,
	go to the tab :guilabel:`Repositories`, and click :guilabel:`Add 3rd party repositories`.
	If you do not want one or more of the added repositories, they can be disabled via 
	:guilabel:`Edit`, or completely removed with the :guilabel:`Delete button`.


There is only one step required to integrate external plugins into QGIS:


*  Download an external plugin from a repository using the
:file:`Python Plugin Installer (Section `python_plugin_installer`).
The new external plugin will be added to the list of available plugins in
the :file:`Plugin Manager` and is automatically loaded.


Using the QGIS Python Plugin Installer
**************************************

.. _`python_plugin_installer`:
:index:`plugins!installing`
:index:`plugins!Python Plugin Installer`
:index:`plugins!upgrading`

.. figure::img/en/plugins/pluginmanager.png
   :align: center
   :width: 12em
   
   Installing external python plugins |nix|

In order to download and install an external Python plugin, click the
menu :menuselection:`Plugins --> Fetch Python Plugins`. The :file:`Plugin Installer` window will appear
(figure `plugininstaller`_) with the tab :guilabel:`Plugins`, containing
a list of all locally installed Python plugins, as well as plugins
available in remote repositories. Each plugin can be either:


*  **not installed** - this means the plugin is available in the repository, but is not installed yet. In order to install it, select the plugin from the list and click the button :guilabel:`Install plugin`.
*  **new** - this means that the plugin is newly available in the repository.
*  **installed** - this indicates that the plugin is already installed. If it is also available in any repository the :guilabel:`Reinstall plugin` button will be enabled. If the available version is older than the installed version, the :guilabel:`Downgrade plugin` button will appear instead.
*  **upgradeable** - this means that the plugin is installed, but there is an updated version available. In this case, the :guilabel:`Upgrade plugin` and :guilabel:`Upgrade all` buttons will be enabled.
*  **invalid** - this means that the plugin is installed, but is unavailable or broken. The reason will be explained in the plugin description field.


Plugins tab
~~~~~~~~~~~


To install a plugin, select it from the list and click the :guilabel:`Install plugin`
button. The plugin is then activated and installed in its own directory.


*  |nix| Linux and other unices: ::
	./share/qgis/python/plugins
	/home/\$USERNAME/.qgis/python/plugins
*  |osx| Mac OS X: ::
	./Contents/MacOS/share/qgis/python/plugins
	/Users/\$USERNAME/.qgis/python/plugins
*  |win| Windows: ::
	C:\text\Program Files\QGIS\python\plugins
	C:\text\Documents and Settings\$USERNAME\.qgis\python\plugins


If the installation is successful, a confirmation message will appear.

If the installation fails, the reason for the failure will be displayed
in a warning dialog. Most often, errors are the result of connection problems
and/or missing Python modules. In the former case you will likely need to
wait before trying the install again, in the latter case, you should install
the missing modules relevant to your operating system prior to using the
plugin. For Linux, most required modules should be available via a
package manager. For install instructions in Windows|win| visit the module
home page. If you are using a proxy, you may need to configure it under
:menuselection:`Edit --> Options (Gnome, OSX)` or :menuselection:`Settings --> Options (KDE, Windows)`
on the :guilabel:`Proxy` tab.

The :guilabel:`Uninstall plugin` button is enabled only if the selected plugin is installed and is not a core plugin. Note that if you have installed an update to a core plugin, you can uninstall this update with the :guilabel:`Uninstall plugin` and revert to the version shipped with Quantum GIS. This default version however, cannot be uninstalled.

Repositories tab
~~~~~~~~~~~~~~~~


The second tab :guilabel:`Repositories`, contains a list of plugin repositories 
available for the :file:`Plugin Installer`. By default, only the QGIS Official 
Repository is enabled. You can add several user-contributed repositories, including 
the central QGIS Contributed Repository and other external repositories by clicking 
the :guilabel:`Add 3rd party repositories` button. The added repositories contain 
a large number of useful plugins which are not maintained by the QGIS Development Team. 
As such, we cannot take any responsibility for them. You can also manage the repository 
list manually, that is add, remove, and edit the entries. Temporarily disabling 
a particular repository is possible by clicking the :guilabel:`Edit` button.

Options tab
~~~~~~~~~~~


The :guilabel:`Options` tab is where you can configure the settings of the :file:`Plugin Installer`. The |checkbox| Check for updates on startup checkbox tells QGIS to automatically look for plugin updates and news. By default, if this feature is enabled all repositories listed and enabled in the :guilabel:`Repositories` tab are checked for updates each time the program is started. The frequency of update checking can be adjusted using the dropdown menu, and may be adjusted from once a day right up to once a month. If a new plugin or update is available for one of the installed plugins, a notification will appear in the Status Bar. If the checkbox is disabled, looking for updates and news is performed only when the :file:`Plugin Installer` is manually launched from the menu.

Although the plugin installer update can handle ports different from 80, some internet
connections will cause problems when attempting to automatically check for updates.
In these cases, a *Looking for new plugins...* indicator will
remain visible in the Status Bar during your entire QGIS session, and may cause a
program crash when exiting. In this case please disable the checkbox.

In addition, you may specify the type of plugins that are displayed by the :file:`Python Plugin Installer`. Under *Allowed plugins*, you can specify whether you would like to:


*  Only show plugins from the official repository,
*  Show all plugins except those marked as experimental,
*  or Show all plugins, even those marked as experimental.

.. note:: 
	**Using experimental plugins**
	Experimental plugins are generally unsuitable for production use. These plugins are in the early stages of development, and should be considered 'incomplete' or 'proof of concept' tools. The QGIS development team does not recommend installing these plugins unless you intend to use them for testing purposes.

Data Providers
==============
:index:`data providers`

Data Providers are "special" plugins that provides access to a data store.
By default, QGIS supports PostGIS layers and disk-based data stores supported by the GDAL/OGR library.
A Data Provider plugin extends the ability of QGIS to use other data sources.

Data Provider plugins are registered automatically by QGIS at startup.
They are not managed by the Plugin Manager but used behind the scenes when a data type is added as a layer in QGIS.

.. [1] Updates of core plugins may be available in this repository as external overlays.
.. [2] fTools, Mapserver Export, and the Plugin Installer are Python plugins, but they are also part of 
the QGIS sources, and are automatically loaded and enabled inside the QGIS Plugin Manager 
(see Section :ref:`load_external_plugin`).
