# Batch Stream [![JavaScript Style Guide](https://img.shields.io/badge/code_style-standard-brightgreen.svg)](https://standardjs.com)

> Transform stream supporting objectMode, which batches a bunch of input data into groups of specified size and will emit arrays, so that you can deal with pieces of input asynchronously.

## Install

> npm install --save batch-stream2

## Usage

```javascript
const BatchStream = require('batch-stream2')
const batch = new BatchStream({
  size : 5, // Bytes or N. of objects if objectMode is true
  objectMode: true, // false by default
  strictMode: false // return the rest of the batch when a stream contains a number of items that is not a strict multiply of the batch size
})

stream
  .pipe(batch)
  .pipe(new ArrayStream()) // In objectMode: true, deals with array input from pipe.
```

You can `.pipe` other streams to it or `.write` them yourself (if you `.write` don't forget to `.end`).

If `objectMode` is enabled the emitted batches are `Array` of length equal to `size`. Otherwise `Buffer` with byte `size`-length are emitted.

The `strictMode: false` allows to get the rest of the batch when a stream contains a number of items that is not a strict multiply of the batch size.

## Test

> npm test


### Author

Rocco Musolino ([@roccomuso](https://twitter.com/roccomuso))

### License

MIT
