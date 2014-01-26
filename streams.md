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



