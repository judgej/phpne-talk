PHP Streams
===========

An overview of streams would be useful here.

A stream is a resource that has a streamable behaviour. The mean features of this is that:

* The stream is a linear sequence of data - it has a start, middle and end.
* A stream has no structure. The data in the stream may represent a meaningful structure to functionality elsewhere, but it is not a property of the stream.
* A stream is readable/writeable/seekable - pick any combination.

For example, a stream may give you the data for a file. It may come from a file with a name in a directory, but that location is not a direct property of the stream, it is just how it is located. A file is not a stream; but a file can be read and written using a stream.

A stream does not have its entire content stored in memory. This allows very large files to be handled - written and read.

Wrappers
--------

Each stream is handled by a "wrapper". Streams are not objects, but they were, a wrapper wopuld be an extension to the basic stream object.

Every stream is handled by a wrapper. If you do not specify the wrapper, then the local filesystem is selected by default. This is the "file://" wrapper.

The locator for a stream is specified as `scheme://target`. The scheme is the name of the wrapper, and the target is a locator that is specific to the wrapper. It may be just a pathname, or a domain, or may include authentication details (e.g. for ftp://).

Examples (TODO)

Filters
-------

Wrappers can use filters. A filter processes the stream (for reading or writing) and can do such things as compressing or decompressing, changing charactersets, or anything more complex. The filters are tagged onto the front of a stream locator using the meta wrapper `php://filter`.

Examples (TODO)

Contexts
--------

This is another name for "options". You can set options globally for a wrapper, or pass specific options into some stream creation functions.

