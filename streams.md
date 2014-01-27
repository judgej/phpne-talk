PHP Streams
===========

An overview of streams would be useful here.

A stream is a resource that has a streamable behaviour. The mean features of this is that:

* The stream is a linear sequence of data - it has a start, middle and end.
* A stream has no structure. The data in the stream may represent a meaningful structure to functionality elsewhere, but it is not a property of the stream.
* A stream is readable/writeable/seekable - pick any combination.

For example, a stream may give you the data for a file. It may come from a file with a name in a directory, but that location is not a direct property of the stream, it is just how it is located. A file is not a stream; but a file can be read and written using a stream.

Streams are acessed through their locator - e.g. a pathname or URI - but do not expose the structure that the resources are organised into. That structure is essentially the filesystem.

A stream does not [need to] have its entire content stored in memory. This allows very large files to be handled, i.e. written and read.

There are 47 stream_*() functions (see http://www.php.net/manual/en/ref.stream.php) in PHP for creating, using and deleting streams. Many of the functions have no user comments, which usually indicates they are not well used. They are very powerful though, allowing much functionality to be hidden away behind some simple streams.

Wrappers
--------

Each stream is handled by a "wrapper". Streams are not objects, but they were, a wrapper wopuld be an extension to the basic stream object. The wrapper handles the protocol, such as knowing how to open a local file, or opening sockets to an FTP or web server and logging in if required.

Every stream is handled by a wrapper. If you do not specify the wrapper, then the local filesystem is selected by default. This is the "file://" wrapper.

The locator for a stream is specified as `scheme://target`. The scheme is the name of the wrapper, and the target is a locator that is specific to the wrapper. It may be just a pathname, or a domain, or may include authentication details (e.g. for ftp://).

Examples (TODO)

Filters
-------

Wrappers can use filters. A filter processes the stream (for reading or writing) and can do such things as compressing or decompressing, changing charactersets, or anything more complex. The filters are tagged onto the front of a stream locator using the meta wrapper `php://filter`.

Examples (TODO)

Alternatively filters can be added to a stream after the stream is opened using stream_filter_append() or stream_filter_prepend(). This is probably easier than trying to squeeze it into the intial stream locator when creating the stream.

Examples (TODO)

Just as for wrappers, a custom filter can be created, registered and used by a stream. The most common types of filters handle compression, conversion, encryption or perform string operations.

Contexts
--------

This is another name for "options". You can set options globally for a wrapper, or pass specific options into some stream creation functions. The options available are specific to the wrapper, but they can be used to tweak the protocol, for example, such as making a `http://` stream use POST or inserting authentication tokens into its header.

Custom Wrappers
---------------

You are not stuck with the wrappers that PHP provides; you can register your own custom wrappers. A wrapper could, for example, log into Dropbox (with an authentication token passed in as a context option) and handle a file there as a stream. Whether Dropbox really supports streaming, or it is emulated by local cacheing appending to a file, does not matter; it should still look like a stream to the local application.
