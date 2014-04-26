node-gnuplot
============

A super-thin wrapper around [gnuplot](http://www.gnuplot.info/) for node.js

## example

``` js
var gnuplot = require('gnuplot');
gnuplot()
    .set('term png')
    .set('output "out.png"')
    .set('title "Some Math Functions"')
    .set('xrange [-10:10]')
    .set('yrange [-2:2]')
    .set('zeroaxis')
    .plot('(x/4)**2, sin(x), 1/x')
    .end();
```
You can use streams!

``` js
var data = fs.createReadStream('input.dat'),
    out = fs.createWriteStream('output.svg'),
    plotter = gnuplot().set('term svg');
    
data.pipe(plotter).pipe(out);
```

# methods

``` js
var gnuplot = require('gnuplot')
```

## gnuplot()

Spawn a new gnuplot process and return a duplex stream combining `stdout` and `stdin`. In addition to the standard stream functions and events, the following syntactic sugar exists: `set`, `unset`, `plot`, `splot`. They all return the gnuplot object and therefor can be chained together:

``` js
gnuplot()
    .set('term png')
    .unset('output')
    .plot('[-6:6] sin(x)')
    .end();
```

To automatically call [end()](http://nodejs.org/api/stream.html#stream_writable_end_chunk_encoding_callback) on the input stream after a command, pass `{end: true}` as options:

``` js
gnuplot()
    .set('term png')
    .unset('output')
    .plot('[-6:6] sin(x)', {end: true})
    .pipe(fs.createWriteStream('out.png');
```

# install

With [npm](https://npmjs.org) do:

```
npm install gnuplot
```

You need to have [gnuplot](http://www.gnuplot.info/) installed. On OSX you can do this with [homebrew](http://brew.sh/):

```
brew install gnuplot
```


# license

MIT
