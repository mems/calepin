Aka Protobuf

[ASN](https://en.wikipedia.org/wiki/Abstract_Syntax_Notation_One) of protobuf data:

```
Protobuf ::= BEGIN
  Message ::= SEQUENCE {
    length VARINT
    payload SEQUENCE OF MessageField
  }
  MessageField ::= SEQUENCE {
    fieldNumAndType VARINT
    payload Message | Scalar | Repeated
  }
  Scalar ::= VARINT | FIXED32 | FIXED64
  Repeated ::= SEQUENCE {
    length VARINT
    payload SEQUENCE of (Scalar | Message)
  }
END
```

Note abou (auto)pack:

> Only repeated fields of primitive numeric types (types which use the varint, 32-bit, or 64-bit wire types) can be declared "packed".



- [Protocol Buffers — Wikipedia](https://en.wikipedia.org/wiki/Protocol_Buffers)
- [google/protobuf: Protocol Buffers - Google's data interchange format](https://github.com/google/protobuf)
- [mmcloughlin/reprotobuf: Reverse engineer protobuf from javanano](https://github.com/mmcloughlin/reprotobuf)
- [Reversing Google Play and Micro-Protobuf applications | Segmentation fault](http://www.segmentationfault.fr/publications/reversing-google-play-and-micro-protobuf-applications/)
- [Encoding  |  Protocol Buffers  |  Google Developers](https://developers.google.com/protocol-buffers/docs/encoding)
- [Reverse-engineering of protobuf-based applications | Sysdream](http://web.archive.org/web/20150914232835/https://www.sysdream.com/reverse-engineering-protobuf-apps)

See also:

- [Variable-length quantity - Wikipedia](https://en.wikipedia.org/wiki/Variable-length_quantity)

Libraries & readers:

- [mapbox/pbf: A low-level, lightweight protocol buffers implementation in JavaScript.](https://github.com/mapbox/pbf)
- [evanw/pbjs: A minimal implementation of Google Protocol Buffers for JavaScript](https://github.com/evanw/pbjs)
- [mafintosh/protocol-buffers-schema: No nonsense protocol buffers schema parser written in Javascript](https://github.com/mafintosh/protocol-buffers-schema)
- `protoc --decode_raw < data.bin` to read binary data to text format. `protoc` already compiled is downloadable from the repository of protobuf
- [Parsing Protocol-Buffers without knowing the .proto - Stack Overflow](https://stackoverflow.com/questions/13937882/parsing-protocol-buffers-without-knowing-the-proto)
- [protocol buffers - raw decoder for protobufs format - Stack Overflow](https://stackoverflow.com/questions/7343867/raw-decoder-for-protobufs-format)
- [jmendeth/protobuf-inspector: Tool to reverse-engineer Protocol Buffers with unknown definition](https://github.com/jmendeth/protobuf-inspector)
