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
data structure in memory. This allowed them to be passed around by reference. In fact,
resources have always been passed by reference.
