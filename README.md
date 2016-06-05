# to2

A write stream constructor that supports a flush function that is called before `finish` is emitted

```
npm install to2
```

This module is an alias of [flush-write-stream][1] for better symmetry with
[from2][2].

[![build status](http://img.shields.io/travis/mafintosh/flush-write-stream.svg?style=flat)](http://travis-ci.org/mafintosh/flush-write-stream)

[1]: https://npmjs.com/package/flush-write-stream
[2]: https://npmjs.com/package/from2

## Usage

``` js
var writer = require('to2')

var ws = writer(write, flush)

ws.on('finish', function () {
  console.log('finished')
})

ws.write('hello')
ws.write('world')
ws.end()

function write (data, enc, cb) {
  // i am your normal ._write method
  console.log('writing', data.toString())
  cb()
}

function flush (cb) {
  // i am called before finish is emitted
  setTimeout(cb, 1000) // wait 1 sec
}
```

If you run the above it will produce the following output

```
writing hello
writing world
(nothing happens for 1 sec)
finished
```

## API

#### `var ws = writer([options], write, [flush])`

Create a new writable stream. Options are forwarded to the stream constructor.

#### `var ws = writer.obj([options], write, [flush])`

Same as the above except `objectMode` is set to `true` per default.

## License

MIT
