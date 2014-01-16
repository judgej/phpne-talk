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

What flysystem isn't
--------------------

TBC

Alternatives
------------

TBC

Architecture
------------

Pattern adapter/driver (TBC)

General use
-----------

Out of the box. (TBC)

How easy is it to put into an existing product? Any case studies?

The "mount manager" allowing one "virtual filesystem" to be constructed from many different
(or the same?) storage engines.

Pathnames for files - the syntax details.

Expansion
---------

Adding new drivers/storage

Storage that would be interesting
---------------------------------

* Flickr
* IMAP
* PDO/MySQL
* BBC iPlayer

