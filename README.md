#Autoloader

The Asgard Autoloader supports PSR-4 and provides some additional features that can be used in addition to the composer autoloader.

- [Installation](#installation)
- [Usage](#usage)
- [Nested Namespaces](#nested-namespaces)
- [Global Classes](#global-classes)
- [Namespace Mapping](#namespace-mapping)
- [Class Mapping](#class-mapping)
- [Preloading Files](#preloading-files)

<a name="installation"></a>
##Installation

	composer require asgard/autoloader 0.*

<a name="usage"></a>
##Usage

	$autoloader = new \Asgard\Autoloader\Autoloader();
	$autoloader->register();

This register the autoloader in the PHP process.

<a name="nested-namespaces"></a>
##Nested Namespaces
When looking for a class like Namespace\Class in Namespace\Subnamespace\Class, unlike some other languages, PHP does not look up in the parents namespaces.

Asgard autoloader however does it if you enable it:

	$autoloader->nestedNamespace(true);

<a name="global-classes"></a>
##Search classes

When using a class without namespace, the autoloader will search for the class in the existing or registered ones whose class name is the same.

For example if the class \Namespace\Class exists or is registered via $autoloader->map($class, $file), and you call \Class, the autoloader will be smart enough to alias \Class to \Namespace\Class, but only if there is only class with the same name.

To enable it:

	$autoloader->search(true);

By combining search and nestedNamespace, the autoloader will be able to match classes like \Namespace\Class to \Anothernamespace\Class if it has to. However it is recommended to use class mapping for better performances.

<a name="namespace-mapping"></a>
##Namespace mapping

Like with composer, you can map a namespace to a specific directory:

	$autoloader->namespaceMap('Namespace', 'myclasses/');

<a name="class-mapping"></a>
##Class mapping

Like the composer autoloader, you can map a class to a specific file:

	$autoloader->map('MyClass', 'myclass.php');

<a name="preloading-files"></a>
##Preloading files

To enable or disable preloading:

	$autoloader->preload(true); #or false

You can then ask the autoloader to analyse a folder's files whose names start with a capital to help it find global classes:

	$autoloader->preloadDir('classes/');

	$autoloader->preloadFile('classes/MyClass.php');

Files like classes\Subfolder\MyClass.php will be mapped to class \MyClass. The preloading can be cached if you provide the autoloader with a cache driver:

	$autoloader->setCache(new \Asgard\Cache\ApcCache());

###Contributing

Please submit all issues and pull requests to the [asgardphp/asgard](http://github.com/asgardphp/asgard) repository.

### License

The Asgard framework is open-sourced software licensed under the [MIT license](http://opensource.org/licenses/MIT)