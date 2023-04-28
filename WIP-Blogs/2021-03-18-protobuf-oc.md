https://developers.google.com/protocol-buffers/docs/cpptutorial
https://www.cnblogs.com/pengyingh/articles/7252218.html
https://www.cnblogs.com/autyinjing/p/6495103.html

https://github.com/protocolbuffers/protobuf

brew install protobuf

```
// $SRC_DIR: .proto 所在的源目录
// --cpp_out: 生成 c++ 代码
// $DST_DIR: 生成代码的目标目录
// xxx.proto: 要针对哪个 proto 文件生成接口代码
 
protoc -I=$SRC_DIR --cpp_out=$DST_DIR $SRC_DIR/xxx.proto
```

protoc --proto_path=/Users/cunfa/QDCares/Projects/ios-components-web/QDCWebModule/Netty/protobuf/proto --objc_out=/Users/cunfa/QDCares/Projects/ios-components-web/QDCWebModule/Netty/protobuf /Users/cunfa/QDCares/Projects/ios-components-web/QDCWebModule/Netty/protobuf/proto/CommandPBDto.proto



[oc doc](https://developers.google.com/protocol-buffers/docs/reference/objective-c-generated?hl=en)

```
protoc --proto_path=src --objc_out=build/gen src/foo.proto src/bar/baz.proto
```