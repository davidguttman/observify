# observify-varhash

This is just a fork of [observify](https://github.com/maxogden/observify), but uses [observ-varhash](https://github.com/nrw/observ-varhash) for objects instead of [observ-struct](https://github.com/raynos/observ-struct) so that keys can be added and removed.

Converts JS objects into their [observable](https://github.com/raynos/mercury#observ) equivalents using [observ](https://github.com/Raynos/observ), [observ-array](https://github.com/Raynos/observ-array) and [observ-varhash](https://github.com/nrw/observ-varhash). Designed for use with [mercury](https://github.com/raynos/mercury)

[![NPM](https://nodei.co/npm/observify-varhash.png?global=true)](https://nodei.co/npm/observify-varhash/)

## installation

```
npm install observify-varhash
```

## usage

```js
var observify = require('observify-varhash')
var data = observify({
  "foo": "bar",
  "cats": ["taco", "burrito"],
  "age": 82
})
```

is equivalent to doing:

```js
var array = require('observ-array')
var varhash = require('observ-varhash')
var value = require('observ')

var data = varhash({
  "foo": value("bar"),
  "cats": array([value("taco"), value("burrito")]),
  "age": value(82)
})
```

## blacklisted properties

`observ-varhash` has a [blacklist](https://github.com/Raynos/observ-struct/blob/master/index.js) of property names that cannot be used as keys (as they clash with javascript reserved words).

You can pass an options object with a `autoRename` property to tell observify to rename these properties.

```js
var observify = require('observify-varhash')
var data = observify({
  "name":"I'm bad, I'm bad, you know it",
  "comment":"I am OK"
}, {
  autoRename:'$'
})

console.log(data())
```

This would print:

```js
{
  $name:"I'm bad, I'm bad, you know it",
  comment:"I am OK"
}
```

If `autoRename` is true it will default to `$`.
