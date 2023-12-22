---
title: File Descriptors
---
File descriptors are a low-level abstraction to perform operations on files. A file descriptor is represented with an integer value - but this value is guaranteed to be unique among open files.

## Functions

Some common functions (in C) that use file descriptors include:

- `open()` - opens a file for reading and writing. Returns a file descriptor
- `close()`
- `read()`
- `write()`

## References

1. Jon Erickson. *Hacking: The Art of Exploitation*. 2nd edition, No Starch Press, 2008.
