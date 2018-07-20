# retrofit-jsonrpc

JSON-RPC with Retrofit.

# Usage

Declare your RPC Service.

```java
interface MultiplicationService {
    @JsonRPC("Arith.Multiply") @POST("/rpc")
    Call<Integer> multiply(@Body MultiplicationArgs args);
}
```

Register the `JsonRPCConverterFactory` while building your `Retrofit` instance.
This must be done before any other converters are applied.

```java
Retrofit retrofit = new Retrofit.Builder()
        .baseUrl("http://localhost:1234")
        .addConverterFactory(JsonRPCConverterFactory.create())
        .addConverterFactory(MoshiConverterFactory.create())
        .build();
```

Use Retrofit to build your service.

```java
MultiplicationService service = retrofit.create(MultiplicationService.class);
```

Use your service.

```java
service.multiply(MultiplicationArgs.create(2, 3)).execute().body(); // -> 6
```

# Download

*Note*: Only snapshot releases are available currently.

Download [the latest JAR](https://oss.sonatype.org/content/repositories/snapshots/com/segment/retrofit/jsonrpc/jsonrpc/) or grab via Maven:
```xml
<dependency>
  <groupId>com.segment.retrofit.jsonrpc</groupId>
  <artifactId>jsonrpc</artifactId>
  <version>1.0.0-SNAPSHOT</version>
</dependency>
```

or Gradle:

```groovy
compile 'com.segment.retrofit.jsonrpc:jsonrpc:1.0.0-SNAPSHOT'
```

License added by cyonic but attributed to SegmentIO per [this](https://github.com/segmentio/retrofit-jsonrpc/issues/7)

MIT License

Copyright (c) [2018] [Segmentio]

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
