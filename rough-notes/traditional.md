Traditional PHP Method of Accessing Files
=========================================

Traditionally, files were accessed through a stream resource and many specialised
functions that operated on that resource.

What is a Resource?
-------------------

Resources were created to fill the gap that the lack of OOP left in early versions of PHP.
They have stayed with us since.

A resource is a primitive PHP type, just like an int or a string. The implementation of
resources is not unlike C-style pointers, with each resource variable pointing to a
data structure in memory. The structure holds properties and state of the resource.
Being a pointer allows resources to be passed around by reference. In fact,
resources have always been passed by reference.

A resource is not an object. It does not have methods or properties you can access
directly. You can only create or access or use resources through specialised functions
that operat, create or destroy those resources.

A PHP resource is a data structure that represents an external resource. An external
resource can be anything - a file or stream, a directory, a document, an image, a HTTP
connection, a Flash object, a database connection - the list goes on.

There are around 120 [resource types](http://www.php.net/manual/en/resource.php) available
in PHP in a standard install. Each one has dozens of functions that operate on them, and
that fills the global function space with well over a thousand functions that we really
don't need; we don't need, because there are better ways of handling external resources now.

TODO: example of using a stream resource and the functions involved.

The problems with resources is:

* They are not objects, so cannot be extended, serialised, dumped to a log file.
* They require many specialised functions to operate on them.

This talk is going to focus on one resource type: stream. This type handles directories
and directory structures, files and file names, and supports a number of different
protocols (not just local files). The flysystem package aims to offer an alternative
to this resource in a more OOP way.
