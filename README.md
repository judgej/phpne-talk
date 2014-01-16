phpne-talk
==========

PHPNE talk notes (February 2014)

This repository contains notes for the talk and any code used for deomonstrations.

Subject
-------

The PHP library php-loep/flysystem at https://github.com/php-loep/flysystem

The library provides an abstract access to file stores, looking much like a
filesystem but providing many storage options, both local and remote.

What flysystem is
-----------------

"Flysystem is a filesystem abstraction which allows you to easily swap out a local filesystem for a remote one."

It provides a generic API for common tasks you would perform with files.
Once your file tasks go through the library API, then the storage layer can be switched
to other storage engines.

How many Filesystem (http://www.php.net/manual/en/book.filesystem.php) functions are implemented?
A checklist would help.

What flysystem isn't
--------------------

Seems to implement self-contained interfaces only (e.g. no iterator for streams or standard
PHP filesystem interfaces e.g. Streams (check this).

Not enough type-hints. Needs more as objects are passed around all over the place.

Alternatives
------------

TBC

Architecture
------------

Pattern adapter/driver (TBC)

The interfaces it implements.

General use
-----------

Out of the box. (TBC)

How easy is it to put into an existing product? Any case studies?

The "mount manager" allowing one "virtual filesystem" to be constructed from many different
(or the same?) storage engines.

Pathnames for files - the syntax details.

Streams vs blocks of data.

Cacheing - how and why.

Incorporation into a DiC.

Expansion
---------

Adding new drivers/storage

Storage that would be interesting
---------------------------------

* Flickr
* IMAP
* PDO/MySQL
* BBC iPlayer

