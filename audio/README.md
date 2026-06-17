# audio/

Drop your `.opus` or `.m4a` files in here. They appear automatically on the
site, sorted by filename. `.opus` is decoded with a bundled WebAssembly
decoder (so it plays on Safari/iOS too); `.m4a` (AAC) plays natively on every
platform, including iOS & Windows. Prefix with numbers to control order, e.g.:

```
01-the-beginning.opus
02-the-twist.m4a
03-the-legend-grows.opus
```
