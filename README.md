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

Not sure if can be made to support all the standard PHP protocols (http://www.php.net/manual/en/wrappers.php)
but maybe a "php" storage engine can do this, or maybe it would need a wrapper around the whole thing to
set up the storage engines on-the-fly and cache them?

Alternatives
------------

TBC

Architecture
------------

Pattern adapter/driver (TBC)

The interfaces it implements.

Can a connection span page requests efficiently, e.g. by keeping connections live through
memcached, if that is even possible?

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

Reference Tables
================

Standard PHP resource protocols
-------------------------------

| Prefix | Description |
| ------ | ----------- |
| file:// | Accessing local filesystem |
| http:// | Accessing HTTP(s) URLs |
| ftp:// | Accessing FTP(s) URLs |
| php:// | Accessing various I/O streams |
| zlib:// | Compression Streams |
| data:// | Data (RFC 2397) |
| glob:// | Find pathnames matching pattern |
| mphar:// | PHP Archive |
| ssh2:// | Secure Shell 2 |
| rar:// | RAR |
| ogg:// | Audio streams |
| expect:// | Process Interaction Streams |
