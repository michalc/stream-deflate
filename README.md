# stream-inflate [![CircleCI](https://circleci.com/gh/michalc/stream-inflate.svg?style=shield)](https://circleci.com/gh/michalc/stream-inflate) [![Test Coverage](https://api.codeclimate.com/v1/badges/1131e6ac6efb36647a9b/test_coverage)](https://codeclimate.com/github/michalc/stream-inflate/test_coverage)

Uncompress Deflate and Deflate64 streams in pure Python.


## Installation

```bash
pip install stream-inflate
```


## Usage

To uncompress Deflate, use the `stream_inflate` function.

```python
from stream_inflate import stream_inflate
import httpx

def compressed_chunks():
    # Iterable that yields the bytes of a DEFLATE-compressed stream
    with httpx.stream('GET', 'https://www.example.com/my.txt') as r:
        yield from r.iter_raw(chunk_size=65536)

for uncompressed_chunk in stream_inflate(compressed_chunks()):
    print(uncompressed_chunk)
```

To uncompress Deflate64, use the stream_unflate64 function.

```python
from stream_inflate import stream_inflate64
import httpx

def compressed_chunks():
    # Iterable that yields the bytes of a DEFLATE64-compressed stream
    with httpx.stream('GET', 'https://www.example.com/my.txt') as r:
        yield from r.iter_raw(chunk_size=65536)

for uncompressed_chunk in stream_inflate64(compressed_chunks()):
    print(uncompressed_chunk)
```
