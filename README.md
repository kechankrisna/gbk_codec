The GBK (Chinese Internal Code Specification: China GBK 汉字内码扩展规范编码表) code converter library

Created from GBK standard, generated code converter tables, overwrote converter class of dart. It's a pure dart solution.

Two class for GBK library: 
1. gbk, standard 16-bits codec library
2. gbk_bytes, gbk byte codec library, for bytes stream

## Usage

deCode and enCode using samples, standard 16-bits library and byte library:

```dart
import 'package:gbk_codec/gbk_codec.dart';

main() {
  String text = 'dart GBK code 兩岸猿聲啼不住, chinese simple:轻舟已过万重山.';

  //gbk encode
  List<int> gbkCodes = gbk.encode(text);
  String hex = '';
  gbkCodes.forEach((i) {hex += i.toRadixString(16)+ ' ';});
  print(hex);

  //gbk decode
  String decoded_text = gbk.decode(gbkCodes);
  print(decoded_text);

  //gbk_bytes encode
  List<int> gbk_byteCodes = gbk_bytes.encode(text);
  hex = '';
  gbk_byteCodes.forEach((i) {hex += i.toRadixString(16)+ ' ';});
  print(hex);

  //gbk_bytes decode
  String decoded_bytes_text = gbk_bytes.decode(gbk_byteCodes);
  print(decoded_bytes_text);
}

```
Here is online page decoding sample:
```dart
import 'dart:io';
import 'package:gbk_codec/gbk_codec.dart';

const String URL = 'http://www.creaders.net/about_us.html';

main() {
  HttpClient()
      .getUrl(Uri.parse(URL))
      .then((HttpClientRequest request) {return request.close();})
      .then((response) {
          List<int> full = new List<int>();
          response.listen((data) => full.addAll(data),
                    onDone:() => print(gbk_bytes.decode(full)), 
                    onError:(e) => print);  
      });             
}
```

## Features and bugs

Please file feature requests and bugs at the [issue tracker][tracker].

