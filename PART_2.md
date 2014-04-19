## Part 2: Encoding and decoding binary files

The article we'll work through in this part of the 
course is [Working with binary file formats](https://practicingruby.com/articles/binary-file-formats).
Reading it carefully should prepare you to work through the questions
and exercises for this topic.

## Questions

TODO

## Exercises

In this set of exercises, you will explore and implement a minimal subset
of the [MessagePack][] binary serialization format. By doing so, you'll exercise
many of the same tools and techniques covered in the "Working with binary file
formats article" while also familiarizing yourself with a fast and efficient
alternative to JSON for data serialization.

> NOTE: The supporting materials for these exercises are in `samples/part2`

**STEP 1:** The `example.msg` file contains a collection of key-value pairs 
encoded as a MessagePack `fixmap`. Using the [MessagePack spec][spec] and a hex dump
utility (i.e. `xxd` or something similar), examine the contents 
of the file and see if you discover the following details without
writing a program to process the file:

* The size of the map (i.e. the number of key-value pairs)
* The human readable ASCII representation for each of the keys (all of which are encoded with the `fixstr` type)
* The type of each value in the map (i.e. `"foo" => fixint, "bar" => float 64` )

The very first byte in the file will tell you how many elements the 
encoded `fixmap` has, and then you'll repeat a similar process to 
uncover the details about its keys and values.

**STEP 2:** Implement the `Packer.unpack` method, which takes an array of bytes
encoded in MessagePack format and converts it to an equivalent primitive 
Ruby object. The `packer.rb` file contains a stubbed out method for you to
implement, as well as a simple test. You are only expected to implement enough
of MessagePack's functionality to process the `example.msg` file, and it only
uses a small subset of the number of types available in MessagePack.

**STEP 3:** Implement the `Unpacker.pack` method, which takes a primitive Ruby
object and converts it into a byte array in MessagePack format. You'll find
a stub method and test for this in `unpacker.rb`. As in STEP 2, you're only
expected to convert the limited set of types used in the `example.msg` file, you
do not need to write a converter for all Ruby formats

**STEP 4:** Using the extension type interface provided by MessagePack, revise
`Packer.pack` and `Unpacker.unpack` to support encoding and decoding of Ruby
symbol objects as an application-specific type. See `extended_messages.rb`
for a test case that covers this scenario.

[MessagePack]: http://msgpack.org/
[spec]: https://github.com/msgpack/msgpack/blob/master/spec.md
