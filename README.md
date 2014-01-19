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

Not enough type-hints. Needs more, as objects are passed around all over the place (improvements section?).

Not sure if can be made to support all the standard PHP protocols (http://www.php.net/manual/en/wrappers.php)
but maybe a "php" storage engine can do this, or maybe it would need a wrapper around the whole thing to
set up the storage engines on-the-fly and cache them?

Alternatives
------------

Resources can be wrapped around resources, with the many functions they need being hidden
behind magic methods (__call(), __toString(), __get() etc).

* [php-resource](https://code.google.com/p/php-resource/) offers a comprehensive OPP wrapper for resources.
* [shesek](http://www.shesek.info/php/generic-php-object-wrapper-for-resources) offers a simpler OOP wrapper for resources.

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

* Adding new drivers/storage
* Interoperability; how does it fit with libraries already out there?

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

| Function | Description |
| -------- | ----------- |
| basename | Returns trailing name component of path |
| chgrp | Changes file group |
| chmod | Changes file mode |
| chown | Changes file owner |
| clearstatcache | Clears file status cache |
| copy | Copies file |
| delete | See unlink or unset |
| dirname | Returns parent directory's path |
| disk_free_space | Returns available space on filesystem or disk partition |
| disk_total_space | Returns the total size of a filesystem or disk partition |
| diskfreespace | Alias of disk_free_space |
| fclose | Closes an open file pointer |
| feof | Tests for end-of-file on a file pointer |
| fflush | Flushes the output to a file |
| fgetc | Gets character from file pointer |
| fgetcsv | Gets line from file pointer and parse for CSV fields |
| fgets | Gets line from file pointer |
| fgetss | Gets line from file pointer and strip HTML tags |
| file_exists | Checks whether a file or directory exists |
| file_get_contents | Reads entire file into a string |
| file_put_contents | Write a string to a file |
| file | Reads entire file into an array |
| fileatime | Gets last access time of file |
| filectime | Gets inode change time of file |
| filegroup | Gets file group |
| fileinode | Gets file inode |
| filemtime | Gets file modification time |
| fileowner | Gets file owner |
| fileperms | Gets file permissions |
| filesize | Gets file size |
| filetype | Gets file type |
| flock | Portable advisory file locking |
| fnmatch | Match filename against a pattern |
| fopen | Opens file or URL |
| fpassthru | Output all remaining data on a file pointer |
| fputcsv | Format line as CSV and write to file pointer |
| fputs | Alias of fwrite |
| fread | Binary-safe file read |
| fscanf | Parses input from a file according to a format |
| fseek | Seeks on a file pointer |
| fstat | Gets information about a file using an open file pointer |
| ftell | Returns the current position of the file read/write pointer |
| ftruncate | Truncates a file to a given length |
| fwrite | Binary-safe file write |
| glob | Find pathnames matching a pattern |
| is_dir | Tells whether the filename is a directory |
| is_executable | Tells whether the filename is executable |
| is_file | Tells whether the filename is a regular file |
| is_link | Tells whether the filename is a symbolic link |
| is_readable | Tells whether a file exists and is readable |
| is_uploaded_file | Tells whether the file was uploaded via HTTP POST |
| is_writable | Tells whether the filename is writable |
| is_writeable | Alias of is_writable |
| lchgrp | Changes group ownership of symlink |
| lchown | Changes user ownership of symlink |
| link | Create a hard link |
| linkinfo | Gets information about a link |
| lstat | Gives information about a file or symbolic link |
| mkdir | Makes directory |
| move_uploaded_file | Moves an uploaded file to a new location |
| parse_ini_file | Parse a configuration file |
| parse_ini_string | Parse a configuration string |
| pathinfo | Returns information about a file path |
| pclose | Closes process file pointer |
| popen | Opens process file pointer |
| readfile | Outputs a file |
| readlink | Returns the target of a symbolic link |
| realpath_cache_get | Get realpath cache entries |
| realpath_cache_size | Get realpath cache size |
| realpath | Returns canonicalized absolute pathname |
| rename | Renames a file or directory |
| rewind | Rewind the position of a file pointer |
| rmdir | Removes directory |
| set_file_buffer | Alias of stream_set_write_buffer |
| stat | Gives information about a file |
| symlink | Creates a symbolic link |
| tempnam | Create file with unique file name |
| tmpfile | Creates a temporary file |
| touch | Sets access and modification time of file |
| umask | Changes the current umask |
| unlink | Deletes a file |
