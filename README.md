CircularBuffer
==================================================
A circular buffer for Node.js with a simple read/write interface and <a href="#getStream">streaming support</a>.


Installation
--------------------------------------------------

The recommended method is to install the package from Github:

```shell
npm install 'cbarrick/CircularBuffer#v1.x' --save
```

Alternatively, you can install the package from the npm registry, but be aware that the package name is different:

```shell
npm install 'cbarrick-circular-buffer' --save
```


API
--------------------------------------------------

```javascript
var CircularBuffer = require('circular-buffer');
```

-----

### new CircularBuffer([options])

Constructs a circular buffer.

#### Arguments
- `options` *(Object)*:
	- `size` *(Number)*: The initial size of the buffer in bytes. Defaults to 1024.
	- `encoding` *(String | null)*: The default encoding to use to when converting to/from strings. If you pass `null` or `"buffer"`, then methods which access data will return buffers of octets. Defaults to `"utf8"`.

-----

### CircularBuffer#length

The number of bytes stored in the buffer.

-----

### CircularBuffer#size

The number of bytes allocated for the buffer. Note that this is ***not*** the size of the data stored in the buffer; that is `CircularBuffer#length`.

-----

### CircularBuffer#peek([n], [encoding])

Retrieve the first `n` bytes of the buffer. If the result would be decoded, partial characters are not returned.

#### Arguments
- `n` *(Number)*: The maximum number of bytes to retreive. Defaults to `Infinity`.
- `encoding` *(String | null)*: The encoding to use to decode the bytes into a string. If you pass `null` or `"buffer"`, the data will not be decoded and a buffer will be returned instead. The default is set by the constructor.

#### Returns
*(String | Buffer)* Returns the first `n` bytes as a string or a buffer if the encoding is null.


-----

### CircularBuffer#read([n], [encoding])

Consumes the first `n` bytes of the buffer. If the result would be decoded, partial characters are not read.

#### Arguments
- `n` *(Number)*: The maximum number of bytes to retrieve. Defaults to `Infinity`.
- `encoding` *(String | null)*: The encoding to use to decode the bytes into a string. If you pass `null`, the data will not be decoded and a buffer will be returned instead. The default is set by the constructor.

#### Returns
*(String | Buffer)* Returns the first `n` bytes as a string or a buffer if the encoding is null.

-----

### CircularBuffer#copy(targetBuffer, [targetStart], [sourceStart], [sourceEnd])

Copies data into a *regular* buffer. All arguments passed that are invalid or out of bounds are set to their defaults.

#### Arguments
- `targetBuffer` *(Buffer)*: Buffer into which data will be copied.
- `targetStart` *(Number)*: The index into the target which will hold the first byte. Defaults to `0`.
- `sourceStart` *(Number)*: The starting index to copy (inclusize). Defaults to `0`.
- `sourceEnd` *(Number)*: The end index to copy (exclusice). Defaults to `buffer.length`.

#### Returns
*(Number)* Returns the number of bytes copied.

-----

### CircularBuffer#slice([start, [end]], [encoding])

Returns a portion of the buffer from `start` to `end`. All arguments passed that are
invalid or out of bounds are set to their defaults. If the slice would be decoded and contains partial multibyte characters, the endpoints are rounded back to the beginning of the character.

#### Arguments
- `start` *(Number)*: The starting index of the slice (inclusive). Defaults to `0`.
- `end` *(Number)*: The end index of the slice (exclusive). Defaults to `buffer.length`.
- `encoding` *(String | null)*: The encoding to use to decode the bytes into a string. If you pass `null`, the data will not be decoded and a buffer will be returned instead. The default is set by the constructor.

#### Returns
*(String | Buffer)* Returns the slice as a string or a buffer if the encoding is null.

-----

### CircularBuffer#expand()

Doubles the storage capacity of the buffer. This method is automatically called when the buffer is full. There are very few cases when you should call this manually.

-----

### CircularBuffer#shrink()

Shrinks the storage capacity to the length of the data, rounded up to the nearest multiple of the initial capacity. There are very few cases when it is useful call this method.

-----

### CircularBuffer#write(chunk, [encoding])

Writes to the end of the buffer.

#### Arguments
- `chunk` *(String | Buffer)*: The data to be written.
- `encoding` *(String)*: If `chunk` is a string, how it should be encoded on the buffer. If `chunk` is a buffer, this is ignored. If the encoding is `null`, utf8 is used. The default is set by the constructor.

-----

### CircularBuffer#writeBack(chunk, [encoding])

Writes to the beginning of the buffer.

#### Arguments
- `chunk` *(String | Buffer)*: The data to be written.
- `encoding` *(String)*: If `chunk` is a string, how it should be encoded on the buffer. If `chunk` is a buffer, this is ignored. If the encoding is `null`, utf8 is used. The default is set by the constructor.

-----

<a name="getStream"></a>
### CircularBuffer#getStream()

Creates a Duplex Stream (i.e. both readable and writeable) backed by the buffer.

#### Returns
*(Stream)* Returns a stream interface for the buffer.

-----

### CircularBuffer#toString([encoding])

Returns the contents of the buffer as a string.

#### Arguments
- `encoding` *(String)*: How to decode the data.

#### Returns
*(String)*: Always returns a string, unlike `CircularBuffer#peek`.


License
--------------------------------------------------
(The ISC License)

Copyright (c) 2014, Chris Barrick <cbarrick1@gmail.com>

Permission to use, copy, modify, and/or distribute this software for any purpose with or without fee is hereby granted, provided that the above copyright notice and this permission notice appear in all copies.

THE SOFTWARE IS PROVIDED "AS IS" AND THE AUTHOR DISCLAIMS ALL WARRANTIES WITH REGARD TO THIS SOFTWARE INCLUDING ALL IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS. IN NO EVENT SHALL THE AUTHOR BE LIABLE FOR ANY SPECIAL, DIRECT, INDIRECT, OR CONSEQUENTIAL DAMAGES OR ANY DAMAGES WHATSOEVER RESULTING FROM LOSS OF USE, DATA OR PROFITS, WHETHER IN AN ACTION OF CONTRACT, NEGLIGENCE OR OTHER TORTIOUS ACTION, ARISING OUT OF OR IN CONNECTION WITH THE USE OR PERFORMANCE OF THIS SOFTWARE.
