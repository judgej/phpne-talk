phpne-talk
==========

PHPNE talk notes (February 2014)

This repository contains notes for the talk and any code used for deomonstrations.

Subject
-------

The PHP library php-loep/flysystem at https://github.com/php-loep/flysystem in the namespace League\Flysystem

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

~~Not enough type-hints. Needs more, as objects are passed around all over the place (improvements section?).~~
Typehints are going in now.

Not sure if can be made to support all the standard PHP protocols (http://www.php.net/manual/en/wrappers.php)
but maybe a "php" storage engine can do this, or maybe it would need a wrapper around the whole thing to
set up the storage engines on-the-fly and cache them?

Alternatives
------------

Resources can be wrapped around resources, with the many functions they need being hidden
behind magic methods (__call(), __toString(), __get() etc).

* [php-resource](https://code.google.com/p/php-resource/) offers a comprehensive OPP wrapper for resources.
* [shesek](http://www.shesek.info/php/generic-php-object-wrapper-for-resources) offers a simpler OOP wrapper for resources.
* [Illuminate\Filesystem\Filesystem](http://laravel.com/api/source-class-Illuminate.Filesystem.Filesystem.html#Filesystem) used by Laravel. Not driver-based, so it *only* supports local filesystem operations. However, it is simple to swap it out through its facade, though that is essentially setting a single, global filestore for the whole application.
* [KnpLabs/Gaufrette](https://github.com/KnpLabs/Gaufrette) takes a similar approach, and has been around for a couple of years.
* [discordier/php-filesystem](https://github.com/discordier/php-filesystem) tries to get to some raw file access methods, though seems to have stopped development before many adapters were written. Implements filesystem iterators, which many other libraries do not.

Architecture
------------

Uses the [adapter](http://www.fluffycat.com/PHP-Design-Patterns/Adapter/) pattern so that many backend
storage engines can be pulled in and accessed through a common adapter interface.

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

* Adding new drivers/storage
* Interoperability; how does it fit with libraries already out there?
* Library wrapper for frameworks, e.g. a DiC wrapper package for Laravel so it is quick to use out of the box.
  No "siloing" though - just an adapter.

Storage that would be interesting
---------------------------------

* Flickr
* IMAP
* PDO/MySQL
* BBC iPlayer
* Google App Engine (uploaded files, cache files)

Reference Tables
================

It would be great if all these could be supported right out of the box.

Standard PHP resource protocols
-------------------------------

Note that streams are not filesystems, but a way to access data, some of which
may be in filesystems.

| Prefix (wrapper) | Description |
| ---------------- | ----------- |
| file:// | Accessing local filesystem |
| http:// | Accessing HTTP(s) URLs |
| ftp:// | Accessing FTP(s) URLs |
| php:// | Accessing various I/O streams (stdin, stdout and stderr, plus many more) |
| zlib:// | Compression Streams |
| data:// | Data (RFC 2397) |
| glob:// | Find pathnames matching pattern |
| mphar:// | PHP Archive |
| ssh2:// | Secure Shell 2 |
| rar:// | RAR |
| ogg:// | Audio streams |
| expect:// | Process Interaction Streams |

PHP Filesystem functions
------------------------

Nice to see equivalents to all these functions. Also documenting how the syntax varies
between these functions and the equivalent flysystem methods, to make migration plans
easier to implement.

| Function | Operates on | Description |
| -------- | ----------- | ----------- |
| basename |path | Returns trailing name component of path |
| chgrp | pathname | Changes file group |
| chmod | pathname | Changes file mode |
| chown | pathname | Changes file owner |
| clearstatcache | pathname (optional) | Clears file status cache |
| copy | pathnames | Copies file |
| dirname | path | Returns parent directory's path |
| disk_free_space | directory | Returns available space on filesystem or disk partition |
| disk_total_space | directory | Returns the total size of a filesystem or disk partition |
| diskfreespace | directory | Alias of disk_free_space |
| fclose | resource | Closes an open file pointer |
| feof | resource | Tests for end-of-file on a file pointer |
| fflush | resource | Flushes the output to a file |
| fgetc | resource | Gets character from file pointer |
| fgetcsv | resource | Gets line from file pointer and parse for CSV fields |
| fgets | resource | Gets line from file pointer |
| fgetss | resource | Gets line from file pointer and strip HTML tags |
| file_exists | pathname | Checks whether a file or directory exists |
| file_get_contents | pathname | Reads entire file into a string |
| file_put_contents | pathname | Write a string to a file |
| file | pathname | Reads entire file into an array |
| fileatime | pathname | Gets last access time of file |
| filectime | pathname | Gets inode change time of file |
| filegroup | pathname | Gets file group |
| fileinode | pathname | Gets file inode |
| filemtime | pathname | Gets file modification time |
| fileowner | pathname | Gets file owner |
| fileperms | pathname | Gets file permissions |
| filesize | pathname | Gets file size |
| filetype | pathname | Gets file type |
| flock | resource | Portable advisory file locking |
| fnmatch | pattern | Match filename against a pattern |
| fopen | pathname | Opens file or URL. Creates a resource. |
| fpassthru | resource | Output all remaining data on a file pointer |
| fputcsv | resource | Format line as CSV and write to file pointer |
| fputs | resource | Alias of fwrite |
| fread | resource | Binary-safe file read |
| fscanf | resource | Parses input from a file according to a format |
| fseek | resource | Seeks on a file pointer |
| fstat | resource | Gets information about a file using an open file pointer |
| ftell | resource | Returns the current position of the file read/write pointer |
| ftruncate | resource | Truncates a file to a given length |
| fwrite | resource | Binary-safe file write |
| glob | pattern | Find pathnames matching a pattern |
| is_dir | pathname | Tells whether the filename is a directory |
| is_executable | pathname | Tells whether the filename is executable |
| is_file | pathname | Tells whether the filename is a regular file |
| is_link | pathname | Tells whether the filename is a symbolic link |
| is_readable | pathname | Tells whether a file exists and is readable |
| is_uploaded_file | pathname | Tells whether the file was uploaded via HTTP POST |
| is_writable | pathname | Tells whether the filename is writable |
| is_writeable | pathname | Alias of is_writable |
| lchgrp | pathname | Changes group ownership of symlink |
| lchown | pathname | Changes user ownership of symlink |
| link | pathnames | Create a hard link |
| linkinfo | path | Gets information about a link |
| lstat | pathnames | Gives information about a file or symbolic link |
| mkdir | path | Makes directory |
| move_uploaded_file | filename + pathname | Moves an uploaded file to a new location |
| parse_ini_file | pathname | Parse a configuration file |
| pathinfo | path or pathname | Returns information about a file path |
| pclose | process resource | Closes process file pointer |
| popen | command string | Opens process file pointer. Returns a resource. |
| readfile | pathname | Outputs a file |
| readlink | path | Returns the target of a symbolic link |
| realpath_cache_get | void | Get realpath cache entries |
| realpath_cache_size | void | Get realpath cache size |
| realpath | path | Returns canonicalized absolute pathname |
| rename | pathnames | Renames a file or directory |
| rewind | resource | Rewind the position of a file pointer |
| rmdir | path | Removes directory |
| set_file_buffer | | Alias of stream_set_write_buffer |
| stat | pathname | Gives information about a file |
| symlink | pathnames | Creates a symbolic link |
| tempnam | path | Create file with unique file name |
| tmpfile | void | Creates a temporary file. Creates a resource. |
| touch | pathname | Sets access and modification time of file |
| umask | string | Changes the current umask |
| unlink | pathname + optional context resource | Deletes a file |

Each function operates on one of the following as its file:

* pathname - a path and file (absolute or relative file)
* path - a path only (a directory)
* filename - a file name with no path
* resource - a file resource

There is a real good mix of pathnames and resources.

A pathname can be a local path to a file, or could make use of a wrapper. Each wrapper is invoked
by adding to the path with the scheme:// prefix. Schemss can include 'file', 'ftp', 'php', 'phar',
and many others. Also custom wrappers can be registered for custom streams. These wrappers can 
both read and write.

Q: can wrappers be mixed, e.g. rename('ftp://user:pass@example.com/foo.txt', 'zip://archive.zip#bar.txt')?
