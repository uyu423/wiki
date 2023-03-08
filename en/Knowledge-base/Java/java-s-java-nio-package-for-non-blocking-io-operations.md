---
title: Java's java.nio Package for Non-Blocking I/O Operations
description: 
published: true
date: 2023-02-15T11:17:51.070Z
tags: 
editor: markdown
dateCreated: 2023-02-15T11:17:43.486Z
---

- [Paquete java.nio de Java para operaciones de E/S sin bloqueo***Spanish** document is available*](/es/Knowledge-base/Java/java-s-java-nio-package-for-non-blocking-io-operations)
{.links-list}
- [Java 的非阻塞 I/O 操作的 java.nio 包***Chinese Simplified** document is available*](/zh/Knowledge-base/Java/java-s-java-nio-package-for-non-blocking-io-operations)
{.links-list}
- [비차단 I/O 작업을 위한 Java의 java.nio 패키지***Korean** document is available*](/ko/Knowledge-base/Java/java-s-java-nio-package-for-non-blocking-io-operations)
{.links-list}



# Java's java.nio Package for Non-Blocking I/O Operations

Java's `java.nio` package provides APIs for performing *non-blocking* input/output (I/O) operations in Java. Non-blocking I/O means that a thread can initiate an I/O operation without having to wait for the operation to complete. This can lead to more efficient I/O operations, as a thread can perform other work while the I/O operation is being performed.

## Overview of java.nio

The `java.nio` package was introduced in Java 1.4 and provides the following:

- A set of `Buffer` classes for storing data in various primitive types
- A set of `Channel` classes for performing I/O operations
- A set of `Selector` classes for multiplexing I/O operations
- A set of `FileLock` and `FileChannel` classes for performing file-based I/O operations

In addition, the `java.nio.file` package was introduced in Java 7 and provides support for file-based I/O operations.

## Buffer

A `Buffer` is a container for data of a specific primitive type. There are `Buffer` classes for each of the primitive data types: `ByteBuffer`, `CharBuffer`, `DoubleBuffer`, `FloatBuffer`, `IntBuffer`, `LongBuffer`, and `ShortBuffer`.

A `Buffer` has the following properties:

- **Capacity:** The maximum number of elements that can be stored in the buffer.
- **Limit:** The index of the first element that should not be read or written.
- **Position:** The index of the next element to be read or written.

A `Buffer` also has the following methods:

- `clear()`: Sets the position to 0 and the limit to the capacity.
- `flip()`: Sets the limit to the current position and the position to 0.
- `rewind()`: Sets the position to 0.
- `remaining()`: Returns the number of elements between the position and the limit.
- `hasRemaining()`: Returns `true` if there are elements remaining, `false` otherwise.

## Channel

A `Channel` is a `Buffer`-like structure that represents an open connection to an I/O device. A `Channel` can be open for reading, writing, or both.

There are several types of `Channel`s, including `FileChannel`, `DatagramChannel`, `SocketChannel`, and `Pipe.SinkChannel`.

A `Channel` has the following methods:

- `isOpen()`: Returns `true` if the channel is open, `false` otherwise.
- `close()`: Closes the channel.
- `read(Buffer)`: Reads data from the channel into the given buffer.
- `write(Buffer)`: Writes data from the given buffer into the channel.

## Selector

A `Selector` is used for multiplexing I/O operations. A `Selector` can be used to wait for I/O operations to complete on one or more `Channel`s.

A `Selector` has the following methods:

- `open()`: Opens a `Selector`.
- `close()`: Closes the `Selector`.
- `select()`: Returns the `SelectionKey`s for the `Channel`s on which I/O operations are ready to be performed.
- `select(long)`: Returns the `SelectionKey`s for the `Channel`s on which I/O operations are ready to be performed, or `null` if the timeout expires.
- `selectedKeys()`: Returns the `Set` of `SelectionKey`s for the `Channel`s on which I/O operations are ready to be performed.
- `keys()`: Returns the `Set` of `SelectionKey`s for all `Channel`s registered with this `Selector`.

## FileLock

A `FileLock` is used to lock a region of a `FileChannel`. A `FileLock` has the following methods:

- `isShared()`: Returns `true` if the lock is shared, `false` otherwise.
- `release()`: Releases the lock.
- `isValid()`: Returns `true` if the lock is still valid, `false` otherwise.

## FileChannel

A `FileChannel` is a `Channel` that is used for performing file-based I/O operations. A `FileChannel` has the following methods:

- `lock(long, long, boolean)`: Locks a region of the file.
- `tryLock()`: Tries to lock a region of the file.
- `read(ByteBuffer, long)`: Reads data from the file into the given buffer.
- `write(ByteBuffer, long)`: Writes data from the given buffer into the file.

## java.nio.file

The `java.nio.file` package was introduced in Java 7 and provides support for file-based I/O operations. This package contains the following classes:

- `Path`: A representation of a file system path.
- `Paths`: A factory for creating `Path` objects.
- `Files`: A utility class for performing file-related operations.

## Conclusion

Java's `java.nio` package provides APIs for performing non-blocking I/O operations in Java. The `java.nio.file` package was introduced in Java 7 and provides support for file-based I/O operations.